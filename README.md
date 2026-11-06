# MootMood — International Law Legal Research Platform

**Search Smarter. Plead Stronger.**

MootMood is a professional legal research platform designed specifically for international law students, moot court participants, legal researchers, and practitioners. It makes finding legal authorities, identifying relevant judicial paragraphs, and generating accurate citations substantially easier.

---

## 🎯 Project Status

**Current Phase:** Planning Complete — Ready for Development  
**Date:** November 6, 2026  
**MVP Target:** 14-16 weeks (indicative, based on 5-case scope)

---

## 📋 Table of Contents

- [About MootMood](#about-mootmood)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Project Documentation](#project-documentation)
- [Getting Started](#getting-started)
- [Development Roadmap](#development-roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## 🌟 About MootMood

MootMood solves the core challenge that international law mooters face: efficiently discovering, organizing, and citing international legal authorities for moot court memorial preparation.

### The Problem

International law mooters struggle to:
1. Find relevant international court judgments and decisions
2. Identify authoritative legal sources supporting specific legal propositions
3. Locate specific paragraphs within lengthy judgments
4. Discover cases through legal topics rather than case names alone
5. Extract relevant legal passages efficiently
6. Generate accurate citations according to different citation styles
7. Organize legal authorities for memorials and legal arguments

### The Solution

**MootMood provides:**
- **Topic-based legal search** — Discover cases by legal concept, not just keywords
- **Paragraph-level precision** — Navigate directly to relevant reasoning
- **Automated citation generation** — OSCOLA and Bluebook citation formats
- **Verified sources** — All authorities linked to official court sources
- **Efficient research workflow** — Copy paragraphs and citations with one click

---

## ✨ Key Features

### 1. Advanced Legal Search Engine
- Keyword search across cases, legal principles, and treaty provisions
- Hierarchical legal topic classification (Public International Law, Use of Force, IHL, ICL, Human Rights, Law of the Sea)
- Multi-dimensional filtering (court, year, document type, legal topic)
- Paragraph-level search results with excerpts
- Faceted search navigation

### 2. Legal Authority Reader
- Professional document viewer with paragraph navigation
- Jump to specific paragraphs instantly
- Copy paragraphs with one click
- Comprehensive case metadata display
- Direct links to official sources
- Within-document search

### 3. Citation Generator
- Automated citation generation (OSCOLA and Bluebook for MVP)
- Pinpoint paragraph citations
- Copy citation or paragraph + citation together
- Validated against official citation guides
- Never fabricates missing information
- Word-compatible formatting

### 4. International Law Sources Library
- ICJ judgments, orders, and advisory opinions
- Future: ICC, ICTY, ICTR, ITLOS, PCA, ECtHR, IACtHR
- Future: Treaties, UN resolutions, ILC materials
- All sources verified against official publications

### 5. Topic-Based Discovery
- Browse cases by legal concept rather than case name
- Hierarchical topic taxonomy
- Paragraph-level topic tagging
- Discover related authorities

---

## 🛠 Technology Stack

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
- **Search:** PostgreSQL Full-Text Search (MVP), Meilisearch (planned)

**Note:** Version numbers like "Next.js 14+" or "Node.js 20+" referenced throughout documentation were current at planning time (November 2026). Always use latest stable, supported versions at implementation time.

### Deployment
- **Hosting:** Vercel
- **Database:** Supabase (or Neon/Railway)
- **Version Control:** GitHub

---

## 📚 Project Documentation

This repository contains comprehensive planning and technical documentation:

### Core Documents
1. **[requirements.md](requirements.md)** — Complete product requirements, features, user flows, and success criteria
2. **[architecture.md](architecture.md)** — Technical architecture, stack decisions, patterns, and deployment strategy
3. **[database-schema.md](database-schema.md)** — Database design with entities, relationships, indexes, and queries
4. **[development-roadmap.md](development-roadmap.md)** — Phased development plan with tasks, timeline, and checkpoints
5. **[PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md)** — High-level project summary and quick reference

### Steering Files (`.kiro/steering/`)
1. **mootmood-product-vision.md** — Product identity and core principles
2. **ui-ux-standards.md** — Design system and visual standards
3. **legal-research-accuracy.md** — Source integrity and accuracy rules
4. **technical-conventions.md** — Coding standards and conventions

**Start with:** `PROJECT-OVERVIEW.md` for a quick introduction, then review `requirements.md` and `architecture.md` for details.

---

## 🚀 Getting Started

### Prerequisites

- Node.js LTS (latest stable version)
- PostgreSQL 15+ (or Supabase account)
- Git
- A code editor (VS Code recommended)

**Note:** Specific version requirements (e.g., "Node.js 20+") will be determined at implementation time based on dependency compatibility.

### Installation (Coming Soon)

Once development begins, installation steps will be:

```bash
# 1. Clone the repository
git clone https://github.com/Mootmood/mootmood.git
cd mootmood

# 2. Install dependencies
npm install

# 3. Set up environment variables
cp .env.example .env.local
# Edit .env.local with your database credentials

# 4. Set up the database
npx prisma migrate dev
npx prisma db seed

# 5. Start the development server
npm run dev

# 6. Open http://localhost:3000
```

### Development Commands

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm start            # Start production server
npm test             # Run tests
npm run lint         # Run linter
npx prisma studio    # Open Prisma Studio (database GUI)
npx prisma migrate dev  # Create database migration
```

---

## 🗺 Development Roadmap

### MVP Timeline: 14-16 Weeks (Indicative)

| Phase | Description | Duration | Status |
|-------|-------------|----------|--------|
| **Phase 0** | Foundation & Setup | 2 weeks | ✅ Planning Complete |
| **Phase 1** | Core Infrastructure | 2 weeks | 🔲 Not Started |
| **Phase 2** | Homepage & Browse | 2 weeks | 🔲 Not Started |
| **Phase 3** | Search Functionality | 2 weeks | 🔲 Not Started |
| **Phase 4** | Case Detail Pages | 2 weeks | 🔲 Not Started |
| **Phase 5** | Citation Generation | 2-3 weeks | 🔲 Not Started |
| **Phase 6** | Initial Dataset (5 cases) | 1 week | 🔲 Not Started |
| **Phase 7** | Testing & Polish | 2 weeks | 🔲 Not Started |
| **Phase 8** | MVP Launch | 1 week | 🔲 Not Started |

**Note:** Timeline is indicative based on 5-case MVP scope. First milestone (1-case prototype) completed by end of Phase 5.

### Post-MVP Phases

- **Phase 9:** Research Workspace (user accounts, saved authorities, project organization)
- **Phase 10:** Extended Dataset (expand to 15-20+ cases across multiple tribunals)
- **Phase 11:** Treaties & Documents (treaty database, article citations)
- **Phase 12:** Advanced Search (Meilisearch, semantic search, synonyms)
- **Phase 13:** Citation Profiles (competition-specific citation rules)
- **Phase 14:** AI Features (case similarity, recommendations, concept extraction)

See [development-roadmap.md](development-roadmap.md) for complete task breakdown.

---

## 🎨 Design Philosophy

### Visual Identity
- **Professional over flashy** — Look like a legal research tool, not a consumer app
- **Clean and organized** — Information-dense without clutter
- **Navy and white** — Professional color palette (#1e3a5f primary)
- **Inter typography** — Modern, readable, professional
- **Desktop-first** — Optimized for research on larger screens

### User Experience
- **Search-focused** — Prominent search bar as hero element
- **Topic-driven** — Browse by legal concept, not just case names
- **Paragraph-precise** — Direct access to relevant reasoning
- **One-click actions** — Copy paragraphs and citations easily
- **Source transparent** — Always link to official sources

---

## 📊 Development Strategy & Dataset

### Two-Milestone Approach

**Milestone 1: 1-Case Prototype** (Weeks 1-10)
- **Goal:** Prove core concept with one complete, verified case
- **Case:** Nicaragua v United States (1986)
- **Paragraphs:** 10 manually verified paragraphs
- **Features:** Search, browse, document reader, citations (OSCOLA + Bluebook)
- **Verification:** Every paragraph checked against official ICJ source

**Milestone 2: 5-Case MVP** (Weeks 11-16)
- **Goal:** Functional research platform with diverse legal topics
- **Cases:** 5 verified landmark ICJ cases
- **Paragraphs:** 100-150 manually verified paragraphs (20-30 per case)
- **Coverage:** Multiple legal topics across international law
- **Requirements:** Complete metadata, official source links, topic tagging

### MVP Dataset: 5 Verified ICJ Cases

**Topics to be covered:**
- State Responsibility & Attribution (Nicaragua v US, Bosnia v Serbia)
- Use of Force & Self-Defence (Nicaragua, Oil Platforms)
- Jurisdiction & Immunities (Arrest Warrant)
- Other key international law principles

**Quality Requirements:**
- Complete verified metadata for each case
- 20-30 key paragraphs per case (100-150 total)
- Official source links for all authorities
- Legal topic tagging (3-8 topics per case)
- Source verification documentation

### Post-MVP Expansion (Phase 10)

Expand dataset to 15-20+ cases after MVP proves the system works:
- Additional ICJ cases covering more legal topics
- Multiple international tribunals (ICC, ICTY, ITLOS, etc.)
- Advisory opinions and arbitral awards
- 500+ verified paragraphs total

---

## 🔐 Legal Research Accuracy Principles

MootMood is an academic legal research platform. **Accuracy takes priority over quantity.**

### Core Rules

1. **Official Sources First** — Prioritize official court websites, always link to sources
2. **Never Fabricate** — No invented cases, judgments, paragraphs, or citations
3. **Preserve Original Text** — Maintain exact wording of legal documents
4. **Transparency** — Mark verification status and missing data clearly
5. **Quality Over Quantity** — Two-milestone approach:
   - First milestone: 1 carefully verified case (Nicaragua v US), 10 paragraphs
   - MVP: 5 verified ICJ cases, 100-150 paragraphs
   - Post-MVP: Expand to 15-20+ cases in Phase 10

See [.kiro/steering/legal-research-accuracy.md](.kiro/steering/legal-research-accuracy.md) for complete guidelines.

---

## 🤝 Contributing

This project is currently in the planning and initial development phase. Contributions will be welcome once the MVP is established.

### Planned Contribution Areas
- Case data verification and extraction
- Legal topic taxonomy expansion
- Citation format implementations
- UI/UX improvements
- Bug reports and feature suggestions

---

## 📝 License

**Status:** License to be determined  

**Options under consideration:**
- **MIT License:** Permissive, allows commercial use, widely adopted
- **Apache 2.0:** Permissive with patent protection
- **GPL v3:** Copyleft, requires derivatives to be open source
- **AGPL v3:** Strong copyleft, includes network use provision

**Considerations:**
- **Data licensing:** Legal case data from official sources (public domain)
- **Code licensing:** Application code and logic
- **Citation templates:** Based on published citation guides
- **Commercial use:** Whether to allow/restrict commercial derivatives

**Decision pending:** License will be chosen after consultation with legal advisors and community feedback.

---

## 👥 Team

**Status:** Developer and contact information to be added  
**Project Type:** Open source international law research platform  

---

## 🌐 Links

- **Repository:** https://github.com/Mootmood/mootmood
- **Documentation:** See files in this repository
- **Project Board:** [Coming soon]
- **Issues:** [Coming soon]
- **Website:** [Coming soon after deployment]

---

## 🙏 Acknowledgments

**Inspiration:**
- Jus Mundi (legal research platform)
- Westlaw and LexisNexis (professional legal databases)
- International Court of Justice (primary source of case law)

**Built for:**
- International law mooters worldwide
- Students preparing for Philip C. Jessup Competition
- ICC Moot Court Competition participants
- Legal researchers and academics

---

## 📧 Contact

**Status:** Contact information to be added  
**Repository:** https://github.com/Mootmood/mootmood  
**Issues:** Use GitHub Issues for bug reports and feature requests  

---

## 🎯 Project Vision

**Mission:** Make international law research substantially easier for moot court participants and students.

**Long-term goal:** Become the go-to legal research platform for international law mooters worldwide.

**Values:**
- **Accuracy** — Legal research integrity above all
- **Accessibility** — Free and easy to use
- **Quality** — Verified sources and accurate citations
- **Student-focused** — Built for mooters, by someone who understands the challenge

---

**MootMood — Search Smarter. Plead Stronger.**

*A legal research platform that understands what mooters need.*

---

**Status:** Planning Complete ✅ | Ready for Development 🚀 | MVP: 5 Cases, 14-16 Weeks (Indicative) ⏱️
