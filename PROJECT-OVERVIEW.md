# MootMood — Project Overview

**Product Name:** MootMood  
**Tagline:** Search Smarter. Plead Stronger.  
**Category:** International Law Legal Research & Moot Court Platform  
**Status:** Planning Complete — Ready for Development  
**Date:** November 6, 2026

---

## Quick Summary

MootMood is a professional legal research platform designed specifically for international law students and moot court participants. It solves the core challenge of efficiently discovering, organizing, and citing international legal authorities for moot court memorial preparation.

**Key Innovation:** Topic-based legal search with paragraph-level precision and automated citation generation in multiple formats.

---

## Core Features (MVP)

### 1. Advanced Legal Search
- Keyword search across cases, principles, and treaties
- Hierarchical legal topic classification
- Multi-dimensional filtering (court, year, topic, document type)
- Paragraph-level search results with excerpts

### 2. Legal Authority Reader
- Professional document viewer with paragraph navigation
- Jump to specific paragraphs
- Copy paragraphs with one click
- Comprehensive case metadata display
- Direct links to official sources

### 3. Citation Generator
- Automated citation generation (OSCOLA and Bluebook)
- Pinpoint paragraph citations
- Copy citation or paragraph + citation
- Validated against official citation guides
- Never fabricates missing information

### 4. International Law Sources Library
- ICJ judgments (5 verified cases for MVP)
- Advisory opinions
- Orders and arbitral awards
- Expandable to other tribunals (ICC, ICTY, ITLOS, etc.) in Phase 10+

### 5. Topic-Based Discovery
- Browse cases by legal concept rather than case name
- Hierarchical topic taxonomy covering:
  - Public International Law
  - Use of Force
  - International Humanitarian Law
  - International Criminal Law
  - Human Rights Law
  - Law of the Sea

---

## Technology Stack

### Frontend
- **Framework:** Next.js (App Router) — Use latest stable version
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS
- **UI Components:** shadcn/ui (Radix UI + Tailwind)
- **Icons:** Lucide React

### Backend
- **Runtime:** Node.js LTS — Use latest stable LTS version
- **API:** Next.js Server Actions & Route Handlers
- **Database:** PostgreSQL 15+
- **ORM:** Prisma
- **Search:** PostgreSQL Full-Text Search (MVP), Meilisearch (future)

**Note:** Version numbers like "Next.js 14+" or "Node.js 20+" referenced elsewhere were current at planning time (November 2026). Always use latest stable, supported versions at implementation time.

### Deployment
- **Hosting:** Vercel
- **Database:** Supabase (or Neon/Railway)
- **Version Control:** GitHub

---

## Architecture Highlights

### Design Principles
1. **Server-first:** React Server Components by default
2. **Type-safe:** Strict TypeScript throughout
3. **Simple:** Avoid unnecessary complexity
4. **Scalable:** Design for 1,000 to 10,000+ authorities
5. **Accurate:** Data integrity over feature quantity

### Database Design
- Relational PostgreSQL schema
- Entities: Courts, Cases, Paragraphs, LegalTopics, Citations
- Many-to-many relationships for topic tagging
- Full-text search with tsvector indexes
- Paragraph-level topic granularity

### Citation Engine
- Strategy pattern for multiple citation styles
- Deterministic template-based generation
- Comprehensive validation
- Never fabricates missing metadata
- Extensible for future citation styles

---

## Development Roadmap

### MVP Timeline: 14-16 Weeks (Indicative)

**Phase 0: Foundation (Weeks 1-2)** ✅ COMPLETE
- Requirements, architecture, database design
- Project steering files
- Development roadmap

**Phase 1: Core Infrastructure (Weeks 3-4)**
- Database implementation
- UI component library
- Layout components
- Utility functions

**Phase 2: Homepage & Browse (Weeks 5-6)**
- Homepage development
- Legal topics taxonomy
- Court directory
- Browse functionality

**Phase 3: Search Functionality (Weeks 7-8)**
- Search interface
- PostgreSQL full-text search
- Filters and facets
- Results display

**Phase 4: Case Detail Pages (Weeks 9-10)**
- Case detail layout
- Document reader
- Paragraph navigation
- Copy functionality

**Phase 5: Citation Generation (Weeks 11-12)**
- Citation engine
- OSCOLA formatter
- Bluebook formatter
- UI integration
- **Milestone 1 Complete:** 1-case prototype (Nicaragua v US)

**Phase 6: Initial Dataset (Week 13)**
- Expand from 1 to 5 verified ICJ cases
- 100-150 total paragraphs
- Topic tagging
- Database seeding

**Phase 7: Testing & Polish (Weeks 14-15)**
- Comprehensive testing
- UI/UX polish
- Performance optimization
- Documentation

**Phase 8: MVP Launch (Week 16)**
- Production deployment
- Monitoring
- Initial feedback
- **Milestone 2 Complete:** 5-case MVP

**Note:** Timeline is indicative based on reduced scope (5 cases instead of 15-20).

### Post-MVP Phases
- **Phase 9:** Research Workspace (user accounts, saved authorities, project organization) - 4 weeks
- **Phase 10:** Extended Dataset (expand to 15-20+ cases across multiple tribunals) - ongoing
- **Phase 11:** Treaties & Documents (6 weeks)
- **Phase 12:** Advanced Search (4 weeks)
- **Phase 13:** Citation Profiles (3 weeks)
- **Phase 14:** AI Features (8 weeks)

---

## Legal Research Accuracy Principles

### Critical Rules

1. **Official Sources First**
   - Prioritize official court websites
   - Always link to official sources
   - Verify against original documents

2. **Never Fabricate**
   - No invented case names, judgments, paragraphs, or citations
   - No AI-generated content presented as official legal text
   - Clear identification of missing or uncertain data

3. **Preserve Original Text**
   - Maintain exact wording of legal documents
   - Distinguish quotations from summaries
   - Never present editorial content as judicial reasoning

4. **Transparency**
   - Mark source verification status
   - Document verification dates
   - Distinguish primary from secondary sources

5. **Quality Over Quantity**
   - Start with 10-20 carefully verified cases
   - Each case must link to official source
   - No unreliable or unverified data

---

## UI/UX Design Standards

### Visual Identity
- **Primary Colors:** Dark navy (#1e3a5f), white, off-white background
- **Accent Colors:** Muted blue (#4a90e2), dark grey, light grey
- **Typography:** Inter (headings and body), monospace for citations
- **Style:** Professional, clean, information-dense without clutter

### Design Philosophy
- **Professional over flashy** — Look like a legal research tool
- **Accuracy over quantity** — Verified sources, not large unreliable databases
- **Structured over chaotic** — Organized taxonomy, not keyword chaos
- **Traceable over mysterious** — Always show source provenance

### Key Layouts

**Homepage:**
- Prominent search bar (hero element)
- Browse by legal topics (grid)
- Browse by courts (directory)
- Recent cases
- Platform description

**Search Results:**
- Two-column layout (filters sidebar + results)
- Result cards with metadata and excerpts
- Faceted navigation
- Sort and pagination

**Document Reader:**
- Sidebar (metadata + navigation) + main content
- Paragraph numbers in gutter
- Copy and citation actions
- Jump to paragraph

---

## Initial Dataset (MVP)

### Two-Milestone Strategy

**Milestone 1: 1-Case Prototype** (End of Phase 5)
- **Case:** Nicaragua v United States (1986)
- **Paragraphs:** 10 manually verified key paragraphs
- **Purpose:** Prove core concept and research workflow
- **Deliverables:** Working search, browse, document reader, citation generation

**Milestone 2: 5-Case MVP** (End of Phase 8)
- **Cases:** 5 verified landmark ICJ cases
- **Paragraphs:** 100-150 manually verified paragraphs (20-30 per case)
- **Purpose:** Functional research platform with topic diversity
- **Deliverables:** Complete MVP ready for user testing

### MVP Dataset: 5 Verified ICJ Cases

**Covering:**
- State Responsibility & Attribution (2 cases)
  - Nicaragua v United States
  - Bosnia v Serbia (Genocide Convention)

- Use of Force & Self-Defence (2 cases)
  - Nicaragua (also covers attribution)
  - Oil Platforms (Iran v United States)

- Jurisdiction & Immunities (1 case)
  - Arrest Warrant (DRC v Belgium)

**Requirements:**
- Complete verified metadata
- Official source links
- 20-30 key paragraphs per case
- Legal topic tagging (3-8 topics per case)
- 100-150 total paragraphs across all cases
- Source verification documentation

### Post-MVP Expansion (Phase 10)

After MVP proves the system works, expand to 15-20+ cases:
- Additional State Responsibility cases (DRC v Uganda)
- Maritime Law (North Sea Continental Shelf, Black Sea Delimitation)
- Human Rights & IHL cases (LaGrand, Pulp Mills)
- Advisory Opinions (Nuclear Weapons, Wall)
- Other tribunals (ICC, ICTY, ITLOS, etc.)

---

## Success Criteria (MVP)

### Functional Success
✅ User can search by legal topic and find relevant cases  
✅ User can filter results by court, year, and topic  
✅ User can view full case metadata and paragraphs  
✅ User can navigate to specific paragraphs  
✅ User can copy paragraphs with one click  
✅ User can generate OSCOLA and Bluebook citations  
✅ All citations link to verifiable official sources  

### Quality Success
✅ All case data verified against official sources  
✅ Zero fabricated legal authorities or paragraphs  
✅ All citations tested against manual reference examples  
✅ Professional UI matching legal research platforms  
✅ Search response < 2 seconds  
✅ No critical bugs in core workflows  

---

## Technical Risks & Mitigation

### Risk 1: Data Acquisition
**Risk:** Difficult to obtain full-text judgments legally  
**Mitigation:** Link to official sources, provide metadata and key paragraphs only

### Risk 2: Citation Complexity
**Risk:** Citation rules are complex and jurisdiction-specific  
**Mitigation:** Start with two well-documented styles, use validated templates, clearly mark limitations

### Risk 3: Search Relevance
**Risk:** Simple keyword search may not find topically relevant cases  
**Mitigation:** Manual legal topic tagging, synonym expansion, topic-based browsing, future Meilisearch migration

### Risk 4: Scope Creep
**Risk:** Feature requests expand beyond MVP  
**Mitigation:** Strict MVP scope, phased development, defer non-critical features

### Risk 5: Source Verification Burden
**Risk:** Manually verifying authorities is time-consuming  
**Mitigation:** Two-milestone approach — 1 case prototype (10 paragraphs), expand to 5 cases (100-150 paragraphs) for MVP, prioritize quality over quantity

---

## Documentation Structure

### Core Documents
1. **requirements.md** — Complete product requirements (features, user flows, success criteria)
2. **architecture.md** — Technical architecture (stack, components, patterns, deployment)
3. **database-schema.md** — Database design (entities, relationships, indexes, queries)
4. **development-roadmap.md** — Phased development plan (tasks, timeline, checkpoints)
5. **PROJECT-OVERVIEW.md** — This document (high-level summary)

### Steering Files (`.kiro/steering/`)
1. **mootmood-product-vision.md** — Product identity and core principles
2. **ui-ux-standards.md** — Design system and visual standards
3. **legal-research-accuracy.md** — Source integrity and accuracy rules
4. **technical-conventions.md** — Coding standards and conventions

---

## Project Directory Structure

```
mootmood/
├── .kiro/
│   └── steering/              # Project steering files
├── prisma/
│   ├── schema.prisma         # Database schema
│   ├── migrations/           # Migration files
│   └── seed.ts               # Seed script
├── public/                   # Static assets
├── src/
│   ├── app/                  # Next.js pages
│   │   ├── layout.tsx
│   │   ├── page.tsx         # Homepage
│   │   ├── search/          # Search results
│   │   ├── cases/[id]/      # Case detail
│   │   ├── topics/[slug]/   # Topic browse
│   │   └── courts/[slug]/   # Court browse
│   ├── components/
│   │   ├── ui/              # Base components
│   │   ├── layout/          # Layout components
│   │   ├── search/          # Search components
│   │   ├── legal/           # Legal document components
│   │   └── browse/          # Browse components
│   ├── lib/
│   │   ├── db/              # Database queries
│   │   ├── citation/        # Citation generation
│   │   └── search/          # Search logic
│   ├── types/               # TypeScript types
│   └── data/                # Seed data (JSON)
├── tests/                   # Test files
├── requirements.md
├── architecture.md
├── database-schema.md
├── development-roadmap.md
├── PROJECT-OVERVIEW.md
└── README.md
```

---

## Key Differentiators

### vs. General Search Engines
- Legal topic-based discovery (not just keywords)
- Paragraph-level precision
- Structured legal taxonomy
- Citation generation
- Moot court focus

### vs. Existing Legal Databases
- Free and accessible
- Moot court-specific features
- Simplified for students
- Topic-based organization
- Modern, clean interface

### vs. Jus Mundi (Inspiration)
- Focused on international law moot topics
- Simpler, more accessible for students
- Citation generation built-in
- Free to use (MVP)
- Academic research tool

---

## Target User Journey

1. **Student receives moot problem** with legal issues to research
2. **Opens MootMood** and searches "Non-intervention"
3. **Discovers relevant cases** tagged with intervention, coercion, sovereignty
4. **Filters by ICJ** and recent cases (post-2000)
5. **Opens Nicaragua v United States** case
6. **Jumps to paragraph 115** about effective control test
7. **Reads paragraph** about attribution of conduct
8. **Copies paragraph + OSCOLA citation** in one click
9. **Pastes into Word memorial** with perfect formatting
10. **Repeats for other issues** and builds legal argument

**Result:** Research time reduced by 50%+, citations are accurate, authorities are verified

---

## Next Steps

### Immediate Actions (Week 1)

1. **Review Planning Documents**
   - ✅ requirements.md
   - ✅ architecture.md
   - ✅ database-schema.md
   - ✅ development-roadmap.md
   - ✅ Documentation synchronized with approved MVP scope

2. **Initialize Project (Local Machine)**
   - Clone GitHub repository
   - Initialize Next.js project
   - Set up development environment
   - Create Supabase/database project

3. **Begin Phase 1**
   - Implement database schema
   - Set up UI component library
   - Create layout structure
   - Build utility functions

---

## Long-Term Vision

**6-Month Goal:**
- 5-case MVP deployed and tested
- Research Workspace implemented (Phase 9)
- Begin dataset expansion (Phase 10)
- 50+ active users
- Feedback from initial moot court participants

**12-Month Goal:**
- 15-20+ verified legal authorities
- 500+ paragraphs
- Multiple international tribunals
- Treaty database foundation
- 500+ active users
- Recognized by moot court community

**24-Month Goal:**
- 50+ legal authorities
- AI-powered case discovery
- Semantic legal search
- Competition-specific citation profiles
- Collaborative research features
- Mobile applications
- Partnership with moot court competitions

**Ultimate Vision:**
Build MootMood into the go-to legal research platform for international law mooters worldwide — making finding legal authorities, identifying relevant judicial paragraphs, and generating accurate citations substantially easier.

---

## Contact & Collaboration

**Repository:** https://github.com/Mootmood/mootmood  
**Status:** Planning Complete — Ready for Development  
**Contact:** Developer information to be added  

---

**MootMood — Search Smarter. Plead Stronger.**

---

**END OF PROJECT OVERVIEW**
