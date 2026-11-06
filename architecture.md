# MootMood — Technical Architecture Document

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Planning Phase

---

## Architecture Overview

MootMood is built as a modern, server-rendered web application using Next.js 14+ with the App Router, PostgreSQL for data persistence, and TypeScript for type safety. The architecture prioritizes simplicity, maintainability, and legal data accuracy.

### Architecture Principles

1. **Server-first:** Use React Server Components for optimal performance
2. **Type-safe:** Strict TypeScript throughout the stack
3. **Simple:** Avoid unnecessary complexity and dependencies
4. **Scalable:** Design for growth from 100 to 10,000+ authorities
5. **Accurate:** Data integrity over feature quantity
6. **Maintainable:** Clear separation of concerns

---

## Technology Stack

### Frontend Layer

**Framework:** Next.js 14+ (App Router)
- Server Components by default
- Client Components only when interactivity required
- Server Actions for mutations
- Route handlers for API endpoints
- Static generation for public pages

**Language:** TypeScript 5+
- Strict mode enabled
- Comprehensive type definitions
- No `any` types without justification

**Styling:** Tailwind CSS 3+
- Utility-first approach
- Custom design system configuration
- Responsive design utilities
- Dark mode support (future)

**UI Components:** shadcn/ui
- Accessible components built on Radix UI
- Customizable with Tailwind
- Copy-paste component model
- Tree-shakeable

**Icons:** Lucide React
- Consistent professional iconography
- Small bundle size
- Wide icon coverage

### Backend Layer

**Runtime:** Node.js 20+ LTS
- Native ES modules
- Modern JavaScript features
- Stable and performant

**API Layer:** Next.js App Router
- Server Actions for mutations
- Route handlers for RESTful endpoints
- Server Components for data fetching
- API middleware for logging/rate limiting

**Database:** PostgreSQL 15+
- Relational data model
- Full-text search (MVP)
- JSONB for flexible metadata
- Robust transaction support

**Database Access:**
- **Option A (Recommended):** Prisma ORM
  - Type-safe queries
  - Schema migrations
  - Developer experience
  - Auto-generated types
  
- **Option B:** Direct SQL with Postgres.js
  - Maximum control
  - No ORM overhead
  - Raw SQL queries
  - Manual type definitions

**Decision:** Start with Prisma for MVP, evaluate performance later

### Search Layer

**Phase 1 (MVP):** PostgreSQL Full-Text Search
- `tsvector` and `tsquery` for full-text indexing
- Trigram similarity for fuzzy matching
- JSON aggregation for faceted filters
- Adequate for 1,000+ documents

**Phase 2 (Future):** Meilisearch
- Dedicated search engine
- Better relevance ranking
- Typo tolerance
- Faceted search
- < 50ms search latency

**Migration Path:**
- Abstract search interface
- Implement PostgreSQL adapter
- Implement Meilisearch adapter
- Switch via configuration

### Deployment Infrastructure

**Hosting:** Vercel
- Automatic deployments from GitHub
- Edge network (CDN)
- Serverless functions
- Zero configuration
- Built-in CI/CD

**Database Hosting:**
- **Option A:** Supabase
  - Managed PostgreSQL
  - Automatic backups
  - Connection pooling
  - Free tier for MVP
  - Built-in authentication (future)

- **Option B:** Neon or Railway
  - Managed PostgreSQL
  - Generous free tier
  - Good performance

**Decision:** Supabase recommended for integrated auth path

**Domain & DNS:** Managed externally (future)

**SSL/TLS:** Automatic via Vercel

---

## Application Architecture

### Directory Structure

```
mootmood/
├── .kiro/                      # Kiro configuration
│   └── steering/               # Project steering files
├── prisma/                     # Database schema and migrations
│   ├── schema.prisma          # Prisma schema
│   ├── migrations/            # Migration files
│   └── seed.ts                # Database seeding script
├── public/                     # Static assets
│   ├── logo.svg               # MootMood logo
│   └── favicon.ico            # Favicon
├── src/
│   ├── app/                   # Next.js App Router
│   │   ├── layout.tsx         # Root layout
│   │   ├── page.tsx           # Homepage
│   │   ├── search/            # Search results page
│   │   │   └── page.tsx
│   │   ├── cases/             # Case detail pages
│   │   │   └── [id]/
│   │   │       └── page.tsx
│   │   ├── topics/            # Browse by legal topic
│   │   │   └── [slug]/
│   │   │       └── page.tsx
│   │   ├── courts/            # Browse by court
│   │   │   └── [slug]/
│   │   │       └── page.tsx
│   │   └── api/               # API routes
│   │       ├── search/
│   │       └── citations/
│   ├── components/            # React components
│   │   ├── ui/               # shadcn/ui components
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── card.tsx
│   │   │   └── ...
│   │   ├── layout/           # Layout components
│   │   │   ├── header.tsx
│   │   │   ├── footer.tsx
│   │   │   └── sidebar.tsx
│   │   ├── search/           # Search components
│   │   │   ├── search-bar.tsx
│   │   │   ├── search-filters.tsx
│   │   │   ├── search-results.tsx
│   │   │   └── result-card.tsx
│   │   ├── legal/            # Legal document components
│   │   │   ├── case-metadata.tsx
│   │   │   ├── document-reader.tsx
│   │   │   ├── paragraph-viewer.tsx
│   │   │   └── citation-generator.tsx
│   │   └── browse/           # Browse components
│   │       ├── topic-tree.tsx
│   │       └── court-list.tsx
│   ├── lib/                  # Utility functions and core logic
│   │   ├── db/              # Database queries
│   │   │   ├── cases.ts     # Case queries
│   │   │   ├── search.ts    # Search queries
│   │   │   └── topics.ts    # Topic queries
│   │   ├── citation/        # Citation generation
│   │   │   ├── types.ts     # Citation types
│   │   │   ├── oscola.ts    # OSCOLA formatter
│   │   │   ├── bluebook.ts  # Bluebook formatter
│   │   │   └── generator.ts # Main citation engine
│   │   ├── search/          # Search logic
│   │   │   ├── query-builder.ts
│   │   │   ├── filters.ts
│   │   │   └── ranking.ts
│   │   ├── utils.ts         # General utilities
│   │   └── constants.ts     # Application constants
│   ├── types/               # TypeScript type definitions
│   │   ├── case.ts          # Case types
│   │   ├── citation.ts      # Citation types
│   │   ├── search.ts        # Search types
│   │   └── index.ts         # Type exports
│   └── data/                # Seed data (JSON)
│       ├── cases/           # Case JSON files
│       ├── topics.json      # Legal topics taxonomy
│       └── courts.json      # Court metadata
├── tests/                   # Test files
│   ├── unit/               # Unit tests
│   │   ├── citation/       # Citation tests
│   │   └── search/         # Search tests
│   └── integration/        # Integration tests
├── .env.example            # Environment variables template
├── .env.local              # Local environment (gitignored)
├── .gitignore             # Git ignore rules
├── next.config.js         # Next.js configuration
├── tailwind.config.ts     # Tailwind configuration
├── tsconfig.json          # TypeScript configuration
├── package.json           # Dependencies
├── README.md              # Project documentation
└── requirements.md        # This file (requirements spec)
```

---

## Data Architecture

### Entity Relationship Overview

```
Courts (1) ─────< (N) Cases
Cases (1) ─────< (N) Paragraphs
Cases (N) >────< (N) LegalTopics (via CaseTopics join table)
Paragraphs (N) >────< (N) LegalTopics (via ParagraphTopics join table)
CitationStyles (1) ─────< (N) CitationTemplates
```

### Core Entities

See `database-schema.md` for complete schema definition.

**Key entities:**
1. **Courts** — International courts and tribunals
2. **Cases** — Legal authorities (judgments, orders, opinions)
3. **Paragraphs** — Individual numbered paragraphs within cases
4. **LegalTopics** — Hierarchical legal topic taxonomy
5. **CaseTopics** — Many-to-many relationship
6. **ParagraphTopics** — Paragraph-level topic tagging
7. **CitationStyles** — Citation format definitions
8. **CitationTemplates** — Style-specific templates

---

## Component Architecture

### Page Components

**1. Homepage (`app/page.tsx`)**
- Server Component
- Static generation
- Fetches recent cases
- Displays search hero
- Shows topic categories

**2. Search Results (`app/search/page.tsx`)**
- Server Component with URL search params
- Handles query parameters
- Executes search with filters
- Renders results grid
- SEO metadata

**3. Case Detail (`app/cases/[id]/page.tsx`)**
- Server Component
- Dynamic route with static params generation
- Fetches case + paragraphs
- Metadata display
- Document reader
- Citation generator integration

**4. Topic Browse (`app/topics/[slug]/page.tsx`)**
- Server Component
- Lists cases by topic
- Breadcrumb navigation
- Filter options

**5. Court Browse (`app/courts/[slug]/page.tsx`)**
- Server Component
- Lists cases by court
- Court metadata display
- Filter options

### Shared Components

**Layout Components:**
- `Header` — Navigation, logo, search
- `Footer` — Links, copyright, contact
- `Sidebar` — Filters and navigation

**Search Components:**
- `SearchBar` — Input with suggestions (Client Component)
- `SearchFilters` — Filter UI (Client Component)
- `SearchResults` — Results grid (Server Component)
- `ResultCard` — Individual result (Server Component)

**Legal Components:**
- `CaseMetadata` — Case information display
- `DocumentReader` — Paragraph-numbered document viewer
- `ParagraphViewer` — Individual paragraph with actions (Client Component)
- `CitationGenerator` — Citation style selector and generator (Client Component)
- `CopyButton` — Copy-to-clipboard with feedback (Client Component)

**Browse Components:**
- `TopicTree` — Hierarchical topic navigation (Client Component)
- `CourtList` — Court directory
- `TopicTag` — Topic badge/chip

### State Management

**Server State:**
- React Server Components fetch data
- No global state on server
- Each request is independent

**Client State:**
- React `useState` for local component state
- React `useReducer` for complex state (filters)
- URL search params for shareable state
- Local storage for user preferences (future)

**No global state management library needed for MVP**

---

## Search Architecture

### PostgreSQL Full-Text Search Implementation

#### 1. Text Search Configuration

**Create search columns:**
```sql
-- Add tsvector column to cases table
ALTER TABLE cases 
ADD COLUMN search_vector tsvector;

-- Create index for fast full-text search
CREATE INDEX cases_search_idx 
ON cases USING GIN(search_vector);

-- Update search vector on insert/update
CREATE TRIGGER cases_search_update 
BEFORE INSERT OR UPDATE ON cases
FOR EACH ROW EXECUTE FUNCTION
  tsvector_update_trigger(
    search_vector, 'pg_catalog.english',
    full_name, short_name, official_citation
  );

-- Add search vector for paragraphs
ALTER TABLE paragraphs 
ADD COLUMN search_vector tsvector;

CREATE INDEX paragraphs_search_idx 
ON paragraphs USING GIN(search_vector);
```

#### 2. Search Query Structure

**Basic keyword search:**
```typescript
// Search cases by keyword
const results = await prisma.$queryRaw`
  SELECT 
    c.id,
    c.full_name,
    c.short_name,
    c.court_id,
    c.year,
    ts_rank(c.search_vector, query) AS rank
  FROM cases c,
       to_tsquery('english', ${searchTerm}) query
  WHERE c.search_vector @@ query
  ORDER BY rank DESC
  LIMIT 20;
`;
```

**Topic-filtered search:**
```typescript
// Search with topic filter
const results = await prisma.case.findMany({
  where: {
    search_vector: {
      matches: searchTerm
    },
    topics: {
      some: {
        topic_id: {
          in: selectedTopicIds
        }
      }
    }
  },
  include: {
    court: true,
    topics: {
      include: {
        topic: true
      }
    }
  },
  orderBy: {
    // Custom ranking logic
  },
  take: 20
});
```

#### 3. Faceted Filtering

**Count documents by facet:**
```typescript
// Get filter counts
const facets = await prisma.$queryRaw`
  SELECT 
    court_id,
    COUNT(*) as count
  FROM cases
  WHERE ${whereConditions}
  GROUP BY court_id;
`;
```

#### 4. Paragraph-Level Search

**Search within paragraphs:**
```typescript
const paragraphResults = await prisma.paragraph.findMany({
  where: {
    text: {
      search: searchTerm
    }
  },
  include: {
    case: {
      include: {
        court: true
      }
    }
  },
  orderBy: {
    // Rank by relevance
  }
});
```

### Search Result Ranking

**Ranking factors:**
1. Text relevance (ts_rank)
2. Exact phrase matches (boost)
3. Title matches vs body matches (weight)
4. Recency (year of judgment)
5. Citation count (future)

**Ranking formula:**
```typescript
const rankWeight = {
  caseNameMatch: 2.0,
  citationMatch: 1.5,
  paragraphMatch: 1.0,
  topicMatch: 1.2,
  recency: (year: number) => year > 2010 ? 1.1 : 1.0
};
```

---

## Citation Generation Architecture

### Citation Engine Design

**Architecture Pattern:** Strategy Pattern

```typescript
interface CitationFormatter {
  formatFull(caseData: CaseMetadata): string;
  formatShort(caseData: CaseMetadata): string;
  formatPinpoint(caseData: CaseMetadata, paragraph: number): string;
  formatFootnote(caseData: CaseMetadata): string;
  validate(caseData: CaseMetadata): ValidationResult;
}

class OSCOLAFormatter implements CitationFormatter {
  formatFull(caseData: CaseMetadata): string {
    // OSCOLA format implementation
  }
  // ... other methods
}

class BluebookFormatter implements CitationFormatter {
  formatFull(caseData: CaseMetadata): string {
    // Bluebook format implementation
  }
  // ... other methods
}

class CitationGenerator {
  private formatters: Map<string, CitationFormatter>;
  
  constructor() {
    this.formatters = new Map([
      ['oscola', new OSCOLAFormatter()],
      ['bluebook', new BluebookFormatter()]
    ]);
  }
  
  generate(
    style: string,
    caseData: CaseMetadata,
    options?: CitationOptions
  ): CitationResult {
    const formatter = this.formatters.get(style);
    if (!formatter) {
      throw new Error(`Unknown citation style: ${style}`);
    }
    
    // Validate metadata
    const validation = formatter.validate(caseData);
    if (!validation.isValid) {
      return {
        citation: null,
        errors: validation.errors,
        warnings: validation.warnings
      };
    }
    
    // Generate citation
    const citation = options?.paragraph
      ? formatter.formatPinpoint(caseData, options.paragraph)
      : formatter.formatFull(caseData);
    
    return {
      citation,
      style,
      metadata: caseData,
      generatedAt: new Date()
    };
  }
}
```

### Citation Validation

**Required metadata by style:**

**OSCOLA:**
- Case name (full) ✓
- Court ✓
- Year ✓
- Report citation OR official citation ✓
- Paragraph number (for pinpoint) ✓

**Bluebook:**
- Case name (parties abbreviated) ✓
- Court abbreviation ✓
- Year ✓
- Report citation ✓
- Page number OR paragraph number ✓
- Date of judgment ✓

**Validation flow:**
```typescript
interface ValidationResult {
  isValid: boolean;
  errors: string[];  // Missing required fields
  warnings: string[]; // Missing optional fields
}

function validateForOSCOLA(metadata: CaseMetadata): ValidationResult {
  const errors: string[] = [];
  const warnings: string[] = [];
  
  if (!metadata.fullName) errors.push('Case name required');
  if (!metadata.court) errors.push('Court required');
  if (!metadata.year) errors.push('Year required');
  if (!metadata.officialCitation) warnings.push('Citation incomplete');
  
  return {
    isValid: errors.length === 0,
    errors,
    warnings
  };
}
```

---

## API Architecture

### API Routes

**Search API:**
```
GET /api/search
Query params:
  - q: string (search query)
  - topics: string[] (topic slugs)
  - courts: string[] (court slugs)
  - yearFrom: number
  - yearTo: number
  - page: number
  - limit: number

Response:
{
  results: CaseResult[],
  total: number,
  page: number,
  facets: {
    courts: { slug: string, count: number }[],
    topics: { slug: string, count: number }[],
    years: { year: number, count: number }[]
  }
}
```

**Citation Generation API:**
```
POST /api/citations/generate
Body:
{
  caseId: string,
  style: 'oscola' | 'bluebook',
  paragraph?: number,
  format: 'full' | 'short' | 'pinpoint'
}

Response:
{
  citation: string,
  style: string,
  warnings?: string[]
}
```

### Server Actions

**Copy actions (for better UX):**
```typescript
// Server Action for logging copies (future analytics)
async function logCitationCopy(
  caseId: string,
  style: string,
  paragraph?: number
) {
  'use server';
  
  // Log to analytics
  await analytics.track('citation_copied', {
    caseId,
    style,
    paragraph
  });
}
```

---

## Security Considerations

### MVP Security (Public Read-Only)

**No authentication required:**
- All data is publicly accessible
- No user accounts
- No sensitive data
- No write operations from users

**Basic protections:**
1. **Rate limiting** on search API
2. **Input validation** for search queries
3. **SQL injection prevention** via Prisma
4. **XSS protection** via React (auto-escaping)
5. **CORS configuration** (same-origin only)

### Future Security (Phase 2)

**When authentication is added:**
1. **Supabase Auth** for user management
2. **Row-level security** in PostgreSQL
3. **JWT tokens** for API authentication
4. **CSRF protection** for mutations
5. **Rate limiting per user**

---

## Performance Optimization

### Database Optimization

**Indexes:**
```sql
-- Full-text search
CREATE INDEX cases_search_idx ON cases USING GIN(search_vector);
CREATE INDEX paragraphs_search_idx ON paragraphs USING GIN(search_vector);

-- Filter queries
CREATE INDEX cases_court_year_idx ON cases(court_id, year);
CREATE INDEX cases_year_idx ON cases(year);

-- Join tables
CREATE INDEX case_topics_case_idx ON case_topics(case_id);
CREATE INDEX case_topics_topic_idx ON case_topics(topic_id);

-- Paragraph lookups
CREATE INDEX paragraphs_case_idx ON paragraphs(case_id);
CREATE INDEX paragraphs_number_idx ON paragraphs(paragraph_number);
```

**Query optimization:**
- Use `SELECT` specific columns (avoid `SELECT *`)
- Implement pagination (LIMIT + OFFSET)
- Use `EXPLAIN ANALYZE` to optimize slow queries
- Add database connection pooling

### Frontend Optimization

**Next.js features:**
- Static generation for homepage, topic pages
- Dynamic rendering for search results
- Incremental Static Regeneration for case pages
- Image optimization with `next/image`

**Component optimization:**
- Server Components for static content
- Client Components only for interactivity
- Lazy loading for heavy components
- Code splitting by route

**Caching strategy:**
```typescript
// Cache case data for 1 hour
export const revalidate = 3600;

// Cache search results for 5 minutes
const searchResults = await fetch('/api/search', {
  next: { revalidate: 300 }
});
```

### Bundle Optimization

**Techniques:**
- Tree-shaking unused code
- Dynamic imports for heavy components
- Minimize client-side JavaScript
- Use Server Components aggressively
- Optimize font loading (next/font)

---

## Testing Strategy

### Unit Tests

**Citation formatting:**
```typescript
describe('OSCOLA Citation Formatter', () => {
  test('formats full ICJ judgment citation', () => {
    const citation = oscola.formatFull(nicaraguaCase);
    expect(citation).toBe(
      'Military and Paramilitary Activities in and against Nicaragua ' +
      '(Nicaragua v United States of America), Judgment, ' +
      'ICJ Reports 1986, p 14'
    );
  });
  
  test('formats pinpoint paragraph citation', () => {
    const citation = oscola.formatPinpoint(nicaraguaCase, 115);
    expect(citation).toContain('para 115');
  });
  
  test('handles missing metadata gracefully', () => {
    const result = oscola.generate(incompleteCaseData);
    expect(result.errors).toContain('Missing official citation');
  });
});
```

**Search query builder:**
```typescript
describe('Search Query Builder', () => {
  test('builds basic keyword query', () => {
    const query = buildSearchQuery('self-defence');
    expect(query).toMatchObject({
      where: { search_vector: { matches: 'self-defence' } }
    });
  });
  
  test('applies topic filters', () => {
    const query = buildSearchQuery('force', {
      topics: ['use-of-force', 'self-defence']
    });
    expect(query.where.topics.some).toBeDefined();
  });
});
```

### Integration Tests

**Search workflow:**
```typescript
describe('Search Workflow', () => {
  test('user can search and view results', async () => {
    const response = await fetch('/api/search?q=nicaragua');
    const data = await response.json();
    
    expect(data.results).toHaveLength(1);
    expect(data.results[0].fullName).toContain('Nicaragua');
  });
  
  test('user can filter by court', async () => {
    const response = await fetch('/api/search?courts=icj');
    const data = await response.json();
    
    expect(data.results.every(r => r.court.slug === 'icj')).toBe(true);
  });
});
```

**Citation generation workflow:**
```typescript
describe('Citation Generation Workflow', () => {
  test('generates OSCOLA citation from case page', async () => {
    const response = await fetch('/api/citations/generate', {
      method: 'POST',
      body: JSON.stringify({
        caseId: 'icj-1986-nicaragua',
        style: 'oscola',
        paragraph: 115
      })
    });
    
    const data = await response.json();
    expect(data.citation).toContain('para 115');
  });
});
```

### End-to-End Tests (Future)

Use Playwright for critical user journeys:
1. Homepage → Search → View case → Copy citation
2. Browse topics → Filter → View case
3. View case → Jump to paragraph → Copy paragraph + citation

---

## Deployment Architecture

### Vercel Deployment

**Build configuration:**
```javascript
// next.config.js
module.exports = {
  output: 'standalone', // For Docker (future)
  experimental: {
    serverActions: true
  },
  images: {
    domains: ['www.icj-cij.org'] // External images
  }
};
```

**Environment variables:**
```bash
# .env.example
DATABASE_URL=postgresql://user:password@host:5432/mootmood
DIRECT_URL=postgresql://user:password@host:5432/mootmood

# Future variables
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

**Deployment process:**
1. Push to GitHub main branch
2. Vercel auto-deploys
3. Run database migrations (Prisma Migrate)
4. Seed database (first deploy only)
5. Build Next.js application
6. Deploy to edge network

### Database Deployment

**Supabase setup:**
1. Create Supabase project
2. Copy connection string
3. Add to Vercel environment variables
4. Enable connection pooling
5. Configure backup schedule

**Migration strategy:**
```bash
# Development
npx prisma migrate dev

# Production
npx prisma migrate deploy
```

---

## Monitoring & Observability (Future)

### Application Monitoring

**Options:**
- Vercel Analytics (built-in)
- Sentry for error tracking
- Logtail for structured logging

**Key metrics:**
- Search query latency
- Database query performance
- API response times
- Error rates
- User engagement

### Database Monitoring

**Supabase dashboard:**
- Connection count
- Query performance
- Table sizes
- Index usage

---

## Development Workflow

### Local Development Setup

```bash
# 1. Clone repository
git clone https://github.com/[username]/mootmood.git
cd mootmood

# 2. Install dependencies
npm install

# 3. Setup database
# Create Supabase project or local PostgreSQL

# 4. Configure environment
cp .env.example .env.local
# Edit .env.local with database credentials

# 5. Run migrations
npx prisma migrate dev

# 6. Seed database
npx prisma db seed

# 7. Start development server
npm run dev

# 8. Open browser
# http://localhost:3000
```

### Development Commands

```bash
# Development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run tests
npm test

# Run linter
npm run lint

# Format code
npm run format

# Database commands
npx prisma studio        # Visual database editor
npx prisma migrate dev   # Create migration
npx prisma generate      # Generate Prisma Client
npx prisma db seed       # Seed database
```

---

## Risk Mitigation

### Technical Risks

**Risk 1: PostgreSQL full-text search insufficient**
- **Mitigation:** Abstract search interface for easy migration
- **Fallback:** Meilisearch integration prepared

**Risk 2: Database performance at scale**
- **Mitigation:** Proper indexing, query optimization
- **Fallback:** Connection pooling, read replicas

**Risk 3: Citation generation complexity**
- **Mitigation:** Start with two well-documented styles
- **Fallback:** Manual citation with template hints

**Risk 4: Vercel serverless limits**
- **Mitigation:** Monitor function duration and memory
- **Fallback:** Move to Docker container deployment

---

## Migration Paths

### Search Migration (PostgreSQL → Meilisearch)

**Phase 1:** Abstract search interface
```typescript
interface SearchAdapter {
  search(query: SearchQuery): Promise<SearchResults>;
  index(documents: Document[]): Promise<void>;
}

class PostgresSearchAdapter implements SearchAdapter { ... }
class MeilisearchAdapter implements SearchAdapter { ... }
```

**Phase 2:** Implement Meilisearch adapter

**Phase 3:** Run both in parallel (testing)

**Phase 4:** Switch to Meilisearch

**Phase 5:** Remove PostgreSQL search

### Authentication Migration (None → Supabase)

**Phase 1:** Add Supabase client

**Phase 2:** Implement optional sign-in

**Phase 3:** Add user-specific features (saved searches)

**Phase 4:** Maintain public access for non-authenticated users

---

## Conclusion

This architecture provides:
- ✅ Clear separation of concerns
- ✅ Type safety throughout
- ✅ Scalability from MVP to production
- ✅ Simple deployment process
- ✅ Migration paths for future enhancements
- ✅ Maintainable codebase
- ✅ Professional developer experience

**Next Steps:**
1. Review and approve architecture
2. Create database schema (see `database-schema.md`)
3. Initialize Next.js project
4. Set up Prisma
5. Begin MVP development

---

**END OF ARCHITECTURE DOCUMENT**
