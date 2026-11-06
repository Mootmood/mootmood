# MootMood — Planning Phase Complete ✅

**Date:** November 6, 2026  
**Phase:** Foundation & Architecture Planning  
**Status:** COMPLETE — Ready for Review & Development

---

## 🎉 What Has Been Completed

I have successfully completed the comprehensive planning and architecture phase for MootMood. All foundational documents are ready for your review.

### ✅ Completed Deliverables

#### 1. **Product Requirements Document** (`requirements.md`)
- Complete feature specifications for MVP
- User personas and user flows
- Legal topic taxonomy (6 major categories, 80+ sub-topics)
- Two-milestone MVP strategy (1-case prototype → 5-case MVP)
- Initial dataset requirements (5 ICJ cases for MVP, expand to 15-20+ in Phase 10)
- Success criteria and metrics
- Non-functional requirements
- Risk analysis

#### 2. **Technical Architecture Document** (`architecture.md`)
- Complete technology stack with justifications
- Application architecture and component design
- Directory structure
- Search architecture (PostgreSQL full-text search)
- Citation generation architecture (strategy pattern)
- API design
- Security considerations
- Performance optimization strategies
- Testing strategy
- Deployment architecture (Vercel + Supabase)

#### 3. **Database Schema Design** (`database-schema.md`)
- Complete entity relationship design
- 8 core tables with full SQL and Prisma schemas:
  - Courts
  - Cases
  - Paragraphs
  - LegalTopics
  - CaseTopics (join table)
  - ParagraphTopics (join table)
  - CitationStyles
  - CitationTemplates
- 4 future tables for Phase 2 (user workspace)
- Full-text search setup
- Index strategy
- Data integrity constraints
- Seeding strategy
- Sample data structures

#### 4. **Development Roadmap** (`development-roadmap.md`)
- Complete 17-week MVP timeline broken into 8 phases
- Detailed task lists for each phase
- Review checkpoints between phases
- Post-MVP phases (9-14) with timelines
- Risk mitigation strategies
- Development guidelines and standards
- Testing requirements
- Success metrics

#### 5. **Project Overview** (`PROJECT-OVERVIEW.md`)
- High-level summary document
- Quick reference for all key information
- Technology stack overview
- Initial dataset details
- Key differentiators
- Target user journey
- Long-term vision

#### 6. **README** (`README.md`)
- Professional project README
- About section
- Features overview
- Technology stack
- Documentation index
- Getting started guide (template for future)
- Development roadmap summary
- Design philosophy
- Contribution guidelines

#### 7. **Kiro Steering Files** (`.kiro/steering/`)
- `mootmood-product-vision.md` — Product identity and principles
- `ui-ux-standards.md` — Complete design system (colors, typography, layouts, components)
- `legal-research-accuracy.md` — Source integrity rules (critical for legal platform)
- `technical-conventions.md` — Coding standards and conventions

---

## 📊 Project Scope Summary

### MVP Features
1. **Advanced Legal Search** — Keyword + topic + filters
2. **Legal Authority Reader** — Document viewer with paragraph navigation
3. **Citation Generator** — OSCOLA + Bluebook automated citations
4. **Topic-Based Discovery** — Hierarchical legal taxonomy

**Note:** Research Workspace (save functionality, user accounts) deferred to Phase 9 (POST-MVP)

### Technology Stack
- **Frontend:** Next.js (App Router) + TypeScript + Tailwind CSS + shadcn/ui
- **Backend:** Next.js Server Actions + PostgreSQL + Prisma
- **Deployment:** Vercel + Supabase
- **Search:** PostgreSQL Full-Text Search (MVP)

**Note:** Use latest stable versions of all technologies at implementation time.

### Timeline
- **MVP Development:** 14-16 weeks (indicative, based on 5-case scope)
- **Phase 0 (Planning):** ✅ Complete
- **Phases 1-8:** Development
- **Two Milestones:** 1-case prototype (Phase 5) → 5-case MVP (Phase 8)

### Initial Dataset
**Milestone 1: 1-Case Prototype**
- Nicaragua v United States (1986)
- 10 manually verified paragraphs

**Milestone 2: 5-Case MVP**
- 5 verified landmark ICJ cases
- 100-150 extracted paragraphs (20-30 per case)
- Complete verified metadata
- Official source links
- Legal topic tagging

---

## 📁 Document Structure

```
/projects/sandbox/
├── README.md                           # Project introduction
├── PROJECT-OVERVIEW.md                 # High-level summary (START HERE)
├── requirements.md                     # Complete product requirements
├── architecture.md                     # Technical architecture
├── database-schema.md                  # Database design
├── development-roadmap.md              # Development plan & tasks
├── PLANNING-COMPLETE.md               # This file (planning summary)
│
└── .kiro/steering/                    # Persistent project rules
    ├── mootmood-product-vision.md     # Product identity
    ├── ui-ux-standards.md             # Design system
    ├── legal-research-accuracy.md     # Source integrity rules
    └── technical-conventions.md       # Coding standards
```

---

## 🎯 Critical Design Decisions Made

### 1. **Accuracy Over Scale**
- Start with 10-20 carefully verified cases rather than large unreliable database
- Every case must link to official source
- Never fabricate legal content
- Clear verification status indicators

### 2. **Simple, Proven Technology**
- Next.js 14 with App Router (stable, modern)
- PostgreSQL (reliable, powerful)
- Prisma (type-safe, great DX)
- No unnecessary complexity

### 3. **Topic-Driven Discovery**
- Hierarchical legal taxonomy (6 major categories, 80+ topics)
- Paragraph-level topic tagging
- Browse by legal concept, not just keywords
- Manual curation for accuracy

### 4. **Citation Engine Architecture**
- Strategy pattern for extensibility
- Template-based generation
- Comprehensive validation
- Never fabricates missing metadata
- Tested against official citation guides

### 5. **Professional Design**
- Navy and white color scheme
- Inter typography
- Clean, organized, information-dense
- Desktop-first (research platform)
- Inspired by Jus Mundi, Westlaw, LexisNexis

### 6. **Phased Development**
- MVP focuses on core search + citation features
- User accounts deferred to Phase 2 (workspace)
- Advanced AI features deferred to Phase 14
- Each phase builds on stable foundation

---

## 🔍 Key Technical Highlights

### Database Design
- **8 core tables** with complete relationships
- **Full-text search** using PostgreSQL tsvector + GIN indexes
- **Many-to-many topic tagging** at case and paragraph level
- **Citation templates** stored in database for flexibility
- **Cascading deletes** for data integrity
- **Verification tracking** (source_verified, source_verified_date)

### Search Architecture
- **Phase 1:** PostgreSQL full-text search (adequate for 1000+ documents)
- **Phase 2:** Meilisearch migration path (abstracted interface)
- **Features:** Keyword search + topic filters + facets + pagination
- **Ranking:** Text relevance + title matches + recency + topic matches

### Citation System
- **Interface-based design** (CitationFormatter interface)
- **Two initial styles:** OSCOLA + Bluebook
- **Three format types:** Full, short, pinpoint
- **Validation system:** Required fields checked before generation
- **Template storage:** Database-driven for easy updates

### Component Architecture
- **Server Components by default** (performance)
- **Client Components only for interactivity** (copy buttons, filters)
- **Clear separation:** ui/ legal/ search/ browse/ layout/
- **Modular and reusable** throughout

---

## ⚠️ Critical Requirements Documented

### Legal Research Accuracy Rules

**NEVER:**
- Fabricate case names, judgments, paragraphs, or citations
- Present AI-generated content as official legal text
- Invent missing metadata
- Reproduce copyrighted material without authorization

**ALWAYS:**
- Link to official sources
- Preserve original legal text
- Mark verification status
- Distinguish primary from secondary sources
- Document source provenance

### UI/UX Standards

**Design System:**
- Primary: Navy #1e3a5f, White #ffffff
- Accents: Muted blue #4a90e2, Dark grey #2c3e50
- Typography: Inter (headings + body), Monospace (citations)
- Professional, clean, information-dense

**Key Layouts:**
- Homepage: Search hero + topic browse + court directory
- Search Results: Two-column (filters + results)
- Document Reader: Sidebar (metadata) + main (paragraphs)

### Technical Conventions

**Code Standards:**
- TypeScript strict mode
- No `any` types without justification
- PascalCase components, camelCase functions
- Error handling everywhere
- Environment variables for secrets

**Testing Requirements:**
- Citation formatters: 10+ test cases each
- Search: 20+ test queries
- Integration tests for critical paths
- Edge cases (missing data, special characters)

---

## 📈 Success Metrics Defined

### MVP Success Criteria

**Functional:**
✅ User can search by legal topic and find relevant cases  
✅ User can filter results by court, year, and topic  
✅ User can view full case metadata and paragraphs  
✅ User can navigate to specific paragraphs  
✅ User can copy paragraphs with one click  
✅ User can generate OSCOLA and Bluebook citations  
✅ All citations link to verifiable official sources  

**Quality:**
✅ All case data verified against official sources  
✅ Zero fabricated legal authorities or paragraphs  
✅ Professional UI matching legal research platforms  
✅ Search response < 2 seconds  
✅ No critical bugs in core workflows  

**Content:**
✅ 5 verified ICJ cases (MVP)  
✅ 100-150 extracted paragraphs  
✅ Complete legal topic taxonomy  

---

## 🚀 Next Steps — What Happens Now

### Immediate Next Steps (Week 1)

#### Step 1: Review Planning Documents ⏳
**Your Action Required:**
1. Read `PROJECT-OVERVIEW.md` (quick summary)
2. Review `requirements.md` (product requirements)
3. Review `architecture.md` (technical architecture)
4. Review `database-schema.md` (database design)
5. Review `development-roadmap.md` (development plan)

**Questions to Consider:**
- Are the MVP features correct?
- Is the technology stack appropriate?
- Is the 14-16 week timeline acceptable (indicative only)?
- Are there any missing requirements?
- Do you approve the design direction?

#### Step 2: Provide Feedback or Approval ✅
**If you approve:**
- I will proceed with project initialization
- Create Git repository
- Initialize Next.js project
- Set up development environment

**If you have feedback:**
- Provide your feedback/changes
- I will revise the relevant documents
- We'll review again before proceeding

#### Step 3: Begin Development 🚀
**Once approved, I will:**
1. Initialize Git repository
2. Create Next.js 14 project with TypeScript
3. Set up Tailwind CSS and shadcn/ui
4. Create project directory structure
5. Initialize Prisma and database
6. Create initial migration
7. Set up development environment
8. Begin Phase 1 tasks (Core Infrastructure)

---

## 💡 Recommendations for You

### Before Development Starts

1. **Set up accounts:**
   - GitHub account (if not already)
   - Supabase account (free tier) OR
   - Neon/Railway account for PostgreSQL

2. **Prepare development environment:**
   - Install Node.js 20+ LTS
   - Install a code editor (VS Code recommended)
   - Install Git

3. **Review legal topic taxonomy:**
   - Check the legal topics in `requirements.md`
   - Suggest any additions or modifications
   - Ensure terminology is accurate

4. **Identify initial cases:**
   - Review the suggested ICJ cases
   - Confirm these are appropriate for moot court research
   - Suggest any essential cases to include

### During Development

1. **Review at checkpoints:**
   - Each phase ends with a review checkpoint
   - I will present completed work
   - You approve or provide feedback before next phase

2. **Test features as built:**
   - Try the search functionality
   - Test citation generation
   - Verify case data accuracy
   - Provide UX feedback

3. **Provide legal expertise:**
   - Verify case metadata accuracy
   - Check citation formats
   - Validate legal topic assignments
   - Suggest improvements

---

## 📋 Pending Decisions

### Decisions You May Want to Make

1. **Project Name Confirmation:**
   - Are you 100% committed to "MootMood"?
   - Consider trademark/domain availability
   - Alternative names to consider?

2. **Database Provider:**
   - Supabase (recommended — includes auth for Phase 2)
   - Neon (PostgreSQL specialist)
   - Railway (simpler setup)
   - Local PostgreSQL (development only)

3. **Domain Name:**
   - Do you want to register a domain now?
   - Suggested: mootmood.com or mootmood.io
   - Can wait until closer to launch

4. **Citation Style Priority:**
   - OSCOLA and Bluebook confirmed for MVP
   - Are there other styles needed for launch?
   - Any competition-specific formats essential?

5. **Logo and Branding:**
   - Do you have a logo design in mind?
   - Should we use a placeholder initially?
   - Professional design or simple text logo?

---

## 🎓 What You Should Know

### About the Planning Process

I have created this comprehensive planning documentation to ensure:

1. **Clear requirements** — We know exactly what to build
2. **Technical foundation** — Architecture is sound and scalable
3. **Legal accuracy** — Source integrity rules are clear
4. **Professional design** — UI/UX standards are defined
5. **Realistic timeline** — 17 weeks with clear milestones
6. **Risk mitigation** — Identified risks and solutions

### About the Technology Choices

**Next.js 14:**
- Modern, fast, excellent developer experience
- Server Components for performance
- Built-in routing and API
- Great for SEO
- Easy deployment to Vercel

**PostgreSQL:**
- Reliable, mature, powerful
- Excellent full-text search
- Strong data integrity
- Free and open-source
- Industry standard

**Prisma:**
- Type-safe database queries
- Automatic migrations
- Great developer experience
- Matches TypeScript philosophy

**Tailwind CSS + shadcn/ui:**
- Modern, professional styling
- Highly customizable
- Accessible components
- Fast development

### About the Development Approach

**Why phased development?**
- Each phase builds on stable foundation
- Review checkpoints prevent scope creep
- Easier to test and validate
- Clear progress milestones
- Can adjust based on feedback

**Two-Milestone Approach:**
- **Milestone 1:** 1 case (Nicaragua v US), 10 paragraphs — Proves core concept
- **MVP (Milestone 2):** 5 cases, 100-150 paragraphs — Functional research platform
- **Phase 10:** Expand to 15-20+ cases with more legal topics
- Test citation accuracy
- Ensure UI/UX is right
- Easier to expand than to fix bad data

**Why MVP before advanced features?**
- Core functionality must work perfectly
- Build trust with accurate, verified data
- User accounts add complexity
- AI features need careful implementation
- Can launch sooner with focused scope

---

## ✅ Planning Phase Checklist

- [x] Product requirements documented
- [x] Technical architecture designed
- [x] Database schema defined
- [x] Development roadmap created
- [x] Project overview written
- [x] README created
- [x] Steering files established
- [x] UI/UX standards documented
- [x] Legal accuracy rules defined
- [x] Technical conventions set
- [x] Risk analysis completed
- [x] Success criteria defined
- [x] Initial dataset specified
- [x] Timeline estimated

**Status:** ALL PLANNING COMPLETE ✅

---

## 📞 Ready for Your Review

I have completed the comprehensive planning phase for MootMood. All documentation is ready for your review.

### What I Need From You

1. **Review the documents** (start with `PROJECT-OVERVIEW.md`)
2. **Provide feedback or approval**
3. **Answer any pending decisions** (database provider, etc.)
4. **Confirm you're ready to begin development**

### What Happens Next

Once you approve:
1. I initialize the project
2. Set up the development environment
3. Begin Phase 1 (Core Infrastructure)
4. Build the foundational components
5. Present Phase 1 results for review
6. Continue through the MVP phases

---

## 💬 Questions for You

Before we proceed, please consider:

1. **Do you approve the overall product requirements and MVP scope?**

2. **Is the technology stack (Next.js + PostgreSQL + Prisma) acceptable?**

3. **Is the 17-week MVP timeline reasonable for your goals?**

4. **Do you have any concerns about the legal accuracy requirements?**

5. **Are you ready to set up the required accounts (GitHub, Supabase)?**

6. **Do you want to make any changes before we begin development?**

---

## 🎯 Final Note

This comprehensive planning ensures we build MootMood correctly from the start. The foundation is solid, the requirements are clear, and the technical approach is sound.

**MootMood will be a professional, accurate, and valuable legal research tool for international law students and mooters worldwide.**

I'm ready to begin development as soon as you approve the plan.

---

**Status:** Planning Complete ✅ | Awaiting Your Review 📋 | Ready to Build 🚀

---

**MootMood — Search Smarter. Plead Stronger.**
