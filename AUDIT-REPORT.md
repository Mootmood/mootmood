# MootMood — Phase 0 Audit Report

**Date:** November 6, 2026  
**Audit Type:** Comprehensive Technical & Product Review  
**Auditor:** Kiro AI Development Partner  
**Status:** Pre-Implementation Validation

---

## Executive Summary

I have conducted a comprehensive audit of all MootMood planning documents by reading the actual file contents and analyzing their internal consistency, technical feasibility, and legal accuracy requirements.

**Overall Assessment:** ⚠️ **GOOD WITH CORRECTIONS NEEDED**

The planning is comprehensive and well-structured, but I have identified **12 critical issues** that must be addressed before implementation begins. Most issues are **scope clarification** and **legal taxonomy refinements** rather than fundamental architecture problems.

**Recommendation:** **PROCEED TO IMPLEMENTATION** after addressing the corrections documented in this report.

---

## 1. Files Audited

### Core Documentation (All Files Read and Analyzed)
✅ **README.md** — 465 lines, complete  
✅ **PROJECT-OVERVIEW.md** — 547 lines, complete  
✅ **requirements.md** — 855 lines, complete  
✅ **architecture.md** — 1,047 lines, complete  
✅ **database-schema.md** — 932 lines, complete  
✅ **development-roadmap.md** — 861 lines, complete  
✅ **PLANNING-COMPLETE.md** — 525 lines, complete  

### Steering Files (All Files Read and Analyzed)
✅ **.kiro/steering/mootmood-product-vision.md** — 77 lines  
✅ **.kiro/steering/ui-ux-standards.md** — 275 lines  
✅ **.kiro/steering/legal-research-accuracy.md** — 82 lines  
✅ **.kiro/steering/technical-conventions.md** — 131 lines  

**Total Documentation:** ~5,000 lines reviewed

---

## 2. Critical Issues Identified

### Issue 1: MVP Scope Confusion — Research Workspace ⚠️ CRITICAL

**Problem:**
The requirements document lists **Feature 5: Research Workspace** as **"Priority: MEDIUM (Phase 3)"**, but it's included in the "Core Features — MVP Scope" section (lines 81-425 of requirements.md).

**Evidence:**
```
requirements.md, line 427:
### Feature 5: Research Workspace
**Priority:** MEDIUM (Phase 3)
```

But it appears under "Core Features — MVP Scope" heading.

Multiple other documents correctly classify Research Workspace as **POST-MVP**:
- development-roadmap.md: "Phase 9: Research Workspace (Weeks 18-21)"
- PROJECT-OVERVIEW.md: "Post-MVP Phases — Phase 9: Research Workspace"
- database-schema.md: Tables 11-12 marked "Future Tables (Post-MVP)"

**Impact:**
- Confusing scope definition
- Risk of scope creep during implementation
- Unclear MVP completion criteria

**Recommended Fix:**
1. **REMOVE Research Workspace from MVP scope entirely**
2. Move Feature 5 to "Post-MVP Features" section in requirements.md
3. Keep save functionality references as "(future phase)" notes
4. MVP should NOT include:
   - User authentication
   - Saved cases/paragraphs
   - Research projects
   - Export functionality

**MVP Copy Actions Should Be:**
- Copy Paragraph (to clipboard)
- Copy Citation (to clipboard)
- Copy Paragraph + Citation (to clipboard)

That's it. No database persistence of user data in MVP.

---

### Issue 2: Legal Topic Taxonomy — Missing Granularity ⚠️ HIGH

**Problem:**
The legal topic taxonomy in requirements.md (lines 102-148) lists broad categories but doesn't show the **hierarchical relationships** clearly. Some critical distinctions are missing.

**Current Structure:**
```
USE OF FORCE (top level)
- Prohibition of the Use of Force
- Self-Defence under Article 51
- Individual Self-Defence
- Collective Self-Defence
- Armed Attack
- Necessity
- Proportionality
- Anticipatory and Pre-emptive Self-Defence
- Intervention by Invitation
- Humanitarian Intervention
- Collective Security
```

**Missing Critical Sub-Topics:**
1. **Attribution** is listed under "Public International Law" but should ALSO appear under "State Responsibility" as a sub-topic
2. **Effective Control** is mentioned in examples but not in the taxonomy
3. **Overall Control** is not mentioned at all
4. **Jus Cogens / Peremptory Norms** is not in the taxonomy (should be under "Sources of International Law")

**Recommendation:**
Create a **three-level hierarchy** for MVP:

**Level 1: Major Area** (e.g., "Use of Force")  
**Level 2: Doctrine/Principle** (e.g., "Self-Defence under Article 51")  
**Level 3: Specific Test/Standard** (e.g., "Effective Control Test")

**Revised USE OF FORCE Taxonomy:**
```
USE OF FORCE
├── Prohibition of the Use of Force (Article 2(4))
│   ├── Armed Attack (Article 51)
│   ├── Threat of Force
│   └── Intervention vs. Use of Force
├── Self-Defence
│   ├── Individual Self-Defence
│   ├── Collective Self-Defence
│   ├── Imminence and Necessity
│   ├── Proportionality
│   └── Anticipatory/Pre-emptive Self-Defence (Controversial)
├── Intervention
│   ├── Non-Intervention Principle
│   ├── Intervention by Invitation
│   ├── Humanitarian Intervention (Controversial)
│   └── Coercion
└── Collective Security
    ├── UN Security Council Authorization
    └── Collective Action
```

**Revised STATE RESPONSIBILITY Taxonomy:**
```
STATE RESPONSIBILITY
├── Attribution of Conduct to States
│   ├── State Organs
│   ├── Effective Control Test (Nicaragua)
│   ├── Overall Control Test (Tadić)
│   └── De Facto Organs
├── Internationally Wrongful Acts
│   ├── Breach of International Obligation
│   └── Circumstances Precluding Wrongfulness
├── Consequences
│   ├── Cessation
│   ├── Reparation
│   └── Satisfaction
└── Invocation of Responsibility
```

**Add to SOURCES OF INTERNATIONAL LAW:**
```
SOURCES OF INTERNATIONAL LAW
├── Treaties
├── Custom
│   ├── State Practice
│   └── Opinio Juris
├── General Principles of Law
├── Judicial Decisions
├── Teachings of Publicists
└── Jus Cogens / Peremptory Norms
    ├── Prohibition of Genocide
    ├── Prohibition of Torture
    ├── Prohibition of Slavery
    └── Prohibition of Aggression
```

---

### Issue 3: Citation Metadata Requirements — Incomplete Specification ⚠️ HIGH

**Problem:**
The citation architecture (architecture.md lines 540-605) defines "Required Metadata for Citations" but doesn't fully specify what happens when metadata is **partially available** or in **non-standard formats**.

**Current Specification (architecture.md):**
```typescript
interface ValidationResult {
  isValid: boolean;
  errors: string[];  // Missing required fields
  warnings: string[]; // Missing optional fields
}
```

**Missing Specifications:**

1. **What if ICJ Reports citation is missing but URL exists?**
   - Should system generate "ICJ (Year)" format?
   - Or should it refuse to generate citation?

2. **What if paragraph number exists but page number doesn't?**
   - OSCOLA: Can use "para X" alone
   - Bluebook: Prefers page numbers

3. **What if case has multiple judgments (preliminary objections, merits, interpretation)?**
   - How to distinguish?
   - Different citations needed?

4. **What if parties' names are very long?**
   - When to use short form?
   - How to generate abbreviations?

5. **Advisory Opinions vs. Contentious Cases**
   - Different citation formats
   - Different required metadata

**Recommended Fix:**
Create a **Citation Metadata Matrix** document specifying:

| Document Type | Required Fields | Optional Fields | Fallback Strategy |
|---------------|----------------|----------------|-------------------|
| ICJ Judgment | case_name, year, court | official_citation, page | Generate "[Court] [Year]" if citation missing |
| ICJ Advisory Opinion | case_name, year, court | official_citation | Include "Advisory Opinion" in format |
| ICC Judgment | case_name, case_number, year | official_citation | Use case number format |

**Implementation Strategy:**
1. Define `CitationMetadata` interface with **required vs optional** fields clearly marked
2. Define **fallback templates** for missing optional fields
3. **Refuse to generate citation** if required fields are missing (return error)
4. **Generate warning** if optional fields are missing (but still generate citation)

---

### Issue 4: Database Schema — Citation Templates Table Design Issue ⚠️ MEDIUM

**Problem:**
The `citation_templates` table (database-schema.md lines 718-760) uses a **template string** approach with placeholders like `{{fullName}}`, but the architecture doesn't specify:

1. **Who creates these templates?** (Admin? Developer? Seeded data?)
2. **How are they validated?** (What if placeholder doesn't match metadata field?)
3. **How to handle edge cases?** (Missing fields in template)

**Current Design:**
```sql
CREATE TABLE citation_templates (
  id SERIAL PRIMARY KEY,
  style_id VARCHAR(50) NOT NULL,
  court_id VARCHAR(50),  -- Specific court or NULL for all
  document_type VARCHAR(50),
  template_type VARCHAR(50) NOT NULL, -- 'full', 'short', 'pinpoint'
  template TEXT NOT NULL,  -- Template string with placeholders
  example TEXT,
  rules JSONB,
  ...
);
```

**Recommendation:**
For MVP, **SIMPLIFY** citation generation:

1. **REMOVE `citation_templates` table from MVP**
2. **Hard-code citation formatters** in TypeScript (as originally designed in architecture.md)
3. **Use template table in Phase 2** when adding custom competition profiles

**Rationale:**
- MVP only needs OSCOLA + Bluebook
- Hard-coded formatters are easier to test and validate
- Template system adds complexity without immediate value
- Can migrate to templates later when adding custom styles

**Revised MVP Citation Strategy:**
```typescript
// lib/citation/oscola.ts
export class OSCOLAFormatter implements CitationFormatter {
  formatFullICJJudgment(metadata: CaseMetadata): string {
    const { fullName, documentType, officialCitation } = metadata;
    return `${fullName}, ${documentType}, ${officialCitation}`;
  }
  
  formatPinpointICJJudgment(metadata: CaseMetadata, para: number): string {
    return `${this.formatFullICJJudgment(metadata)}, para ${para}`;
  }
}

// lib/citation/bluebook.ts
export class BluebookFormatter implements CitationFormatter {
  formatFullICJJudgment(metadata: CaseMetadata): string {
    const shortName = this.generateShortName(metadata);
    const { year, citationPageNumber, judgmentDate } = metadata;
    return `${shortName}, ${year} ICJ Rep. ${citationPageNumber} (${this.formatDate(judgmentDate)})`;
  }
}
```

**Database Change for MVP:**
- Keep `citation_styles` table (simple: id, name, description)
- Remove `citation_templates` table
- Add it back in Phase 13 (Citation Profiles)

---

### Issue 5: Search Architecture — Unrealistic Relevance Ranking ⚠️ MEDIUM

**Problem:**
The architecture document (architecture.md lines 449-473) proposes a custom relevance ranking formula:

```typescript
const rankWeight = {
  caseNameMatch: 2.0,
  citationMatch: 1.5,
  paragraphMatch: 1.0,
  topicMatch: 1.2,
  recency: (year: number) => year > 2010 ? 1.1 : 1.0
};
```

But PostgreSQL's `ts_rank()` function doesn't support this level of customization easily.

**Reality Check:**
PostgreSQL full-text search provides `ts_rank()` and `ts_rank_cd()` which calculate relevance based on:
- Term frequency
- Document length
- Position of matches

You **cannot easily** factor in "case name match vs paragraph match" weights without complex custom SQL.

**Recommended MVP Approach:**
Use **simple, proven PostgreSQL ranking**:

```sql
-- Simple ranking query
SELECT 
  c.id,
  c.full_name,
  c.short_name,
  ts_rank(c.search_vector, query) AS rank
FROM cases c,
     to_tsquery('english', 'self & defence') query
WHERE c.search_vector @@ query
ORDER BY rank DESC;
```

**Add secondary sorting:**
```sql
ORDER BY 
  ts_rank(c.search_vector, query) DESC,
  c.year DESC,  -- Recency as tiebreaker
  c.full_name ASC;
```

**For Topic Filtering:**
Use separate query logic, not weighting:

```sql
-- Topic-filtered search
SELECT c.*, ts_rank(c.search_vector, query) AS rank
FROM cases c
JOIN case_topics ct ON c.id = ct.case_id
WHERE c.search_vector @@ query
  AND ct.topic_id IN ('self-defence', 'use-of-force')
ORDER BY rank DESC;
```

**Defer complex ranking to Phase 12** (Meilisearch migration).

---

### Issue 6: Initial Dataset — Overly Ambitious for MVP ⚠️ MEDIUM

**Problem:**
Requirements specify **15-20 ICJ cases** (requirements.md line 614) with **20+ key paragraphs per case** = **300+ paragraphs to manually extract and verify**.

**Reality Check:**
This is a **substantial data entry task**:
- Find official ICJ sources
- Verify case metadata
- Read each judgment
- Identify relevant paragraphs
- Extract text (copy-paste, OCR from PDF, or type)
- Verify paragraph numbers
- Tag with legal topics
- Record source verification

**Estimated time:** 1-2 hours per case × 15 cases = **15-30 hours of data work**

**Recommendation:**
**START WITH 5 LANDMARK CASES** for MVP prototype:

1. **Nicaragua v United States (1986)** — Use of Force, Self-Defence, Intervention, Attribution
2. **Oil Platforms (Iran v United States) (2003)** — Self-Defence, Necessity, Proportionality
3. **Armed Activities (DRC v Uganda) (2005)** — Use of Force, Occupation, Attribution
4. **Legality of Use of Force (Serbia v Belgium) (2004)** — Jurisdiction, Use of Force (Preliminary Objections)
5. **Nuclear Weapons Advisory Opinion (1996)** — Use of Force, IHL, Self-Defence

**15-25 paragraphs per case = 75-125 total paragraphs**

**Expand to 15-20 cases in Phase 6** (Dataset Expansion) after proving the system works.

**Benefits:**
- Faster MVP delivery
- Proves the concept works
- Easier to maintain data quality
- Can refine extraction process before scaling

---

### Issue 7: Development Timeline — Unrealistic Estimates ⚠️ MEDIUM

**Problem:**
The roadmap estimates **17 weeks total** (development-roadmap.md line 781), but:
- Phase 6 (Initial Dataset) = 2 weeks
- For 15-20 cases with manual verification
- While also building features in Phases 1-5

**Reality Check:**
- Phase 1-5 development: **10 weeks** (reasonable)
- Manual data extraction: **3-4 weeks** (if done properly)
- Testing & polish: **2 weeks** (minimum)

**More Realistic Timeline:**

| Phase | Description | Duration | Notes |
|-------|-------------|----------|-------|
| 0 | Planning | ✅ Complete | Done |
| 1 | Infrastructure | 2 weeks | Database, UI components |
| 2 | Homepage & Browse | 2 weeks | Topics, courts |
| 3 | Search | 2-3 weeks | Complex feature |
| 4 | Document Reader | 2 weeks | Paragraph navigation |
| 5 | Citation Engine | 2-3 weeks | Needs thorough testing |
| 6 | Initial Dataset | **1 week** | **5 cases only** |
| 7 | Testing & Polish | 2 weeks | Critical QA phase |
| 8 | MVP Launch | 1 week | Deployment |

**Revised Total: 14-16 weeks** for a **5-case MVP**

Or: **18-20 weeks** for a **15-case MVP**

**Recommendation:**
Accept the longer timeline or reduce initial case count.

---

### Issue 8: PostgreSQL Full-Text Search — Missing Configuration Details ⚠️ LOW

**Problem:**
The database schema (database-schema.md lines 195-208) shows:

```sql
CREATE TRIGGER cases_search_vector_update 
BEFORE INSERT OR UPDATE ON cases
FOR EACH ROW EXECUTE FUNCTION
  tsvector_update_trigger(
    search_vector, 'pg_catalog.english',
    full_name, short_name, official_citation, summary
  );
```

But doesn't specify:
1. **Language configuration** — What about French judgments? (ICJ uses English + French)
2. **Stop words** — Should legal terms like "court", "case" be excluded?
3. **Synonym support** — How to handle "self-defence" vs "self-defense"?

**Recommendation:**
For MVP:
1. **Use 'english' configuration only** (as shown)
2. **Defer multilingual support** to Phase 10+
3. **Add basic synonym handling** via search query transformation:

```typescript
function expandSearchTerms(query: string): string {
  const synonyms: Record<string, string[]> = {
    'self-defence': ['self-defence', 'self-defense', 'self defence'],
    'judgement': ['judgement', 'judgment'],
    'organisation': ['organisation', 'organization']
  };
  
  // Transform query to include synonyms using OR
  // "self-defence" → "self-defence | self-defense"
}
```

4. **Document this limitation** in MVP release notes

---

### Issue 9: Technology Stack — Unnecessary "Option A vs Option B" ⚠️ LOW

**Problem:**
The architecture document presents **multiple options** for several technologies:

- Database Access: "Option A: Prisma" vs "Option B: Direct SQL"
- Database Hosting: "Option A: Supabase" vs "Option B: Neon or Railway"

**Issue:**
This creates decision paralysis and suggests uncertainty about the architecture.

**Recommendation:**
**REMOVE ALL "OPTION B" ALTERNATIVES**

**Definitive Stack for MVP:**
- **Database Access:** Prisma (decision made, stick with it)
- **Database Hosting:** Supabase (integrates auth for Phase 2, good free tier)
- **Hosting:** Vercel (no alternatives needed, it's the obvious choice for Next.js)

**Rationale:**
- Prisma provides excellent TypeScript integration
- Supabase offers managed PostgreSQL + future auth
- These are proven, well-documented choices
- Making a decision is better than leaving options open

Update architecture.md to remove all "Option A vs Option B" sections.

---

### Issue 10: Missing: First Milestone Definition ⚠️ HIGH

**Problem:**
The planning documents don't define a **clear first deliverable** — the smallest working prototype that proves the concept.

**What's Missing:**
- Specific user story
- Exact case(s) to include
- Specific acceptance criteria
- Definition of "working prototype"

**Recommended First Milestone: "Self-Defence Search Prototype"**

**Scope:**
- **1 case:** Nicaragua v United States (1986)
- **10 paragraphs:** Paragraphs 115, 176, 188, 190, 194, 195, 200, 211, 228, 292
- **1 topic:** Self-Defence under Article 51
- **1 court:** ICJ
- **2 citation styles:** OSCOLA, Bluebook

**User Story:**
```
As a moot court participant,
I want to search for "self-defence" or "Nicaragua",
So that I can find the Nicaragua v United States case,
View paragraph 195 about the requirements for self-defence,
Copy the paragraph with an OSCOLA citation,
And paste it into my memorial.
```

**Acceptance Criteria:**
1. ✅ Homepage loads with search bar
2. ✅ Search "self-defence" returns Nicaragua case
3. ✅ Search "nicaragua" returns Nicaragua case
4. ✅ Click case → opens document page
5. ✅ See case metadata (name, court, date, citation)
6. ✅ See 10 paragraphs with numbers
7. ✅ Click "Jump to paragraph 195" → scrolls to paragraph
8. ✅ Click "Copy Paragraph" → copies text to clipboard
9. ✅ Select "OSCOLA" citation style
10. ✅ Click "Copy Citation" → copies formatted citation
11. ✅ Click "Copy Paragraph + Citation" → copies both
12. ✅ Verify OSCOLA citation matches reference example
13. ✅ Verify Bluebook citation matches reference example
14. ✅ All data verified against official ICJ source

**Timeline:** Weeks 1-10 (Phases 0-4)

**Deliverable:** Working prototype deployed to Vercel test environment

---

### Issue 11: Missing: Source Verification Procedure ⚠️ HIGH

**Problem:**
The legal accuracy requirements (`.kiro/steering/legal-research-accuracy.md`) state:

> "Start with 10–20 carefully verified case records"

But **NO PROCEDURE** is defined for what "verified" means.

**What's Missing:**
1. Verification checklist
2. Who verifies (you? me? both?)
3. Documentation requirements
4. How to handle discrepancies
5. Re-verification schedule

**Recommended Verification Procedure:**

**Level 1: Metadata Verification**
- [ ] Visit official ICJ case page
- [ ] Verify full case name (exact spelling)
- [ ] Verify parties (Applicant vs Respondent)
- [ ] Verify judgment date
- [ ] Verify official ICJ Reports citation
- [ ] Verify case number
- [ ] Copy official URL
- [ ] Check if PDF is available
- [ ] Record verification date

**Level 2: Paragraph Verification**
For each paragraph:
- [ ] Open official PDF (if available) OR visit ICJ website
- [ ] Locate paragraph number in document
- [ ] Copy paragraph text (exact wording)
- [ ] Verify page number (if applicable)
- [ ] Note any formatting issues (tables, footnotes, etc.)
- [ ] Confirm paragraph is publically accessible

**Level 3: Citation Verification**
- [ ] Generate OSCOLA citation from metadata
- [ ] Compare against official OSCOLA guide examples
- [ ] Generate Bluebook citation
- [ ] Compare against Bluebook manual examples
- [ ] Test both citations in Microsoft Word
- [ ] Document any format ambiguities

**Verification Record:**
```json
{
  "caseId": "icj-1986-nicaragua",
  "verificationDate": "2026-11-15",
  "verifiedBy": "Your Name",
  "sourceUrl": "https://www.icj-cij.org/case/70",
  "metadataVerified": true,
  "paragraphsVerified": [115, 176, 188, ...],
  "citationsVerified": ["oscola", "bluebook"],
  "notes": "All paragraphs verified against official PDF",
  "issues": []
}
```

**Include this in each case's JSON data file.**

---

### Issue 12: Missing: .gitignore and Environment Configuration ⚠️ MEDIUM

**Problem:**
The planning documents mention creating `.env.example` (development-roadmap.md line 50), but don't specify:

1. What variables are needed
2. What should be in `.gitignore`
3. How to handle secrets in Vercel

**Recommended `.env.example`:**
```bash
# Database (Supabase or local PostgreSQL)
DATABASE_URL="postgresql://user:password@host:5432/mootmood"
DIRECT_URL="postgresql://user:password@host:5432/mootmood"

# Supabase (for Phase 2 auth)
# NEXT_PUBLIC_SUPABASE_URL=
# NEXT_PUBLIC_SUPABASE_ANON_KEY=
# SUPABASE_SERVICE_ROLE_KEY=

# Environment
NODE_ENV="development"

# Optional: Analytics (future)
# NEXT_PUBLIC_GA_ID=
```

**Recommended `.gitignore`:**
```
# Dependencies
node_modules/
.pnp/
.pnp.js

# Testing
coverage/
.nyc_output/

# Next.js
.next/
out/
build/
dist/

# Environment variables
.env
.env.local
.env.*.local

# Debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# IDEs
.vscode/
.idea/
*.swp
*.swo
*~

# OS
.DS_Store
Thumbs.db

# Prisma
prisma/*.db
prisma/*.db-journal

# Vercel
.vercel
```

---

## 3. Core Product Concept Validation ✅ APPROVED

**Assessment:** The core concept is **sound and properly addresses user needs**.

### Primary Workflow: ✅ FULLY SUPPORTED

1. ✅ **Search for legal topic** → Supported via hierarchical topic taxonomy + keyword search
2. ✅ **Discover relevant authorities** → Search results with topic tags + filters
3. ✅ **Identify relevant paragraphs** → Paragraph-level search + topic tagging
4. ✅ **Read original legal text** → Document reader with official source links
5. ✅ **Copy paragraphs** → One-click copy functionality
6. ✅ **Generate citations** → OSCOLA + Bluebook formatters
7. ✅ **Copy paragraph + citation** → Combined copy functionality

**No fundamental changes needed to support this workflow.**

### Additional Validation:

**Search Engine:** ✅ Well-designed
- Keyword search across multiple fields
- Topic-based filtering
- Court and year filters
- Faceted navigation

**Citation Generator:** ✅ Architecture is sound
- Strategy pattern allows multiple formats
- Validation system prevents fabrication
- Template-based generation (needs simplification for MVP, see Issue #4)

**Document Reader:** ✅ Appropriate for use case
- Paragraph navigation
- Jump to paragraph
- Copy functionality
- Metadata display

---

## 4. Revised MVP Scope

### MVP Features: ESSENTIAL ONLY

#### ✅ INCLUDE IN MVP

**A. Advanced Legal Search** (CRITICAL)
- Keyword search (PostgreSQL full-text)
- Legal topic filters (hierarchical browse + filter)
- Court filter (checkbox list)
- Year filter (range or dropdown)
- Search results with excerpts
- Simple relevance ranking (`ts_rank` + year)
- Pagination (20 results per page)

**B. Legal Authority Database** (CRITICAL)
- Case metadata (full schema as designed)
- Official source links (required for every case)
- Paragraph records (with text and numbers)
- Legal topic associations (many-to-many)
- Source verification tracking (status + date)

**C. Document Reader** (CRITICAL)
- Case detail page
- Metadata display sidebar
- Paragraph viewer with numbers in gutter
- Jump to paragraph input
- Copy paragraph button (to clipboard)
- Within-document search (browser Ctrl+F is sufficient for MVP)

**D. Citation Generator** (CRITICAL)
- OSCOLA formatter (hard-coded in TypeScript)
- Bluebook formatter (hard-coded in TypeScript)
- Full citation format
- Pinpoint paragraph citation
- Citation validation (required metadata check)
- Copy citation button
- Copy paragraph + citation button
- Warnings for missing optional fields

**E. Browse Interface** (HIGH)
- Homepage with search hero
- Legal topics page (hierarchical display)
- Browse cases by topic
- Court directory page
- Browse cases by court

#### ❌ REMOVE FROM MVP (Move to Post-MVP)

**F. Research Workspace** → Phase 9 (Post-MVP)
- User accounts
- Save cases
- Save paragraphs
- Research projects
- Export functionality

**G. Advanced Features** → Future Phases
- Within-document search with highlighting (sufficient to use browser find)
- Search suggestions/autocomplete → Phase 12
- Synonym expansion (add basic version if time permits)
- Advanced citation profiles → Phase 13
- Multiple document types (focus on ICJ judgments only for MVP)
- Treaty database → Phase 11
- UN resolutions → Phase 11

#### ⚠️ SIMPLIFY FOR MVP

**Citation Templates Table** → Remove from MVP database
- Hard-code formatters instead
- Add template system in Phase 13

**Search Relevance Ranking** → Use simple PostgreSQL ranking
- Defer custom weights to Phase 12 (Meilisearch)

**Initial Dataset** → 5 cases instead of 15-20
- Prove concept first
- Expand in Phase 6

---

## 5. Revised Legal Topic Taxonomy

### Recommended MVP Taxonomy (Manageable, Expandable)

I recommend a **three-level hierarchy** with **clear parent-child relationships**:

**Level 1:** Major Legal Area (6 categories)  
**Level 2:** Doctrine or Principle (20-30 topics)  
**Level 3:** Specific Test or Standard (optional for MVP, 10-20 subtopics)

### Complete Revised Taxonomy:

```
1. PUBLIC INTERNATIONAL LAW
   ├── 1.1 Sources of International Law
   │   ├── Treaties
   │   ├── Customary International Law
   │   ├── General Principles of Law
   │   └── Jus Cogens (Peremptory Norms)
   ├── 1.2 State Responsibility
   │   ├── Attribution of Conduct
   │   │   ├── State Organs
   │   │   ├── Effective Control Test
   │   │   ├── Overall Control Test
   │   │   └── De Facto Organs
   │   ├── Internationally Wrongful Acts
   │   ├── Cessation and Reparation
   │   └── Circumstances Precluding Wrongfulness
   ├── 1.3 Jurisdiction
   │   ├── Territorial Jurisdiction
   │   ├── Extraterritorial Jurisdiction
   │   └── Universal Jurisdiction
   ├── 1.4 State Immunity
   │   ├── Sovereign Immunity
   │   ├── Exceptions to Immunity
   │   └── Immunity of State Officials
   ├── 1.5 Diplomatic Protection
   └── 1.6 International Dispute Settlement
       ├── Jurisdiction of International Courts
       └── Preliminary Objections

2. USE OF FORCE
   ├── 2.1 Prohibition of Use of Force (Article 2(4))
   │   ├── Definition of "Use of Force"
   │   ├── Threat of Force
   │   └── Distinction: Intervention vs. Use of Force
   ├── 2.2 Self-Defence (Article 51)
   │   ├── Armed Attack Requirement
   │   ├── Individual Self-Defence
   │   ├── Collective Self-Defence
   │   ├── Necessity and Immediacy
   │   ├── Proportionality
   │   └── Anticipatory / Pre-emptive Self-Defence
   ├── 2.3 Non-Intervention
   │   ├── Prohibition of Intervention
   │   ├── Coercion
   │   ├── Internal Affairs
   │   └── Intervention by Invitation
   ├── 2.4 Humanitarian Intervention
   ├── 2.5 Collective Security
   │   └── UN Security Council Authorization

3. INTERNATIONAL HUMANITARIAN LAW
   ├── 3.1 Classification of Armed Conflicts
   │   ├── International Armed Conflict (IAC)
   │   ├── Non-International Armed Conflict (NIAC)
   │   └── Internationalized Armed Conflict
   ├── 3.2 Conduct of Hostilities
   │   ├── Distinction
   │   ├── Proportionality in Attack
   │   ├── Military Necessity
   │   ├── Precautions in Attack
   │   └── Direct Participation in Hostilities
   ├── 3.3 Protection of Persons
   │   ├── Protection of Civilians
   │   ├── Prisoners of War
   │   ├── Wounded and Sick
   │   └── Humanitarian Relief
   ├── 3.4 Occupation
   │   ├── Law of Occupation
   │   ├── Rights and Duties of Occupying Power
   │   └── Protected Persons under Occupation
   └── 3.5 Prohibited Weapons
       └── Indiscriminate Weapons

4. INTERNATIONAL CRIMINAL LAW
   ├── 4.1 Modes of Liability
   │   ├── Individual Criminal Responsibility
   │   ├── Command Responsibility
   │   ├── Joint Criminal Enterprise
   │   ├── Aiding and Abetting
   │   └── Incitement
   ├── 4.2 Core International Crimes
   │   ├── Genocide
   │   ├── Crimes Against Humanity
   │   ├── War Crimes
   │   └── Crime of Aggression
   └── 4.3 Defenses and Immunities
       ├── Superior Orders
       └── Head of State Immunity

5. INTERNATIONAL HUMAN RIGHTS LAW
   ├── 5.1 Civil and Political Rights
   │   ├── Right to Life
   │   ├── Prohibition of Torture
   │   ├── Right to Fair Trial
   │   └── Freedom of Expression
   ├── 5.2 State Obligations
   │   ├── Obligation to Respect
   │   ├── Obligation to Protect
   │   └── Obligation to Fulfill
   ├── 5.3 Extraterritorial Application
   │   └── Jurisdiction and Control
   ├── 5.4 Derogation
   │   └── Derogation in Emergencies
   └── 5.5 Human Rights in Armed Conflict
       └── Interaction with IHL

6. LAW OF THE SEA
   ├── 6.1 Maritime Zones
   │   ├── Territorial Sea
   │   ├── Contiguous Zone
   │   ├── Exclusive Economic Zone (EEZ)
   │   └── Continental Shelf
   ├── 6.2 Maritime Delimitation
   │   ├── Equidistance / Special Circumstances
   │   ├── Relevant Circumstances
   │   └── Proportionality
   ├── 6.3 High Seas
   │   └── Freedom of Navigation
   └── 6.4 Marine Environment
       └── Protection of Marine Environment
```

### Implementation Notes:

**Database Structure:**
```sql
-- Level indicates hierarchy depth
-- 0 = Major area (e.g., "Use of Force")
-- 1 = Doctrine (e.g., "Self-Defence")
-- 2 = Specific test (e.g., "Effective Control Test")

CREATE TABLE legal_topics (
  id VARCHAR(100) PRIMARY KEY,
  parent_id VARCHAR(100) REFERENCES legal_topics(id),
  name VARCHAR(200) NOT NULL,
  slug VARCHAR(200) NOT NULL UNIQUE,
  level INT NOT NULL DEFAULT 0,
  path VARCHAR(500), -- e.g., "/use-of-force/self-defence"
  display_order INT DEFAULT 0,
  ...
);
```

**Seed Data:**
Create `src/data/topics.json` with full hierarchy.

---

## 6. Citation Architecture Audit

### Current Design: ✅ MOSTLY SOUND

The strategy pattern approach (architecture.md lines 540-565) is **good**, but needs **simplification for MVP**.

### Required Metadata by Document Type

#### ICJ Judgment
**Required:**
- `fullName` (full case name)
- `court` ("ICJ")
- `year` (judgment year)
- `judgmentDate` (full date)
- `documentType` ("Judgment", "Order", "Advisory Opinion")

**Highly Recommended (for proper citations):**
- `officialCitation` (e.g., "ICJ Reports 1986, p. 14")
- `citationPageNumber` (starting page)

**Optional:**
- `shortName` (parties only, e.g., "Nicaragua v United States")
- `caseNumber` (ICJ internal number)
- `proceduralStage` ("Merits", "Preliminary Objections", etc.)

**For Pinpoint Citations:**
- `paragraphNumber` (the specific paragraph being cited)

#### ICJ Advisory Opinion
**Same as Judgment, but:**
- `documentType` = "Advisory Opinion"
- No `applicant` / `respondent` parties
- Different citation format

#### Other Document Types (Future)
Defer to post-MVP:
- ICC Judgments → Phase 10
- Arbitral Awards → Phase 10
- Treaties → Phase 11
- UN Resolutions → Phase 11

### Metadata Handling Strategy

```typescript
interface CaseMetadata {
  // Required for all cases
  id: string;
  fullName: string;
  court: string;
  year: number;
  judgmentDate: Date;
  documentType: 'Judgment' | 'Order' | 'Advisory Opinion';
  officialUrl: string;
  
  // Highly recommended (for citations)
  officialCitation?: string;  // "ICJ Reports 1986, p. 14"
  citationPageNumber?: number; // 14
  
  // Optional (improves citation quality)
  shortName?: string;
  applicant?: string;
  respondent?: string;
  caseNumber?: string;
  proceduralStage?: string;
}

interface ValidationResult {
  isValid: boolean;
  canGenerateCitation: boolean;
  errors: string[];    // Missing REQUIRED fields
  warnings: string[];  // Missing OPTIONAL but recommended fields
}
```

### Fallback Strategy

**If `officialCitation` is missing:**
- OSCOLA: Generate `[Case Name], [Court], [Date]`
- Bluebook: Generate `[Short Name], [Court] ([Date])`
- Add warning: "⚠️ Official citation not available. Using simplified format."

**If `paragraphNumber` is not provided for pinpoint:**
- Return error: "Cannot generate pinpoint citation without paragraph number"

**If `shortName` is missing (Bluebook needs it):**
- Auto-generate from `fullName`: Extract party names
- Or fallback to full name

---

## 7. Technology Stack Audit

### Recommended Definitive Stack for MVP

| Component | Technology | Version | Justification |
|-----------|-----------|---------|---------------|
| **Framework** | Next.js | 14.2+ | Latest stable, App Router mature |
| **Language** | TypeScript | 5.3+ | Type safety, excellent tooling |
| **Styling** | Tailwind CSS | 3.4+ | Utility-first, fast development |
| **UI Components** | shadcn/ui | Latest | Accessible, customizable |
| **Icons** | Lucide React | Latest | Professional, comprehensive |
| **Database** | PostgreSQL | 15+ | Proven, powerful full-text search |
| **ORM** | Prisma | 5.x | Best TypeScript integration |
| **Database Host** | Supabase | N/A | Managed PostgreSQL + future auth |
| **App Hosting** | Vercel | N/A | Zero-config Next.js deployment |
| **Version Control** | GitHub | N/A | Industry standard |

### Rationale for Each Choice

**Next.js 14:**
- ✅ Server Components = better performance
- ✅ App Router = modern, powerful routing
- ✅ Server Actions = clean data mutations
- ✅ Static generation for public pages
- ✅ Excellent Vercel integration
- ✅ Large community, great documentation

**TypeScript:**
- ✅ Catch errors at compile time
- ✅ Excellent IDE support
- ✅ Self-documenting code
- ✅ Prisma auto-generates types
- ✅ Industry standard for serious projects

**Prisma:**
- ✅ Type-safe database queries
- ✅ Automatic migrations
- ✅ Schema-first approach
- ✅ Prisma Studio (database GUI)
- ✅ Excellent documentation
- ❌ Slight performance overhead (acceptable for MVP)

**PostgreSQL Full-Text Search:**
- ✅ Adequate for 1,000+ documents
- ✅ No external service needed
- ✅ Built-in to PostgreSQL
- ✅ `tsvector` + GIN indexes are fast
- ✅ Can migrate to Meilisearch later
- ❌ Not as sophisticated as dedicated search engine

**Supabase:**
- ✅ Managed PostgreSQL (no DevOps)
- ✅ Generous free tier
- ✅ Automatic backups
- ✅ Built-in authentication (for Phase 2)
- ✅ Connection pooling
- ✅ Direct SQL access

**Vercel:**
- ✅ Zero-config Next.js deployment
- ✅ Automatic HTTPS
- ✅ Global CDN
- ✅ GitHub integration
- ✅ Preview deployments
- ✅ Generous free tier

### Unnecessary Dependencies to AVOID

❌ **Redux/Zustand** — Not needed with Server Components  
❌ **React Query** — Not needed with Server Components  
❌ **Axios** — Use native `fetch` with Next.js  
❌ **Lodash** — Use native JavaScript  
❌ **Moment.js** — Use native `Date` or `date-fns` if needed  
❌ **Elasticsearch** — Too complex for MVP  
❌ **Docker** — Not needed for MVP (Vercel handles deployment)

---

## 8. Legal Source Verification System

### Recommended Verification Procedure

#### Step 1: Metadata Verification Checklist

For each case, create a `verification-record.json`:

```json
{
  "caseId": "icj-1986-nicaragua",
  "verificationDate": "2026-11-15",
  "verifiedBy": "Your Name",
  "verificationLevel": "full",
  "sources": {
    "primary": "https://www.icj-cij.org/case/70",
    "pdfUrl": "https://www.icj-cij.org/public/files/case-related/70/070-19860627-JUD-01-00-EN.pdf",
    "alternativeSources": []
  },
  "metadataChecks": {
    "fullNameVerified": true,
    "fullNameSource": "ICJ case list page",
    "partiesVerified": true,
    "dateVerified": true,
    "officialCitationVerified": true,
    "officialCitationSource": "ICJ Reports 1986, p. 14",
    "caseNumberVerified": true,
    "caseNumber": "70"
  },
  "paragraphVerification": {
    "method": "manual_extraction_from_pdf",
    "paragraphsVerified": [115, 176, 188, 190, 194, 195, 200, 211, 228, 292],
    "pageNumbers": {
      "115": 65,
      "195": 103
    },
    "extractionNotes": "All paragraphs copied from official PDF. Paragraph numbering verified. No tables or special formatting in selected paragraphs."
  },
  "citationVerification": {
    "oscolaVerified": true,
    "oscolaReference": "OSCOLA 4th ed., section 2.1.1",
    "bluebookVerified": true,
    "bluebookReference": "Bluebook 21st ed., Rule 21.5",
    "testCitations": [
      {
        "style": "oscola",
        "generated": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195",
        "verified": true
      }
    ]
  },
  "issues": [],
  "nextReviewDate": "2027-11-15"
}
```

#### Step 2: Database Fields for Verification

Ensure these fields exist in the `cases` table:

```sql
-- Verification tracking
source_verified BOOLEAN DEFAULT false,
source_verified_date DATE,
source_verification_level VARCHAR(50), -- 'full', 'metadata_only', 'pending'
source_notes TEXT,
verification_record JSONB, -- Store full verification record
```

#### Step 3: Verification Levels

**Level 1: Metadata Only** (Basic)
- Case name verified
- Court verified
- Date verified
- Official URL confirmed

**Level 2: Standard** (Recommended for MVP)
- All metadata verified
- 10+ paragraphs extracted and verified
- OSCOLA citation tested
- Bluebook citation tested

**Level 3: Full** (Gold standard)
- All metadata verified against multiple sources
- All paragraphs in database verified
- Both citations tested and validated
- Independent verification by second person
- PDF archived locally (if permitted)

#### Step 4: Verification Status UI

Display verification status on case pages:

```tsx
<VerificationBadge status={case.sourceVerified}>
  {case.sourceVerified ? (
    <>
      ✅ Verified against official source
      <small>Last verified: {case.sourceVerifiedDate}</small>
    </>
  ) : (
    <>
      ⚠️ Pending verification
    </>
  )}
</VerificationBadge>
```

---

## 9. First Development Milestone: "Self-Defence Search Prototype"

### Clear Definition

**Milestone Name:** Self-Defence Search Prototype  
**Goal:** Prove the core research workflow with one complete example  
**Timeline:** Weeks 1-10 (Phases 0-5)

### Exact Scope

**Cases:**
1. **Nicaragua v United States (1986)** — Judgment on Merits

**Paragraphs (10 key paragraphs):**
- Para 115: Effective control test for attribution
- Para 176: Armed attack vs mere frontier incident
- Para 188: Necessity and proportionality in self-defence
- Para 191: Collective self-defence requirements
- Para 194: Right of self-defence under customary law
- Para 195: Requirements for exercise of self-defence
- Para 200: Reporting to Security Council
- Para 211: Prohibition of intervention
- Para 228: Humanitarian intervention not justified
- Para 292: Dispositif (judgment summary)

**Legal Topics (4 topics):**
1. Use of Force → Self-Defence (Article 51)
2. Use of Force → Non-Intervention
3. State Responsibility → Attribution of Conduct → Effective Control Test
4. Use of Force → Collective Self-Defence

**Features:**
- Search functionality (keyword + topic filter)
- Case detail page
- Document reader with paragraphs
- Copy paragraph button
- OSCOLA citation generator
- Bluebook citation generator
- Copy paragraph + citation

### User Story

```
As a law student preparing for a moot court competition,
I need to research the legal requirements for self-defence under Article 51,
So that I can cite authoritative ICJ jurisprudence in my memorial.

Scenario 1: Keyword Search
- I open MootMood homepage
- I search for "self-defence" in the search bar
- I see Nicaragua v United States case in results
- I click on the case
- I see the case metadata and paragraphs
- I jump to paragraph 195
- I read the paragraph about self-defence requirements
- I click "Copy Paragraph + Citation (OSCOLA)"
- I paste into my Word document
- The citation is correctly formatted

Scenario 2: Topic Browse
- I open MootMood homepage
- I click "Browse Legal Topics"
- I expand "Use of Force"
- I click "Self-Defence (Article 51)"
- I see Nicaragua v United States case listed
- I follow the same workflow as Scenario 1

Scenario 3: Specific Paragraph
- I know I need Nicaragua case, paragraph 115 (effective control)
- I open case page
- I type "115" in "Jump to paragraph" input
- Page scrolls to paragraph 115
- I read the paragraph about attribution
- I copy paragraph + Bluebook citation
- Citation correctly shows "¶ 115"
```

### Acceptance Criteria (Detailed)

#### 1. Homepage
- [ ] Page loads in < 2 seconds
- [ ] Search bar is prominent and functional
- [ ] "Browse Legal Topics" section exists
- [ ] Nicaragua case appears in "Recent Cases" (since it's the only case)
- [ ] SEO metadata present (title, description)

#### 2. Search Functionality
- [ ] Search "self-defence" returns Nicaragua case
- [ ] Search "nicaragua" returns Nicaragua case
- [ ] Search "effective control" returns Nicaragua case (paragraph match)
- [ ] Search "attribution" returns Nicaragua case
- [ ] No search returns "No results found" message
- [ ] Search results show case name, court, date, excerpt

#### 3. Topic Browse
- [ ] Legal topics page displays hierarchical taxonomy
- [ ] "Use of Force" → "Self-Defence (Article 51)" is clickable
- [ ] Clicking shows Nicaragua case tagged with this topic
- [ ] Topic page shows case count (1 case)

#### 4. Case Detail Page
- [ ] Loads in < 2 seconds
- [ ] Displays full case metadata:
  - Full case name (exact official name)
  - Court: ICJ
  - Date: 27 June 1986
  - Parties: Nicaragua v United States of America
  - Document type: Judgment
  - Official citation: ICJ Reports 1986, p. 14
  - Official URL (linked): https://www.icj-cij.org/case/70
- [ ] Displays verification badge: "✅ Verified against official source"
- [ ] Shows 4 topic tags
- [ ] "View Official Source" button works

#### 5. Document Reader
- [ ] Displays all 10 paragraphs with numbers
- [ ] Paragraph numbers appear in left gutter
- [ ] Paragraphs are selectable (text selection works)
- [ ] Each paragraph has "Copy Paragraph" button
- [ ] "Jump to Paragraph" input exists
- [ ] Entering "195" and pressing Enter scrolls to paragraph 195
- [ ] URL updates to include anchor: `/cases/icj-1986-nicaragua#para-195`
- [ ] Direct URL with anchor works (sharable links)

#### 6. Copy Paragraph
- [ ] Click "Copy Paragraph" button on paragraph 195
- [ ] Visual feedback appears (toast or checkmark)
- [ ] Paste into Word → paragraph text appears
- [ ] Paste into notepad → paragraph text appears (no HTML)
- [ ] Paragraph preserves formatting (no weird characters)

#### 7. Citation Generator - OSCOLA
- [ ] Citation style selector shows "OSCOLA" and "Bluebook"
- [ ] Select "OSCOLA"
- [ ] Citation preview displays:
  ```
  Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14
  ```
- [ ] Click "Copy Citation"
- [ ] Paste into Word → citation appears correctly formatted
- [ ] Select paragraph 195
- [ ] Click "Copy Citation (Pinpoint)"
- [ ] Citation includes:
  ```
  Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195
  ```
- [ ] Manually compare against OSCOLA 4th ed. guide → format is correct

#### 8. Citation Generator - Bluebook
- [ ] Select "Bluebook" style
- [ ] Citation preview displays:
  ```
  Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14, ¶ 195 (June 27)
  ```
- [ ] Click "Copy Citation"
- [ ] Paste into Word → citation formatted correctly
- [ ] Manually compare against Bluebook 21st ed. Rule 21.5 → format is correct

#### 9. Copy Paragraph + Citation
- [ ] Select paragraph 195
- [ ] Select OSCOLA style
- [ ] Click "Copy Paragraph + Citation"
- [ ] Paste into Word → both appear:
  ```
  [Paragraph text]
  
  Citation: Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195.
  ```
- [ ] Formatting is clean (no weird line breaks)
- [ ] Ready to use in a memorial

#### 10. Data Verification
- [ ] All metadata verified against https://www.icj-cij.org/case/70
- [ ] All 10 paragraphs verified against official PDF
- [ ] Paragraph numbers confirmed correct
- [ ] No fabricated content
- [ ] Verification record documented in database

#### 11. Performance
- [ ] Homepage loads in < 2 seconds
- [ ] Search results appear in < 2 seconds
- [ ] Case page loads in < 2 seconds
- [ ] Paragraph scrolling is smooth
- [ ] No JavaScript errors in console
- [ ] Works on Chrome, Firefox, Safari

#### 12. Deployment
- [ ] Deployed to Vercel
- [ ] HTTPS working
- [ ] Database connected to Supabase
- [ ] Public URL accessible
- [ ] No errors in Vercel logs

### Success Definition

**This milestone is complete when:**
A user can search for "self-defence", find Nicaragua, read paragraph 195, and copy it with a correct OSCOLA citation — all verified against official sources.

---

## 10. GitHub and Project Management Recommendations

### Repository Organization

```
mootmood/
├── .github/
│   └── workflows/          # CI/CD (future)
├── .kiro/
│   └── steering/           # ✅ Already created
├── docs/                   # New: Archive planning docs here
│   ├── planning/
│   │   ├── requirements.md
│   │   ├── architecture.md
│   │   ├── database-schema.md
│   │   └── development-roadmap.md
│   └── verification/       # New: Verification records
│       └── icj-1986-nicaragua.json
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   └── seed.ts
├── public/
├── src/
│   ├── app/
│   ├── components/
│   ├── lib/
│   ├── types/
│   └── data/               # Seed data (verified cases)
│       ├── cases/
│       │   └── icj-1986-nicaragua.json
│       ├── topics.json
│       └── courts.json
├── tests/
├── .env.example            # ✅ Template provided above
├── .gitignore              # ✅ Template provided above
├── README.md
├── package.json
└── tsconfig.json
```

### Git Workflow

**Branch Strategy:**
- `main` — production-ready code only
- `develop` — integration branch (optional for MVP)
- `feature/search` — feature branches
- `fix/citation-formatting` — bug fixes

**Commit Guidelines:**
```
feat: add OSCOLA citation formatter
fix: correct paragraph number display
docs: update citation verification procedure
test: add citation formatter tests
chore: update dependencies
```

### Project Management

**GitHub Issues:**
Create issues for each phase:
- `#1 Phase 1: Core Infrastructure`
- `#2 Phase 2: Homepage & Browse`
- etc.

**Milestones:**
- `MVP - Phase 0` ✅ Complete
- `MVP - Phase 1-5` (Development)
- `MVP - Phase 6` (Dataset)
- `MVP - Phase 7-8` (Launch)

**Labels:**
- `priority: critical` (blocking issues)
- `priority: high`
- `priority: medium`
- `type: bug`
- `type: feature`
- `type: documentation`
- `phase: 1` (etc.)

---

## 11. Problems Summary

### Critical Problems (Must Fix Before Implementation)
1. ⚠️ **MVP Scope Confusion** — Research Workspace marked as MVP but is Phase 9
2. ⚠️ **First Milestone Undefined** — No clear prototype definition
3. ⚠️ **Source Verification Undefined** — No procedure for "verified" data

### High Priority Problems (Should Fix)
4. ⚠️ **Legal Taxonomy Incomplete** — Missing key topics (Effective Control, Overall Control, Jus Cogens)
5. ⚠️ **Citation Metadata Incomplete** — Unclear fallback handling
6. ⚠️ **Initial Dataset Too Large** — 15-20 cases unrealistic for MVP timeline

### Medium Priority Problems (Can Address During Development)
7. ⚠️ **Database Design Overcomplicated** — Citation templates table not needed for MVP
8. ⚠️ **Search Ranking Unrealistic** — Custom weighting difficult in PostgreSQL
9. ⚠️ **Timeline Optimistic** — 17 weeks assumes everything goes perfectly
10. ⚠️ **Technology "Options"** — Presents alternatives instead of decisions
11. ⚠️ **PostgreSQL Config Underspecified** — No multilingual or synonym plan
12. ⚠️ **Environment Setup Missing** — No `.gitignore` or `.env.example` in docs

---

## 12. Recommended Corrections

### Immediate Actions (Before Implementation)

1. **Update requirements.md:**
   - Move "Feature 5: Research Workspace" to "Post-MVP Features" section
   - Mark all save functionality as "(Phase 9)"
   - Clarify MVP is copy-to-clipboard only

2. **Create legal-topic-taxonomy.md:**
   - Document complete 3-level hierarchy
   - Include all topics from Section 5 of this audit
   - Create `src/data/topics.json` seed file

3. **Create first-milestone.md:**
   - Copy "Section 9" of this audit
   - Add to project documentation
   - Use as Phase 1-5 completion criteria

4. **Create source-verification-procedure.md:**
   - Copy "Section 8" of this audit
   - Add verification record template
   - Define verification levels

5. **Simplify architecture.md:**
   - Remove "Option A vs Option B" sections
   - Make definitive technology choices
   - Remove citation templates table from MVP

6. **Create `.gitignore` and `.env.example`:**
   - Use templates from Section 12 of this audit

7. **Revise development-roadmap.md:**
   - Update Phase 6: "5 cases instead of 15-20"
   - Update timeline: "14-16 weeks realistic"
   - Add First Milestone as Phase 0-5 deliverable

8. **Create citation-metadata-requirements.md:**
   - Document required vs optional fields
   - Define fallback strategies
   - Include validation logic

### Phase 1 Actions (During Implementation)

9. **Implement simplified citation architecture:**
   - Hard-code OSCOLA and Bluebook formatters
   - Skip citation templates table
   - Add comprehensive tests

10. **Use simple PostgreSQL search:**
    - `ts_rank()` + year sorting
    - No custom weighting
    - Add synonym expansion if time permits

11. **Document data extraction process:**
    - Create verification records as you extract
    - Test citations against official guides
    - Keep verification records in Git

---

## 13. External Services & Accounts Required

### Absolutely Required for MVP

1. **GitHub Account**
   - Purpose: Version control, collaboration
   - Cost: Free for public repositories
   - Setup: github.com/signup
   - When: Before Phase 1

2. **Supabase Account**
   - Purpose: Managed PostgreSQL database
   - Cost: Free tier (500MB database, 2GB bandwidth)
   - Setup: supabase.com/signup
   - When: Phase 1 (database setup)
   - Note: Includes future authentication for Phase 9

3. **Vercel Account**
   - Purpose: Application hosting and deployment
   - Cost: Free tier (unlimited personal projects)
   - Setup: vercel.com/signup (use GitHub to sign in)
   - When: Phase 8 (deployment)
   - Note: Connect to GitHub repo for auto-deploy

### Optional (Not Required for MVP)

4. **Domain Name** (Optional)
   - Purpose: Custom domain (e.g., mootmood.com)
   - Cost: $10-15/year
   - Provider: Namecheap, Google Domains, Cloudflare
   - When: Before public launch (can use vercel.app subdomain for MVP)

5. **Google Analytics** (Optional)
   - Purpose: Usage tracking
   - Cost: Free
   - When: Phase 8 or later

6. **Sentry** (Optional)
   - Purpose: Error tracking
   - Cost: Free tier available
   - When: Post-MVP

### Not Required for MVP

- ❌ AWS account (Vercel handles hosting)
- ❌ Docker Hub (not using Docker for MVP)
- ❌ Elasticsearch (using PostgreSQL search)
- ❌ Stripe (no payments in MVP)
- ❌ SendGrid (no emails in MVP)

---

## 14. Final Recommendation

### Recommendation: ✅ **PROCEED TO IMPLEMENTATION**

**With the following conditions:**

1. **Complete the 8 immediate corrections** listed in Section 12 before writing application code
2. **Reduce MVP scope** by removing Research Workspace (already correctly in Phase 9, just fix documentation)
3. **Start with 5 cases** instead of 15-20 for the initial dataset
4. **Use the First Milestone definition** from Section 9 as your Phase 1-5 target
5. **Accept 14-16 week timeline** instead of 17 weeks (or keep 17 weeks with 5 cases)

### Why Proceed?

**Strengths:**
- ✅ Core product concept is sound and well-validated
- ✅ Technology stack is appropriate and proven
- ✅ Database schema is well-designed (with minor simplifications needed)
- ✅ Architecture principles are solid
- ✅ Legal accuracy requirements are properly documented
- ✅ Documentation is comprehensive and professional

**Weaknesses (All Addressable):**
- ⚠️ Scope needs clarification (easy fix)
- ⚠️ Legal taxonomy needs expansion (defined in this audit)
- ⚠️ Timeline needs adjustment (realistic expectation)
- ⚠️ First milestone needs definition (provided in this audit)

**Risk Assessment: LOW**

The identified issues are **documentation and planning refinements**, not fundamental architecture problems. With the corrections applied, this project has a **high probability of success**.

### What Makes This Different from Typical Student Projects

**Professional Characteristics:**
1. **Comprehensive planning** — Most student projects skip this entirely
2. **Legal domain expertise** — You understand the user needs deeply
3. **Source integrity focus** — Most projects would fake the data
4. **Structured development** — Phased approach with clear milestones
5. **Realistic scope** — MVP is focused and achievable

**This is not a toy project.** This is a genuine legal research tool being built with professional standards.

---

## 15. Next Steps

### Immediate Tasks (This Week)

1. **Review this audit report carefully**
2. **Make corrections to documentation:**
   - Update requirements.md (remove workspace from MVP)
   - Create legal-topic-taxonomy.md
   - Create first-milestone.md
   - Create source-verification-procedure.md
   - Simplify architecture.md (remove options)
3. **Create `.gitignore` and `.env.example` files**
4. **Approve revised scope and timeline**

### Phase 1 Start (Next Week)

5. **Initialize Git repository**
6. **Create Next.js project**
7. **Set up Supabase account and database**
8. **Initialize Prisma with schema**
9. **Begin UI component development**

### First Deliverable (Week 10)

10. **Complete First Milestone:**
    - Nicaragua case with 10 paragraphs
    - Search functionality
    - Citation generation
    - Verified data

---

## Conclusion

MootMood is **ready to proceed to implementation** after addressing the corrections outlined in this audit. The foundation is solid, the concept is validated, and with realistic scope adjustments, this will be a valuable legal research tool.

**The project planning is 85% excellent.** The 15% that needs correction consists mainly of scope clarification, taxonomy expansion, and setting realistic expectations — all of which are addressed in this audit report.

**Recommendation: Implement corrections and begin Phase 1 development.**

---

**End of Audit Report**

**Prepared by:** Kiro AI Development Partner  
**Date:** November 6, 2026  
**Document Version:** 1.0  
**Status:** READY FOR REVIEW

---

**MootMood — Search Smarter. Plead Stronger.**
