# MootMood — Database Schema Design

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Planning Phase

---

## Schema Overview

MootMood uses a relational PostgreSQL database to store legal authorities, case metadata, paragraph-level content, legal topic taxonomy, and citation configurations. The schema is designed for data integrity, query performance, and future extensibility.

### Design Principles

1. **Normalized:** Minimize data duplication
2. **Relational:** Use foreign keys and joins appropriately
3. **Typed:** Strong column types with constraints
4. **Indexed:** Strategic indexes for query performance
5. **Extensible:** Easy to add new entity types
6. **Auditable:** Track source verification and dates

---

## Entity Relationship Diagram

```
┌──────────────┐
│    Courts    │
└──────┬───────┘
       │ 1
       │
       │ N
┌──────┴───────────────────────────────┐
│             Cases                     │
│  - Full metadata                      │
│  - Official citations                 │
│  - Source URLs                        │
└──────┬───────────────────────┬───────┘
       │ 1                     │ N
       │                       │
       │ N                     │
┌──────┴────────┐       ┌─────┴──────────┐
│  Paragraphs   │       │  CaseTopics    │
│  - Text       │       │  (join table)  │
│  - Number     │       └─────┬──────────┘
└───────────────┘             │ N
                              │
                              │ 1
                      ┌───────┴──────────┐
                      │  LegalTopics     │
                      │  - Hierarchical  │
                      └──────────────────┘

┌──────────────────┐       ┌─────────────────────┐
│ CitationStyles   │   1   │ CitationTemplates   │
│ - OSCOLA        │───────│ - Format strings    │
│ - Bluebook      │   N   │ - Rules             │
└──────────────────┘       └─────────────────────┘
```

---

## Core Tables

### 1. Courts Table

Stores international courts and tribunals.

```sql
CREATE TABLE courts (
  id VARCHAR(50) PRIMARY KEY,           -- e.g., 'icj', 'icc', 'echr'
  full_name VARCHAR(255) NOT NULL,      -- "International Court of Justice"
  short_name VARCHAR(100) NOT NULL,     -- "ICJ"
  abbreviation VARCHAR(20) NOT NULL,    -- "ICJ" (for citations)
  description TEXT,                     -- Court description
  official_url VARCHAR(500),            -- https://www.icj-cij.org
  established_year INT,                 -- 1945
  location VARCHAR(100),                -- "The Hague, Netherlands"
  court_type VARCHAR(50),               -- 'international', 'regional', 'hybrid'
  jurisdiction_type VARCHAR(100),       -- 'general', 'criminal', 'human_rights'
  is_active BOOLEAN DEFAULT true,       -- Currently operating
  display_order INT DEFAULT 0,          -- For sorting in UI
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX courts_active_idx ON courts(is_active);
CREATE INDEX courts_type_idx ON courts(court_type);

-- Example data
INSERT INTO courts VALUES (
  'icj',
  'International Court of Justice',
  'ICJ',
  'ICJ',
  'The principal judicial organ of the United Nations',
  'https://www.icj-cij.org',
  1945,
  'The Hague, Netherlands',
  'international',
  'general',
  true,
  1
);
```

**Prisma Model:**
```prisma
model Court {
  id               String    @id
  fullName         String    @map("full_name")
  shortName        String    @map("short_name")
  abbreviation     String
  description      String?   @db.Text
  officialUrl      String?   @map("official_url")
  establishedYear  Int?      @map("established_year")
  location         String?
  courtType        String?   @map("court_type")
  jurisdictionType String?   @map("jurisdiction_type")
  isActive         Boolean   @default(true) @map("is_active")
  displayOrder     Int       @default(0) @map("display_order")
  createdAt        DateTime  @default(now()) @map("created_at")
  updatedAt        DateTime  @updatedAt @map("updated_at")
  
  cases            Case[]
  
  @@index([isActive])
  @@index([courtType])
  @@map("courts")
}
```

---

### 2. Cases Table

Stores legal authorities (judgments, orders, advisory opinions, etc.).

```sql
CREATE TABLE cases (
  id VARCHAR(100) PRIMARY KEY,              -- 'icj-1986-nicaragua'
  court_id VARCHAR(50) NOT NULL REFERENCES courts(id),
  
  -- Case names
  full_name VARCHAR(500) NOT NULL,          -- Full official name
  short_name VARCHAR(200) NOT NULL,         -- Short citation name
  alternative_names TEXT[],                 -- Array of alternative names
  
  -- Parties
  applicant VARCHAR(200),                   -- "Nicaragua"
  respondent VARCHAR(200),                  -- "United States of America"
  parties_full TEXT,                        -- Full party description
  
  -- Dates
  judgment_date DATE NOT NULL,              -- 1986-06-27
  year INT NOT NULL,                        -- 1986 (for filtering)
  filed_date DATE,                          -- When case was filed
  
  -- Document type
  document_type VARCHAR(50) NOT NULL,       -- 'judgment', 'order', 'advisory_opinion'
  procedural_stage VARCHAR(100),            -- 'merits', 'preliminary_objections', etc.
  
  -- Citations and sources
  official_citation VARCHAR(300),           -- "ICJ Reports 1986, p. 14"
  case_number VARCHAR(100),                 -- "1986/27" or similar
  official_url VARCHAR(500) NOT NULL,       -- Link to official source
  pdf_url VARCHAR(500),                     -- Link to PDF if available
  
  -- Content
  summary TEXT,                             -- Case summary
  has_full_text BOOLEAN DEFAULT false,      -- Whether we have full text
  paragraph_count INT DEFAULT 0,            -- Number of paragraphs
  
  -- Metadata
  language VARCHAR(10) DEFAULT 'en',        -- 'en', 'fr', etc.
  citation_page_number INT,                 -- Starting page in reports
  
  -- Verification and source tracking
  source_verified BOOLEAN DEFAULT false,    -- Verified against official source
  source_verified_date DATE,                -- When verified
  source_notes TEXT,                        -- Verification notes
  
  -- Search
  search_vector tsvector,                   -- Full-text search
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX cases_court_idx ON cases(court_id);
CREATE INDEX cases_year_idx ON cases(year);
CREATE INDEX cases_court_year_idx ON cases(court_id, year);
CREATE INDEX cases_document_type_idx ON cases(document_type);
CREATE INDEX cases_date_idx ON cases(judgment_date DESC);
CREATE INDEX cases_search_idx ON cases USING GIN(search_vector);

-- Foreign key
ALTER TABLE cases ADD CONSTRAINT fk_cases_court 
  FOREIGN KEY (court_id) REFERENCES courts(id);

-- Search vector trigger
CREATE TRIGGER cases_search_vector_update 
BEFORE INSERT OR UPDATE ON cases
FOR EACH ROW EXECUTE FUNCTION
  tsvector_update_trigger(
    search_vector, 'pg_catalog.english',
    full_name, short_name, official_citation, summary
  );
```

**Prisma Model:**
```prisma
model Case {
  id                  String    @id
  courtId             String    @map("court_id")
  
  // Names
  fullName            String    @map("full_name")
  shortName           String    @map("short_name")
  alternativeNames    String[]  @map("alternative_names")
  
  // Parties
  applicant           String?
  respondent          String?
  partiesFull         String?   @map("parties_full") @db.Text
  
  // Dates
  judgmentDate        DateTime  @map("judgment_date") @db.Date
  year                Int
  filedDate           DateTime? @map("filed_date") @db.Date
  
  // Document type
  documentType        String    @map("document_type")
  proceduralStage     String?   @map("procedural_stage")
  
  // Citations
  officialCitation    String?   @map("official_citation")
  caseNumber          String?   @map("case_number")
  officialUrl         String    @map("official_url")
  pdfUrl              String?   @map("pdf_url")
  
  // Content
  summary             String?   @db.Text
  hasFullText         Boolean   @default(false) @map("has_full_text")
  paragraphCount      Int       @default(0) @map("paragraph_count")
  
  // Metadata
  language            String    @default("en")
  citationPageNumber  Int?      @map("citation_page_number")
  
  // Verification
  sourceVerified      Boolean   @default(false) @map("source_verified")
  sourceVerifiedDate  DateTime? @map("source_verified_date") @db.Date
  sourceNotes         String?   @map("source_notes") @db.Text
  
  // Timestamps
  createdAt           DateTime  @default(now()) @map("created_at")
  updatedAt           DateTime  @updatedAt @map("updated_at")
  
  // Relations
  court               Court     @relation(fields: [courtId], references: [id])
  paragraphs          Paragraph[]
  topics              CaseTopic[]
  
  @@index([courtId])
  @@index([year])
  @@index([courtId, year])
  @@index([documentType])
  @@index([judgmentDate(sort: Desc)])
  @@map("cases")
}
```

---

### 3. Paragraphs Table

Stores individual paragraphs from cases with their text and metadata.

```sql
CREATE TABLE paragraphs (
  id SERIAL PRIMARY KEY,
  case_id VARCHAR(100) NOT NULL REFERENCES cases(id) ON DELETE CASCADE,
  
  -- Paragraph identification
  paragraph_number INT NOT NULL,        -- 115
  section_number VARCHAR(50),           -- "III.A.2" or similar
  heading VARCHAR(500),                 -- Section heading if applicable
  
  -- Content
  text TEXT NOT NULL,                   -- Full paragraph text
  text_length INT,                      -- Character count
  
  -- Location in document
  page_number INT,                      -- Page in official reports
  page_location VARCHAR(20),            -- 'top', 'middle', 'bottom'
  
  -- Search
  search_vector tsvector,
  
  -- Metadata
  is_heading BOOLEAN DEFAULT false,     -- Is this a heading/title?
  is_operative BOOLEAN DEFAULT false,   -- Is this operative paragraph?
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX paragraphs_case_idx ON paragraphs(case_id);
CREATE INDEX paragraphs_case_number_idx ON paragraphs(case_id, paragraph_number);
CREATE INDEX paragraphs_search_idx ON paragraphs USING GIN(search_vector);

-- Unique constraint: one paragraph number per case
CREATE UNIQUE INDEX paragraphs_case_number_unique 
  ON paragraphs(case_id, paragraph_number);

-- Foreign key
ALTER TABLE paragraphs ADD CONSTRAINT fk_paragraphs_case 
  FOREIGN KEY (case_id) REFERENCES cases(id) ON DELETE CASCADE;

-- Search vector trigger
CREATE TRIGGER paragraphs_search_vector_update 
BEFORE INSERT OR UPDATE ON paragraphs
FOR EACH ROW EXECUTE FUNCTION
  tsvector_update_trigger(
    search_vector, 'pg_catalog.english', text
  );
```

**Prisma Model:**
```prisma
model Paragraph {
  id               Int       @id @default(autoincrement())
  caseId           String    @map("case_id")
  
  // Identification
  paragraphNumber  Int       @map("paragraph_number")
  sectionNumber    String?   @map("section_number")
  heading          String?
  
  // Content
  text             String    @db.Text
  textLength       Int?      @map("text_length")
  
  // Location
  pageNumber       Int?      @map("page_number")
  pageLocation     String?   @map("page_location")
  
  // Flags
  isHeading        Boolean   @default(false) @map("is_heading")
  isOperative      Boolean   @default(false) @map("is_operative")
  
  // Timestamps
  createdAt        DateTime  @default(now()) @map("created_at")
  updatedAt        DateTime  @updatedAt @map("updated_at")
  
  // Relations
  case             Case      @relation(fields: [caseId], references: [id], onDelete: Cascade)
  topics           ParagraphTopic[]
  
  @@unique([caseId, paragraphNumber])
  @@index([caseId])
  @@index([caseId, paragraphNumber])
  @@map("paragraphs")
}
```

---

### 4. Legal Topics Table

Hierarchical taxonomy of legal topics for organizing authorities.

```sql
CREATE TABLE legal_topics (
  id VARCHAR(100) PRIMARY KEY,          -- 'use-of-force'
  parent_id VARCHAR(100) REFERENCES legal_topics(id),
  
  -- Topic information
  name VARCHAR(200) NOT NULL,           -- "Use of Force"
  slug VARCHAR(200) NOT NULL UNIQUE,    -- "use-of-force"
  description TEXT,                     -- Topic description
  
  -- Hierarchy
  level INT NOT NULL DEFAULT 0,         -- 0=top-level, 1=sub-topic, etc.
  path VARCHAR(500),                    -- "/public-intl-law/use-of-force"
  
  -- Display
  display_order INT DEFAULT 0,          -- Sort order within parent
  icon VARCHAR(50),                     -- Icon name (optional)
  color VARCHAR(20),                    -- Color code (optional)
  
  -- Metadata
  case_count INT DEFAULT 0,             -- Denormalized count
  is_active BOOLEAN DEFAULT true,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX topics_parent_idx ON legal_topics(parent_id);
CREATE INDEX topics_level_idx ON legal_topics(level);
CREATE INDEX topics_slug_idx ON legal_topics(slug);
CREATE INDEX topics_path_idx ON legal_topics(path);

-- Foreign key
ALTER TABLE legal_topics ADD CONSTRAINT fk_topics_parent 
  FOREIGN KEY (parent_id) REFERENCES legal_topics(id);
```

**Prisma Model:**
```prisma
model LegalTopic {
  id           String      @id
  parentId     String?     @map("parent_id")
  
  // Information
  name         String
  slug         String      @unique
  description  String?     @db.Text
  
  // Hierarchy
  level        Int         @default(0)
  path         String?
  
  // Display
  displayOrder Int         @default(0) @map("display_order")
  icon         String?
  color        String?
  
  // Metadata
  caseCount    Int         @default(0) @map("case_count")
  isActive     Boolean     @default(true) @map("is_active")
  
  // Timestamps
  createdAt    DateTime    @default(now()) @map("created_at")
  updatedAt    DateTime    @updatedAt @map("updated_at")
  
  // Relations
  parent       LegalTopic? @relation("TopicHierarchy", fields: [parentId], references: [id])
  children     LegalTopic[] @relation("TopicHierarchy")
  cases        CaseTopic[]
  paragraphs   ParagraphTopic[]
  
  @@index([parentId])
  @@index([level])
  @@index([slug])
  @@index([path])
  @@map("legal_topics")
}
```

---

### 5. Case Topics (Join Table)

Many-to-many relationship between cases and legal topics.

```sql
CREATE TABLE case_topics (
  id SERIAL PRIMARY KEY,
  case_id VARCHAR(100) NOT NULL REFERENCES cases(id) ON DELETE CASCADE,
  topic_id VARCHAR(100) NOT NULL REFERENCES legal_topics(id) ON DELETE CASCADE,
  
  -- Relevance metadata
  relevance_score DECIMAL(3, 2) DEFAULT 1.0,  -- 0.0 to 1.0
  is_primary BOOLEAN DEFAULT false,            -- Primary topic for case
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX case_topics_case_idx ON case_topics(case_id);
CREATE INDEX case_topics_topic_idx ON case_topics(topic_id);
CREATE UNIQUE INDEX case_topics_unique ON case_topics(case_id, topic_id);

-- Foreign keys
ALTER TABLE case_topics ADD CONSTRAINT fk_case_topics_case 
  FOREIGN KEY (case_id) REFERENCES cases(id) ON DELETE CASCADE;
ALTER TABLE case_topics ADD CONSTRAINT fk_case_topics_topic 
  FOREIGN KEY (topic_id) REFERENCES legal_topics(id) ON DELETE CASCADE;
```

**Prisma Model:**
```prisma
model CaseTopic {
  id              Int         @id @default(autoincrement())
  caseId          String      @map("case_id")
  topicId         String      @map("topic_id")
  
  // Metadata
  relevanceScore  Decimal     @default(1.0) @map("relevance_score") @db.Decimal(3, 2)
  isPrimary       Boolean     @default(false) @map("is_primary")
  
  // Timestamps
  createdAt       DateTime    @default(now()) @map("created_at")
  
  // Relations
  case            Case        @relation(fields: [caseId], references: [id], onDelete: Cascade)
  topic           LegalTopic  @relation(fields: [topicId], references: [id], onDelete: Cascade)
  
  @@unique([caseId, topicId])
  @@index([caseId])
  @@index([topicId])
  @@map("case_topics")
}
```

---

### 6. Paragraph Topics (Join Table)

Many-to-many relationship for paragraph-level topic tagging.

```sql
CREATE TABLE paragraph_topics (
  id SERIAL PRIMARY KEY,
  paragraph_id INT NOT NULL REFERENCES paragraphs(id) ON DELETE CASCADE,
  topic_id VARCHAR(100) NOT NULL REFERENCES legal_topics(id) ON DELETE CASCADE,
  
  -- Metadata
  relevance_score DECIMAL(3, 2) DEFAULT 1.0,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX paragraph_topics_paragraph_idx ON paragraph_topics(paragraph_id);
CREATE INDEX paragraph_topics_topic_idx ON paragraph_topics(topic_id);
CREATE UNIQUE INDEX paragraph_topics_unique 
  ON paragraph_topics(paragraph_id, topic_id);

-- Foreign keys
ALTER TABLE paragraph_topics ADD CONSTRAINT fk_paragraph_topics_paragraph 
  FOREIGN KEY (paragraph_id) REFERENCES paragraphs(id) ON DELETE CASCADE;
ALTER TABLE paragraph_topics ADD CONSTRAINT fk_paragraph_topics_topic 
  FOREIGN KEY (topic_id) REFERENCES legal_topics(id) ON DELETE CASCADE;
```

**Prisma Model:**
```prisma
model ParagraphTopic {
  id             Int        @id @default(autoincrement())
  paragraphId    Int        @map("paragraph_id")
  topicId        String     @map("topic_id")
  
  // Metadata
  relevanceScore Decimal    @default(1.0) @map("relevance_score") @db.Decimal(3, 2)
  
  // Timestamps
  createdAt      DateTime   @default(now()) @map("created_at")
  
  // Relations
  paragraph      Paragraph  @relation(fields: [paragraphId], references: [id], onDelete: Cascade)
  topic          LegalTopic @relation(fields: [topicId], references: [id], onDelete: Cascade)
  
  @@unique([paragraphId, topicId])
  @@index([paragraphId])
  @@index([topicId])
  @@map("paragraph_topics")
}
```

---

## Citation System Tables

### 7. Citation Styles Table

Stores citation style definitions.

```sql
CREATE TABLE citation_styles (
  id VARCHAR(50) PRIMARY KEY,           -- 'oscola', 'bluebook'
  name VARCHAR(100) NOT NULL,           -- "OSCOLA"
  full_name VARCHAR(200) NOT NULL,      -- "Oxford Standard for Citation of Legal Authorities"
  description TEXT,
  version VARCHAR(50),                  -- "4th edition"
  official_url VARCHAR(500),
  is_active BOOLEAN DEFAULT true,
  display_order INT DEFAULT 0,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Example data
INSERT INTO citation_styles VALUES (
  'oscola',
  'OSCOLA',
  'Oxford Standard for Citation of Legal Authorities',
  'Citation style commonly used in UK and international law',
  '4th edition',
  'https://www.law.ox.ac.uk/oscola',
  true,
  1
);

INSERT INTO citation_styles VALUES (
  'bluebook',
  'Bluebook',
  'The Bluebook: A Uniform System of Citation',
  'Citation style used in United States legal documents',
  '21st edition',
  'https://www.legalbluebook.com',
  true,
  2
);
```

**Prisma Model:**
```prisma
model CitationStyle {
  id          String    @id
  name        String
  fullName    String    @map("full_name")
  description String?   @db.Text
  version     String?
  officialUrl String?   @map("official_url")
  isActive    Boolean   @default(true) @map("is_active")
  displayOrder Int      @default(0) @map("display_order")
  
  // Timestamps
  createdAt   DateTime  @default(now()) @map("created_at")
  updatedAt   DateTime  @updatedAt @map("updated_at")
  
  // Relations
  templates   CitationTemplate[]
  
  @@map("citation_styles")
}
```

---

### 8. Citation Templates Table

Stores format templates for different document types and citation styles.

```sql
CREATE TABLE citation_templates (
  id SERIAL PRIMARY KEY,
  style_id VARCHAR(50) NOT NULL REFERENCES citation_styles(id),
  
  -- Template identification
  court_id VARCHAR(50) REFERENCES courts(id),  -- Specific court or NULL for all
  document_type VARCHAR(50),                    -- 'judgment', 'order', etc.
  template_type VARCHAR(50) NOT NULL,           -- 'full', 'short', 'pinpoint'
  
  -- Template format
  template TEXT NOT NULL,                       -- Template string with placeholders
  example TEXT,                                 -- Example output
  
  -- Rules (stored as JSON)
  rules JSONB,                                  -- Additional formatting rules
  
  -- Metadata
  description TEXT,
  is_active BOOLEAN DEFAULT true,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX templates_style_idx ON citation_templates(style_id);
CREATE INDEX templates_court_idx ON citation_templates(court_id);
CREATE INDEX templates_type_idx ON citation_templates(template_type);

-- Example data
INSERT INTO citation_templates (
  style_id, court_id, document_type, template_type, template, example
) VALUES (
  'oscola',
  'icj',
  'judgment',
  'full',
  '{{fullName}}, {{documentType}}, {{officialCitation}}',
  'Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14'
);

INSERT INTO citation_templates (
  style_id, court_id, document_type, template_type, template, example
) VALUES (
  'oscola',
  'icj',
  'judgment',
  'pinpoint',
  '{{fullName}}, {{documentType}}, {{officialCitation}}, para {{paragraph}}',
  'Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 115'
);
```

**Prisma Model:**
```prisma
model CitationTemplate {
  id           Int           @id @default(autoincrement())
  styleId      String        @map("style_id")
  
  // Identification
  courtId      String?       @map("court_id")
  documentType String?       @map("document_type")
  templateType String        @map("template_type")
  
  // Format
  template     String        @db.Text
  example      String?       @db.Text
  
  // Rules
  rules        Json?
  
  // Metadata
  description  String?       @db.Text
  isActive     Boolean       @default(true) @map("is_active")
  
  // Timestamps
  createdAt    DateTime      @default(now()) @map("created_at")
  updatedAt    DateTime      @updatedAt @map("updated_at")
  
  // Relations
  style        CitationStyle @relation(fields: [styleId], references: [id])
  court        Court?        @relation(fields: [courtId], references: [id])
  
  @@index([styleId])
  @@index([courtId])
  @@index([templateType])
  @@map("citation_templates")
}

// Add to Court model:
// templates    CitationTemplate[]
```

---

## Future Tables (Post-MVP)

### 9. Users Table (Phase 2)

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  full_name VARCHAR(200),
  
  -- Authentication (via Supabase)
  auth_id UUID UNIQUE NOT NULL,  -- Supabase auth.users.id
  
  -- Profile
  institution VARCHAR(300),
  role VARCHAR(100),              -- 'student', 'researcher', 'practitioner'
  
  -- Preferences
  default_citation_style VARCHAR(50),
  preferences JSONB,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  last_login TIMESTAMP
);
```

### 10. Research Projects Table (Phase 2)

```sql
CREATE TABLE research_projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  
  -- Project information
  name VARCHAR(300) NOT NULL,
  description TEXT,
  competition VARCHAR(200),       -- "Jessup 2027"
  role VARCHAR(100),              -- "Applicant", "Respondent"
  
  -- Metadata
  is_archived BOOLEAN DEFAULT false,
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### 11. Saved Authorities Table (Phase 2)

```sql
CREATE TABLE saved_authorities (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  project_id UUID REFERENCES research_projects(id) ON DELETE CASCADE,
  case_id VARCHAR(100) NOT NULL REFERENCES cases(id),
  
  -- Organization
  issue_name VARCHAR(300),        -- "Issue I: Jurisdiction"
  tags TEXT[],
  
  -- Notes
  notes TEXT,
  importance INT,                 -- 1-5 rating
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW()
);
```

### 12. Saved Paragraphs Table (Phase 2)

```sql
CREATE TABLE saved_paragraphs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  project_id UUID REFERENCES research_projects(id) ON DELETE CASCADE,
  paragraph_id INT NOT NULL REFERENCES paragraphs(id),
  
  -- Organization
  issue_name VARCHAR(300),
  tags TEXT[],
  
  -- Notes
  annotation TEXT,
  highlight_color VARCHAR(20),
  
  -- Timestamps
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## Sample Data Structure

### Example Case Record

```json
{
  "id": "icj-1986-nicaragua",
  "courtId": "icj",
  "fullName": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v. United States of America)",
  "shortName": "Nicaragua v United States",
  "alternativeNames": ["Nicaragua Case"],
  "applicant": "Nicaragua",
  "respondent": "United States of America",
  "judgmentDate": "1986-06-27",
  "year": 1986,
  "documentType": "judgment",
  "proceduralStage": "merits",
  "officialCitation": "ICJ Reports 1986, p. 14",
  "officialUrl": "https://www.icj-cij.org/case/70",
  "summary": "The Court found that the United States violated international law by supporting armed activities against Nicaragua...",
  "hasFullText": false,
  "paragraphCount": 292,
  "sourceVerified": true,
  "sourceVerifiedDate": "2026-11-01"
}
```

### Example Paragraph Record

```json
{
  "id": 1,
  "caseId": "icj-1986-nicaragua",
  "paragraphNumber": 115,
  "text": "In the case of military and paramilitary activities against Nicaragua, the Court finds that...",
  "pageNumber": 65,
  "topics": [
    {
      "topicId": "attribution",
      "relevanceScore": 1.0
    },
    {
      "topicId": "effective-control",
      "relevanceScore": 1.0
    }
  ]
}
```

### Example Legal Topic Hierarchy

```json
{
  "id": "public-international-law",
  "name": "Public International Law",
  "slug": "public-international-law",
  "level": 0,
  "children": [
    {
      "id": "state-responsibility",
      "name": "State Responsibility",
      "slug": "state-responsibility",
      "parentId": "public-international-law",
      "level": 1,
      "children": [
        {
          "id": "attribution",
          "name": "Attribution of Conduct",
          "slug": "attribution",
          "parentId": "state-responsibility",
          "level": 2,
          "children": []
        }
      ]
    }
  ]
}
```

---

## Database Migrations Strategy

### Initial Migration

```bash
# Create Prisma schema
npx prisma migrate dev --name init

# This creates:
# - All tables
# - All indexes
# - All constraints
# - Full-text search setup
```

### Seeding Strategy

```typescript
// prisma/seed.ts
import { PrismaClient } from '@prisma/client';
import courtsData from '../src/data/courts.json';
import topicsData from '../src/data/topics.json';
import casesData from '../src/data/cases/*.json';

const prisma = new PrismaClient();

async function main() {
  // 1. Seed courts
  for (const court of courtsData) {
    await prisma.court.upsert({
      where: { id: court.id },
      update: court,
      create: court
    });
  }
  
  // 2. Seed legal topics
  await seedTopics(topicsData);
  
  // 3. Seed cases
  for (const caseData of casesData) {
    await seedCase(caseData);
  }
  
  // 4. Seed citation styles
  await seedCitationStyles();
}

main();
```

---

## Performance Optimization

### Index Strategy

**Primary indexes** (created above):
- Full-text search (GIN indexes)
- Foreign keys
- Filter columns (court_id, year, document_type)
- Join table lookups

**Composite indexes:**
```sql
-- Common filter combinations
CREATE INDEX cases_court_year_type_idx 
  ON cases(court_id, year, document_type);

-- Topic + case lookup
CREATE INDEX case_topics_topic_primary_idx 
  ON case_topics(topic_id, is_primary);
```

### Query Optimization Tips

1. **Select specific columns** (avoid SELECT *)
2. **Use pagination** (LIMIT + OFFSET or cursor-based)
3. **Denormalize counts** where appropriate (case_count in topics)
4. **Use materialized views** for complex aggregations (future)
5. **Connection pooling** (via Prisma or pgBouncer)

---

## Data Integrity Constraints

### Constraints Applied

1. **NOT NULL** for required fields
2. **UNIQUE** constraints for identifiers
3. **FOREIGN KEY** constraints for relations
4. **CHECK** constraints for valid values
5. **ON DELETE CASCADE** for dependent records

### Example CHECK Constraints

```sql
-- Valid document types
ALTER TABLE cases ADD CONSTRAINT check_document_type 
  CHECK (document_type IN ('judgment', 'order', 'advisory_opinion', 'award'));

-- Valid court types
ALTER TABLE courts ADD CONSTRAINT check_court_type 
  CHECK (court_type IN ('international', 'regional', 'hybrid', 'national'));

-- Valid relevance score
ALTER TABLE case_topics ADD CONSTRAINT check_relevance_score 
  CHECK (relevance_score >= 0 AND relevance_score <= 1);
```

---

## Backup and Maintenance

### Backup Strategy

**Supabase automatic backups:**
- Daily automated backups
- Point-in-time recovery
- Manual backup on-demand

**Export strategy:**
```bash
# Export entire database
pg_dump $DATABASE_URL > backup.sql

# Export specific tables
pg_dump $DATABASE_URL -t cases -t paragraphs > cases_backup.sql
```

### Maintenance Tasks

```sql
-- Update statistics for query planner
ANALYZE;

-- Rebuild indexes if needed
REINDEX INDEX cases_search_idx;

-- Vacuum to reclaim space
VACUUM ANALYZE;
```

---

## Complete Prisma Schema

See the complete `prisma/schema.prisma` file in the next artifact.

---

**END OF DATABASE SCHEMA DOCUMENT**
