# MootMood — Development Roadmap & Task List

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Planning Phase

---

## Development Strategy

This roadmap outlines the phased development approach for MootMood, starting with a focused MVP and expanding in structured phases. Each phase builds on the previous one, ensuring a stable foundation before adding complexity.

### Guiding Principles

1. **Quality over speed:** Verify data accuracy at every step
2. **Build incrementally:** Complete one feature fully before starting the next
3. **Test continuously:** Test each component as it's built
4. **Document thoroughly:** Explain decisions and implementation details
5. **Review checkpoints:** Present completed phases for review before proceeding

---

## Phase 0: Foundation & Setup (CURRENT PHASE)

**Status:** ✅ IN PROGRESS  
**Duration:** 1-2 weeks  
**Goal:** Establish project requirements, architecture, and development environment

### Tasks

#### ✅ Planning Documents (COMPLETE)
- [x] Product requirements document
- [x] Technical architecture document
- [x] Database schema design
- [x] Development roadmap
- [x] Kiro steering files (UI/UX, legal accuracy, technical conventions, product vision)

#### 🔲 Project Initialization
- [ ] Initialize Git repository
- [ ] Create Next.js 14 project with TypeScript
- [ ] Configure Tailwind CSS
- [ ] Set up shadcn/ui components
- [ ] Configure ESLint and Prettier
- [ ] Set up project directory structure
- [ ] Create `.env.example` file
- [ ] Write README.md with setup instructions

#### 🔲 Database Setup
- [ ] Create Supabase project (or local PostgreSQL)
- [ ] Initialize Prisma
- [ ] Create Prisma schema file
- [ ] Configure database connection
- [ ] Run initial migration
- [ ] Test database connection

#### 🔲 Development Environment
- [ ] Verify Node.js 20+ installed
- [ ] Install dependencies
- [ ] Configure VS Code (or preferred IDE)
- [ ] Set up Git hooks (Husky)
- [ ] Configure path aliases (@/ for src/)
- [ ] Test development server startup

**Deliverables:**
- ✅ Complete planning documentation
- Working Next.js development environment
- Database connected and schema created
- README with setup instructions

**Review Checkpoint:** Present project structure and verify setup before proceeding

---

## Phase 1: Core Infrastructure (Weeks 3-4)

**Duration:** 2 weeks  
**Goal:** Build foundation: layout, navigation, UI components, database schema

### Tasks

#### Database Implementation
- [ ] Implement complete Prisma schema
- [ ] Create migration files
- [ ] Add PostgreSQL full-text search extensions
- [ ] Create database indexes
- [ ] Write seed data structure (JSON templates)
- [ ] Implement database seeding script
- [ ] Test database queries

#### UI Component Library
- [ ] Install and configure shadcn/ui
- [ ] Create base components:
  - Button
  - Input
  - Card
  - Badge
  - Dropdown
  - Checkbox
  - Dialog/Modal
- [ ] Create custom theme configuration
- [ ] Apply MootMood color palette
- [ ] Configure typography (Inter font)
- [ ] Test component library

#### Layout Components
- [ ] Create root layout (`app/layout.tsx`)
- [ ] Build Header component with navigation
- [ ] Build Footer component
- [ ] Create responsive navigation menu
- [ ] Add MootMood logo (create or placeholder)
- [ ] Implement sticky header
- [ ] Test responsive behavior

#### Utility Functions
- [ ] Create date formatting utilities
- [ ] Create text truncation utilities
- [ ] Create URL slug generators
- [ ] Create type definitions (`src/types/`)
- [ ] Set up constants file
- [ ] Write utility tests

**Deliverables:**
- Complete database schema with migrations
- UI component library ready to use
- Basic layout structure working
- Utility functions tested

**Review Checkpoint:** Verify database structure and UI components before building pages

---

## Phase 2: Homepage & Browse Pages (Weeks 5-6)

**Duration:** 2 weeks  
**Goal:** Build homepage, topic browsing, and court directory

### Tasks

#### Homepage Development
- [ ] Design homepage layout
- [ ] Create hero section with search bar (UI only for now)
- [ ] Build "Browse by Topic" section
- [ ] Build "Browse by Court" section
- [ ] Add platform description section
- [ ] Create "Recent Cases" section (fetch from DB)
- [ ] Implement responsive design
- [ ] Add SEO metadata
- [ ] Test homepage rendering

#### Legal Topics System
- [ ] Create legal topics taxonomy (JSON)
- [ ] Seed topics into database
- [ ] Build TopicTree component (expandable hierarchy)
- [ ] Create topic detail page (`app/topics/[slug]/page.tsx`)
- [ ] Implement topic breadcrumb navigation
- [ ] Display cases by topic
- [ ] Add topic descriptions
- [ ] Test topic navigation

#### Court Directory
- [ ] Create courts data (JSON with ICJ, ICC, ITLOS, etc.)
- [ ] Seed courts into database
- [ ] Build CourtList component
- [ ] Create court detail page (`app/courts/[slug]/page.tsx`)
- [ ] Display court metadata and description
- [ ] List cases by court
- [ ] Add court logos/icons (optional)
- [ ] Test court browsing

#### Database Queries
- [ ] Write query: Get all top-level topics
- [ ] Write query: Get topic with children
- [ ] Write query: Get cases by topic
- [ ] Write query: Get cases by court
- [ ] Write query: Get recent cases
- [ ] Test query performance
- [ ] Add query result pagination

**Deliverables:**
- Fully functional homepage
- Topic browsing with hierarchy
- Court directory with cases
- Database queries optimized

**Review Checkpoint:** Verify browse functionality before implementing search

---

## Phase 3: Search Functionality (Weeks 7-8)

**Duration:** 2 weeks  
**Goal:** Implement search with filters and results display

### Tasks

#### Search Interface
- [ ] Create SearchBar component (with state)
- [ ] Build search results page (`app/search/page.tsx`)
- [ ] Implement URL query parameters for search
- [ ] Create SearchFilters sidebar component
- [ ] Build filter controls:
  - Topic filter (checkboxes)
  - Court filter (checkboxes)
  - Year range filter
  - Document type filter
- [ ] Add active filter chips (dismissible)
- [ ] Implement "Clear all filters" button
- [ ] Test filter interactions

#### PostgreSQL Full-Text Search
- [ ] Set up tsvector columns
- [ ] Create full-text search triggers
- [ ] Write search query builder function
- [ ] Implement keyword search
- [ ] Add topic filtering to search
- [ ] Add court filtering to search
- [ ] Add year filtering to search
- [ ] Implement relevance ranking
- [ ] Test search accuracy

#### Search Results Display
- [ ] Create ResultCard component
- [ ] Display case metadata in cards
- [ ] Show matched paragraph excerpts
- [ ] Highlight search terms in excerpts
- [ ] Add topic tags to results
- [ ] Implement result sorting (relevance, date, court)
- [ ] Add pagination controls
- [ ] Show result count
- [ ] Test results rendering

#### Search Facets
- [ ] Calculate filter counts (facets)
- [ ] Display counts next to filter options
- [ ] Update counts when filters change
- [ ] Test facet accuracy

**Deliverables:**
- Working search with keyword matching
- Comprehensive filtering system
- Search results with excerpts
- Faceted search navigation

**Review Checkpoint:** Verify search accuracy and performance before building case pages

---

## Phase 4: Case Detail Pages (Weeks 9-10)

**Duration:** 2 weeks  
**Goal:** Build document reader with paragraph navigation and metadata display

### Tasks

#### Case Detail Page
- [ ] Create case detail route (`app/cases/[id]/page.tsx`)
- [ ] Fetch case data with paragraphs
- [ ] Build page layout (sidebar + main content)
- [ ] Implement static params generation (SSG)
- [ ] Add SEO metadata for cases
- [ ] Test case page rendering

#### Case Metadata Display
- [ ] Create CaseMetadata component
- [ ] Display all case information:
  - Full name
  - Court and date
  - Parties
  - Document type
  - Official citation
  - Official URL (linked)
- [ ] Add "View Official Source" button
- [ ] Display legal topic tags
- [ ] Show verification status
- [ ] Test metadata display

#### Document Reader
- [ ] Create DocumentReader component
- [ ] Display paragraphs with numbers
- [ ] Style paragraph numbers (left gutter)
- [ ] Implement paragraph anchors (#para-115)
- [ ] Add "Jump to Paragraph" input
- [ ] Create paragraph navigation
- [ ] Implement scroll-to-paragraph
- [ ] Add sticky case title header
- [ ] Test reader functionality

#### Paragraph Actions
- [ ] Create ParagraphViewer component (Client Component)
- [ ] Add "Copy Paragraph" button per paragraph
- [ ] Implement copy to clipboard functionality
- [ ] Add visual feedback on copy (toast/checkmark)
- [ ] Style paragraph hover state
- [ ] Test paragraph copying

#### Within-Document Search
- [ ] Add search input in sidebar
- [ ] Implement browser find (Ctrl+F) enhancement
- [ ] Highlight matched terms
- [ ] Navigate between matches
- [ ] Test within-document search

**Deliverables:**
- Complete case detail pages
- Document reader with paragraph navigation
- Copy paragraph functionality
- Case metadata display

**Review Checkpoint:** Verify document reader UX before implementing citations

---

## Phase 5: Citation Generation (Weeks 11-12)

**Duration:** 2 weeks  
**Goal:** Build citation engine with OSCOLA and Bluebook formatters

### Tasks

#### Citation Engine Architecture
- [ ] Design CitationFormatter interface
- [ ] Create CitationGenerator class
- [ ] Implement validation system
- [ ] Create citation type definitions
- [ ] Set up citation test framework
- [ ] Write test cases with reference examples

#### OSCOLA Formatter
- [ ] Implement OSCOLA format rules
- [ ] Create full citation formatter
- [ ] Create short citation formatter
- [ ] Create pinpoint paragraph formatter
- [ ] Handle ICJ judgments
- [ ] Handle orders and advisory opinions
- [ ] Handle missing metadata gracefully
- [ ] Write OSCOLA tests (10+ test cases)
- [ ] Verify against official OSCOLA guide

#### Bluebook Formatter
- [ ] Implement Bluebook format rules
- [ ] Create full citation formatter
- [ ] Create short citation formatter
- [ ] Create pinpoint paragraph formatter
- [ ] Handle ICJ judgments
- [ ] Handle party name abbreviations
- [ ] Handle date formatting
- [ ] Write Bluebook tests (10+ test cases)
- [ ] Verify against Bluebook manual

#### Citation UI Integration
- [ ] Create CitationGenerator component
- [ ] Add citation style selector dropdown
- [ ] Display generated citation preview
- [ ] Add "Copy Citation" button
- [ ] Implement "Copy Paragraph + Citation" button
- [ ] Format output for Word compatibility
- [ ] Add citation warnings display
- [ ] Test citation copying workflow

#### Citation Templates (Database)
- [ ] Seed citation styles table
- [ ] Create citation templates for ICJ (OSCOLA)
- [ ] Create citation templates for ICJ (Bluebook)
- [ ] Store format rules in database
- [ ] Test template retrieval

**Deliverables:**
- Working citation engine
- OSCOLA formatter (tested)
- Bluebook formatter (tested)
- Citation UI integrated into case pages
- Copy citation functionality

**Review Checkpoint:** Verify citation accuracy against manual examples

---

## Phase 6: Initial Dataset (Weeks 13-14)

**Duration:** 2 weeks  
**Goal:** Create verified dataset of 10-20 ICJ cases with metadata and paragraphs

### Tasks

#### Case Selection
- [ ] Select 15-20 landmark ICJ cases
- [ ] Prioritize cases for moot topics:
  - State responsibility & attribution (3-4 cases)
  - Use of force & self-defence (3-4 cases)
  - Jurisdiction & immunities (2-3 cases)
  - Maritime law (2-3 cases)
  - Humanitarian law & human rights (2-3 cases)
- [ ] Verify case availability on ICJ website

#### Data Collection & Verification
For each case:
- [ ] Visit official ICJ case page
- [ ] Record full case name (exact)
- [ ] Record short name
- [ ] Record parties (applicant/respondent)
- [ ] Record judgment date
- [ ] Record official citation (ICJ Reports)
- [ ] Record case number
- [ ] Copy official URL
- [ ] Verify PDF availability
- [ ] Note any access restrictions

#### Paragraph Extraction
For each case (minimum 20 key paragraphs per case):
- [ ] Identify operative paragraphs
- [ ] Identify key legal reasoning paragraphs
- [ ] Extract paragraph numbers
- [ ] Extract paragraph text (exact wording)
- [ ] Note page numbers
- [ ] Identify relevant legal topics
- [ ] Create paragraph JSON records

#### Topic Tagging
- [ ] Assign 3-8 topics per case
- [ ] Tag paragraphs with specific topics
- [ ] Ensure balanced topic distribution
- [ ] Mark primary topics for each case

#### Data Format & Validation
- [ ] Create JSON files for each case
- [ ] Validate JSON structure
- [ ] Check for required fields
- [ ] Verify no fabricated content
- [ ] Document sources and verification dates
- [ ] Create data validation script

#### Database Seeding
- [ ] Update seed script with case data
- [ ] Run database seed
- [ ] Verify data integrity
- [ ] Test search functionality with real data
- [ ] Test citations with real cases
- [ ] Check for any errors or inconsistencies

**Deliverables:**
- 15-20 verified ICJ cases
- Minimum 300 extracted paragraphs
- Complete metadata for all cases
- All cases seeded into database
- Verification documentation

**Review Checkpoint:** Verify data accuracy and citation outputs

---

## Phase 7: Testing, Polish & Documentation (Weeks 15-16)

**Duration:** 2 weeks  
**Goal:** Comprehensive testing, UI polish, performance optimization, documentation

### Tasks

#### Testing
- [ ] Write unit tests for citation formatters
- [ ] Write unit tests for search query builder
- [ ] Write unit tests for utility functions
- [ ] Write integration tests for search workflow
- [ ] Write integration tests for citation workflow
- [ ] Test all user flows manually:
  - Homepage → Browse topics → View case
  - Homepage → Search → Filter → View case
  - Case page → Copy paragraph → Copy citation
  - Browse courts → View court cases
- [ ] Test responsive design (desktop, tablet, mobile)
- [ ] Test accessibility (keyboard navigation, screen readers)
- [ ] Fix all identified bugs

#### UI/UX Polish
- [ ] Review all page layouts
- [ ] Ensure consistent spacing
- [ ] Verify color palette usage
- [ ] Check typography consistency
- [ ] Add loading states (skeletons)
- [ ] Add empty states with helpful messages
- [ ] Add error states with recovery options
- [ ] Improve hover states and interactions
- [ ] Add micro-interactions (subtle animations)
- [ ] Polish citation display formatting

#### Performance Optimization
- [ ] Run Lighthouse audit
- [ ] Optimize images (if any)
- [ ] Check bundle size
- [ ] Optimize database queries
- [ ] Add database query indexes if needed
- [ ] Test search response time (< 2 seconds)
- [ ] Test page load time (< 3 seconds)
- [ ] Implement caching strategy
- [ ] Test with 1000+ search queries

#### Documentation
- [ ] Write comprehensive README
- [ ] Document setup instructions
- [ ] Document database schema
- [ ] Document API routes (if any)
- [ ] Create developer guide
- [ ] Document citation format rules
- [ ] Create user guide (how to use MootMood)
- [ ] Document known limitations
- [ ] Create troubleshooting guide
- [ ] Add inline code comments where needed

#### Deployment Preparation
- [ ] Set up Vercel project
- [ ] Configure environment variables in Vercel
- [ ] Set up Supabase production database
- [ ] Run production migration
- [ ] Seed production database
- [ ] Configure custom domain (if ready)
- [ ] Set up SSL certificate
- [ ] Test production deployment
- [ ] Monitor for errors

**Deliverables:**
- Comprehensive test coverage
- Polished UI/UX
- Optimized performance
- Complete documentation
- Production deployment ready

**Final Review Checkpoint:** Complete walkthrough before launch

---

## Phase 8: MVP Launch (Week 17)

**Duration:** 1 week  
**Goal:** Deploy MVP and monitor initial usage

### Tasks

#### Pre-Launch
- [ ] Final end-to-end testing
- [ ] Verify all links work
- [ ] Check all official source URLs
- [ ] Review all content for accuracy
- [ ] Verify citation outputs one final time
- [ ] Create backup of database
- [ ] Prepare rollback plan

#### Launch
- [ ] Deploy to production
- [ ] Verify production site works
- [ ] Test from multiple devices
- [ ] Share with initial test users
- [ ] Monitor error logs
- [ ] Monitor performance metrics

#### Post-Launch
- [ ] Gather initial feedback
- [ ] Fix any critical bugs
- [ ] Monitor search queries
- [ ] Track usage patterns
- [ ] Create feedback collection mechanism
- [ ] Plan Phase 2 features based on feedback

**Deliverables:**
- Live MVP at production URL
- Monitoring dashboard
- Initial user feedback
- Bug fix plan

---

## Future Phases (Post-MVP)

### Phase 9: Research Workspace (Weeks 18-21)
**Duration:** 4 weeks

**Features:**
- User authentication (Supabase Auth)
- User accounts and profiles
- Research project creation
- Save cases and paragraphs
- Organize by issue/argument
- Personal notes and annotations
- Export research (Word/PDF)

**Tasks:**
- [ ] Implement Supabase authentication
- [ ] Create user registration/login
- [ ] Build user dashboard
- [ ] Implement saved authorities
- [ ] Build research project interface
- [ ] Create export functionality
- [ ] Test workspace features

---

### Phase 10: Extended Dataset (Ongoing)
**Duration:** Ongoing

**Goals:**
- Expand to 50+ ICJ cases
- Add ICTY/ICTR cases (20+)
- Add ICC cases (15+)
- Add ITLOS cases (10+)
- Add PCA arbitral awards (10+)
- Add ECtHR cases (10+)

**Process:**
- Systematic case selection
- Verification against official sources
- Paragraph extraction
- Topic tagging
- Database updates
- Citation testing

---

### Phase 11: Treaties & Documents (Weeks 22-27)
**Duration:** 6 weeks

**Features:**
- Treaty database
- Article-level citations
- UN resolutions
- ILC materials
- Treaty search and browse

**Tasks:**
- [ ] Design treaty schema
- [ ] Collect treaty texts
- [ ] Implement treaty search
- [ ] Create treaty citation formats
- [ ] Build treaty viewer
- [ ] Test treaty integration

---

### Phase 12: Advanced Search (Weeks 28-31)
**Duration:** 4 weeks

**Features:**
- Meilisearch integration
- Better relevance ranking
- Typo tolerance
- Synonym expansion
- Search suggestions
- Advanced query syntax

**Tasks:**
- [ ] Set up Meilisearch instance
- [ ] Implement search adapter
- [ ] Migrate search logic
- [ ] Test search quality
- [ ] Add suggestions
- [ ] Performance tuning

---

### Phase 13: Citation Profiles (Weeks 32-34)
**Duration:** 3 weeks

**Features:**
- Competition-specific profiles
- Custom citation rules
- Citation validation
- Bulk citation export
- Memorial templates

**Tasks:**
- [ ] Research competition rules
- [ ] Implement profile system
- [ ] Create Jessup profile
- [ ] Create ICC Moot profile
- [ ] Build profile editor
- [ ] Test custom citations

---

### Phase 14: AI Features (Weeks 35-42)
**Duration:** 8 weeks

**Features:**
- Semantic search
- Case similarity
- Authority recommendations
- Legal concept extraction
- Argument structuring

**Requirements:**
- Must not fabricate authorities
- Must cite sources accurately
- Must indicate AI-generated content
- Must allow verification

**Tasks:**
- [ ] Research AI legal tech ethics
- [ ] Design AI architecture
- [ ] Implement embeddings
- [ ] Build recommendation engine
- [ ] Test accuracy rigorously
- [ ] Add transparency features

---

## Risk Mitigation Strategies

### Risk 1: Data Accuracy Issues
**Mitigation:**
- Manual verification process
- Source documentation
- Multiple review passes
- User feedback mechanism
- Regular audits

### Risk 2: Citation Complexity
**Mitigation:**
- Start with simple formats
- Extensive testing
- Clear limitation documentation
- User-reported corrections
- Gradual complexity increase

### Risk 3: Search Quality
**Mitigation:**
- Topic-based browsing as alternative
- Manual curation of key cases
- Search query logging and analysis
- Iterative improvement
- Future Meilisearch migration

### Risk 4: Performance at Scale
**Mitigation:**
- Database indexing
- Query optimization
- Caching strategy
- Connection pooling
- Monitoring and profiling

### Risk 5: Scope Creep
**Mitigation:**
- Strict MVP definition
- Feature prioritization
- Phase-based development
- Regular review checkpoints
- Defer non-critical features

---

## Development Guidelines

### Code Review Checklist
- [ ] Follows TypeScript strict mode
- [ ] No `any` types without justification
- [ ] Proper error handling
- [ ] Meaningful variable names
- [ ] Components are modular and reusable
- [ ] No hardcoded values (use constants)
- [ ] Environment variables for secrets
- [ ] Accessibility considerations
- [ ] Responsive design
- [ ] Tests written for complex logic

### Testing Standards
- [ ] Citation formatters: 10+ test cases each
- [ ] Search: 20+ test queries
- [ ] Edge cases covered (missing data, special characters)
- [ ] Integration tests for critical paths
- [ ] Manual testing of all UX flows

### Documentation Standards
- [ ] Every function has JSDoc comment
- [ ] Complex logic is explained
- [ ] API endpoints documented
- [ ] Database schema documented
- [ ] User-facing features explained in README

---

## Success Metrics

### MVP Success Criteria

**Functional:**
- ✅ User can search by keyword
- ✅ User can browse by legal topic
- ✅ User can filter by court and year
- ✅ User can view case detail pages
- ✅ User can navigate to specific paragraphs
- ✅ User can copy paragraphs with one click
- ✅ User can generate OSCOLA citations
- ✅ User can generate Bluebook citations
- ✅ All citations verified against manual examples

**Quality:**
- ✅ 100% of cases verified against official sources
- ✅ Zero fabricated legal content
- ✅ All citation outputs tested
- ✅ Professional UI matching design standards
- ✅ Search response < 2 seconds
- ✅ Page load < 3 seconds
- ✅ Zero critical bugs

**Content:**
- ✅ 15-20 verified ICJ cases
- ✅ 300+ extracted paragraphs
- ✅ Complete legal topic taxonomy
- ✅ 8+ courts in directory

### Phase 2 Success Criteria (Workspace)
- User authentication working
- Can save 100+ authorities
- Can organize by research project
- Can export to Word format
- 50+ active users

### Long-Term Success Criteria (12 months)
- 100+ verified legal authorities
- 2000+ paragraphs
- 500+ active users
- 90%+ user satisfaction
- Recognized by moot court community

---

## Development Tools & Resources

### Required Tools
- Node.js 20+
- PostgreSQL 15+ (via Supabase)
- Git
- VS Code (or preferred IDE)
- Vercel CLI (optional)

### Helpful Resources
- Next.js documentation
- Prisma documentation
- Tailwind CSS documentation
- shadcn/ui components
- OSCOLA citation guide (4th ed)
- Bluebook citation manual (21st ed)
- ICJ website (case source)

---

## Estimated Timeline Summary

| Phase | Description | Duration | Weeks |
|-------|-------------|----------|-------|
| 0 | Foundation & Setup | 2 weeks | 1-2 |
| 1 | Core Infrastructure | 2 weeks | 3-4 |
| 2 | Homepage & Browse | 2 weeks | 5-6 |
| 3 | Search Functionality | 2 weeks | 7-8 |
| 4 | Case Detail Pages | 2 weeks | 9-10 |
| 5 | Citation Generation | 2 weeks | 11-12 |
| 6 | Initial Dataset | 2 weeks | 13-14 |
| 7 | Testing & Polish | 2 weeks | 15-16 |
| 8 | MVP Launch | 1 week | 17 |
| **Total MVP** | | **17 weeks** | |

**Post-MVP phases:** 25+ additional weeks for Phases 9-14

---

## Next Immediate Steps

### To Start Phase 0 (Project Initialization):

1. **Review and Approve Planning Documents**
   - Review requirements.md
   - Review architecture.md
   - Review database-schema.md
   - Review this roadmap
   - Provide feedback or approval

2. **Initialize Project**
   - Create Git repository
   - Initialize Next.js project
   - Set up development environment
   - Create Supabase project

3. **Begin Development**
   - Start Phase 1 tasks
   - Set up database
   - Build UI components
   - Create layout structure

**Awaiting your review and approval to proceed with project initialization.**

---

**END OF DEVELOPMENT ROADMAP**
