# MootMood — Product Requirements Document

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Planning Phase

---

## Executive Summary

MootMood is a professional international law legal research platform designed specifically for moot court participants, international law students, legal researchers, and practitioners. The platform addresses the core challenge of efficiently discovering, organizing, and citing international legal authorities for moot court memorial preparation and legal research.

**Core Value Proposition:** Transform legal research from time-consuming keyword hunting into structured topic-based discovery with paragraph-level precision and automated citation generation.

---

## Product Goals

### Primary Goals
1. Enable rapid discovery of relevant international law authorities by legal topic
2. Provide paragraph-level access to judicial reasoning within judgments
3. Generate accurate citations in multiple citation styles (OSCOLA, Bluebook, custom)
4. Maintain absolute source integrity and accuracy
5. Create a professional, trustworthy research tool

### Success Metrics (Future)
- Time to find relevant authority reduced by 50%+
- Citation accuracy approaching 100%
- User satisfaction among moot court participants
- Regular usage during memorial preparation periods

---

## Target Users

### Primary Users
1. **Moot Court Participants** (Priority 1)
   - Preparing written memorials
   - Researching legal arguments
   - Need accurate citations
   - Time-constrained research

2. **International Law Students**
   - Academic research
   - Essay writing
   - Learning international law

3. **Legal Researchers & Academics**
   - In-depth research
   - Teaching materials
   - Publications

### User Needs Analysis

**Moot Court Participant Workflow:**
1. Identify legal issue from competition problem
2. Search for relevant authorities
3. Read judgments to find supporting paragraphs
4. Extract quotations with pinpoint citations
5. Organize authorities by memorial issue
6. Generate properly formatted citations
7. Draft memorial with cited authorities

**Pain Points Addressed:**
- ❌ Current: Search case databases by name only
- ✅ MootMood: Search by legal topic and principle

- ❌ Current: Read entire 100+ page judgments
- ✅ MootMood: Navigate directly to relevant paragraphs

- ❌ Current: Manually format citations from templates
- ✅ MootMood: Auto-generate citations from metadata

- ❌ Current: Copying and pasting from PDFs is error-prone
- ✅ MootMood: One-click copy with perfect formatting

---

## Core Features — MVP Scope

### Feature 1: Advanced Legal Search Engine

**Priority:** CRITICAL

#### 1.1 Search Interface
- Prominent search bar on homepage
- Keyword search across:
  - Case names
  - Legal principles
  - Treaty provisions
  - Legal terminology
  - Paragraph text
  - Court names

**Example searches:**
- "Nicaragua v United States"
- "Article 51 UN Charter"
- "Effective Control Test"
- "Prohibition of Intervention"
- "Necessity and Proportionality"

#### 1.2 Legal Topic Classification

Hierarchical browsable taxonomy with initial categories:

**PUBLIC INTERNATIONAL LAW**
- Sources of International Law
- Statehood and Recognition
- Jurisdiction
- Immunities
- State Responsibility
- Attribution
- Non-Intervention
- Sovereignty
- Diplomatic Protection
- International Dispute Settlement

**USE OF FORCE**
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

**INTERNATIONAL HUMANITARIAN LAW**
- Classification of Armed Conflicts
- International Armed Conflict
- Non-International Armed Conflict
- Distinction
- Proportionality
- Military Necessity
- Precautions in Attack
- Direct Participation in Hostilities
- Occupation
- Protection of Civilians

**INTERNATIONAL CRIMINAL LAW**
- Individual Criminal Responsibility
- Modes of Liability
- Command Responsibility
- Joint Criminal Enterprise
- Incitement
- Genocide
- Crimes Against Humanity
- War Crimes
- Crime of Aggression

**INTERNATIONAL HUMAN RIGHTS LAW**
- Right to Life
- Torture and Ill-Treatment
- Derogation
- Extraterritorial Jurisdiction
- State Obligations
- Human Rights in Armed Conflict

**LAW OF THE SEA**
- Territorial Sea
- Exclusive Economic Zone
- Continental Shelf
- Maritime Delimitation
- Freedom of Navigation
- Marine Environmental Protection

**Technical Requirements:**
- Topics stored in database
- Many-to-many relationship (cases can have multiple topics)
- Admin interface for managing topics (future phase)
- Expandable taxonomy

#### 1.3 Advanced Filters

**Filter Dimensions:**
- International court/tribunal
- Year range
- Document type
- Country/State involved
- Legal topic
- Relevant treaty
- Source category (primary/secondary)

**Supported Courts/Tribunals (MVP):**
- International Court of Justice (ICJ)
- International Criminal Court (ICC)
- International Tribunal for the Law of the Sea (ITLOS)
- International Criminal Tribunal for the former Yugoslavia (ICTY)
- International Criminal Tribunal for Rwanda (ICTR)
- Permanent Court of Arbitration (PCA)
- European Court of Human Rights (ECtHR)
- Inter-American Court of Human Rights (IACtHR)

#### 1.4 Search Results Display

Each result card shows:
- Full case name (clickable)
- Court + Date
- Document type badge
- Legal topic tags
- Matched paragraph excerpt (with search term highlighting)
- Paragraph number
- "View Document" button

**Sorting Options:**
- Relevance (default)
- Date (newest/oldest)
- Court (alphabetical)

**Pagination:**
- 20 results per page
- Clear pagination controls

---

### Feature 2: Legal Authority Reader

**Priority:** CRITICAL

#### 2.1 Document Page Structure

**Metadata Display:**
- Full case name
- Short case name
- Court and chamber
- Date of decision
- Parties (Applicant vs Respondent)
- Procedural stage (Judgment, Order, Advisory Opinion)
- Official citation
- Official source URL (linked)
- Document type
- Related legal topics (tags)

#### 2.2 Document Reader Features

**Text Display:**
- Clean, readable typography
- Paragraph numbers in left gutter
- Page numbers (where available)
- Numbered sections/headings

**Navigation:**
- Jump to paragraph input
- Table of contents (if structured)
- Scroll progress indicator
- Back to top button

**Text Interaction:**
- Select any text
- Search within document
- Highlight passages (future)

#### 2.3 Paragraph-Level Actions

For each paragraph, provide:
1. **Copy Paragraph** — Copy paragraph text only
2. **Copy Citation** — Copy formatted citation with paragraph reference
3. **Copy Paragraph + Citation** — Both together, formatted for Word

**Note:** Save functionality deferred to Phase 9 (Research Workspace - POST-MVP)

**Output Format Example:**
```
[Paragraph text]

Citation: Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 115.
```

#### 2.4 Citation Generator Integration

**Citation Style Selector:**
- OSCOLA (default for UK/international competitions)
- Bluebook (for US-focused competitions)
- Custom Competition Style (future)

**Generated Citation Elements:**
- Full citation
- Short citation
- Pinpoint paragraph reference
- Court abbreviation
- Year
- Report citation

**Copy Actions:**
- Copy citation button
- Visual feedback on successful copy
- Citation preview before copying

---

### Feature 3: Citation Generator

**Priority:** CRITICAL

#### 3.1 Citation Styles (MVP)

**OSCOLA (Oxford Standard for the Citation of Legal Authorities):**

Format:
```
Case Name (Parties) [Year or Report Citation] para X
```

Example:
```
Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 115
```

**Bluebook (20th Edition):**

Format varies by source type. Example for ICJ:
```
Case Name (Country v Country), Year ICJ Rep. page (date of decision)
```

Example:
```
Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 ICJ Rep. 14, ¶ 115 (June 27)
```

#### 3.2 Citation Components

**Required Metadata for Citations:**
- Full case name
- Short case name (parties)
- Court
- Year
- Report citation (ICJ Reports, etc.)
- Page number
- Paragraph number
- Date of judgment
- Procedural stage (Judgment, Order, Advisory Opinion)

#### 3.3 Citation Generation Rules

**Critical Requirements:**
1. Generate from verified metadata only
2. Never fabricate missing information
3. Mark missing or uncertain metadata clearly
4. Use deterministic templates
5. Validate output format
6. Allow user inspection before copy

**Missing Metadata Handling:**
```
✓ Good: "Citation incomplete: paragraph number not available"
✗ Bad: Inventing a paragraph number
```

#### 3.4 Citation Profiles (Future Phase)

Competition-specific profiles:
- Philip C. Jessup International Law Moot Court Competition
- ICC Moot Court Competition
- European Law Students' Association Moot Courts
- Custom user-defined profiles

**Profile Contents:**
- Citation format templates
- Abbreviation rules
- Ordering preferences
- Footnote vs bibliography format

---

### Feature 4: International Law Sources Library

**Priority:** HIGH

#### 4.1 Source Categories

**A. Cases and Decisions** (MVP Focus)
- Judgments (final decisions on merits)
- Orders (procedural decisions)
- Advisory Opinions (ICJ non-contentious proceedings)
- Arbitral Awards
- Tribunal Decisions

**B. Treaties and Conventions** (Phase 2)
- UN Charter
- Geneva Conventions (I-IV)
- Additional Protocols (I-II)
- Rome Statute of the ICC
- UNCLOS
- Vienna Convention on the Law of Treaties
- ICCPR, ICESCR
- Regional human rights treaties

**C. International Organizations' Documents** (Phase 3)
- UN Security Council resolutions
- UN General Assembly resolutions
- ILC Draft Articles
- Reports of Special Rapporteurs
- Advisory Committee on Administrative and Budgetary Questions reports

**D. Customary International Law Materials** (Phase 4)
- ICRC Customary IHL Study
- State practice compilations
- Opinio juris evidence
- Relevant judicial dicta

**E. Secondary Sources** (Phase 5)
- Academic journal articles
- Textbooks and treatises
- Legal commentaries
- Dissertations and working papers

#### 4.2 Source Verification Requirements

**For MVP (Cases):**
- Link to official court website
- Verify case name, date, parties
- Confirm paragraph numbering
- Check official citation
- Record source verification date

**Source Status Indicators:**
- ✅ Verified from official source
- ⚠️ Pending verification
- ℹ️ Metadata incomplete
- 🔗 External source only

---

## Core Features — MVP Scope (Summary)

**MVP includes ONLY the following 4 features:**
1. Advanced Legal Search Engine
2. Legal Authority Reader  
3. Citation Generator
4. Topic-Based Discovery

**Research Workspace is EXCLUDED from MVP** — Deferred to Phase 9 (POST-MVP)

---

## Non-Functional Requirements

### Performance
- Search results in < 2 seconds
- Page load < 3 seconds
- Document reader responsive scrolling
- Efficient database queries with proper indexing

### Scalability
- Support 1000+ legal authorities in MVP
- Design for 10,000+ authorities in future
- Handle 100+ concurrent users
- Efficient full-text search

### Security
- No user authentication in MVP (public read-only)
- Prepare for authentication in Phase 2
- Protect admin functions
- Secure database connections
- Rate limiting on API routes

### Reliability
- 99% uptime target
- Graceful error handling
- Clear error messages
- Fallback mechanisms

### Usability
- Intuitive navigation
- Professional visual design
- Responsive on desktop/tablet
- Accessible (WCAG AA)
- Fast keyboard navigation

### Maintainability
- Clean, modular code
- Comprehensive documentation
- Type safety (TypeScript)
- Automated testing
- Version control

---

## Technical Constraints

### MVP Constraints
- No authentication system
- No payment processing
- Public read-only access
- No email notifications
- No social features
- No mobile app

### Data Constraints
- Start with 5 verified ICJ cases for MVP (expand to 15-20+ in Phase 10)
- 1-case prototype first (Nicaragua v US, 10 paragraphs)
- Expand to 5 cases with 100-150 paragraphs total
- Focus on cases relevant to common moot topics
- Ensure each case has official source link
- Manual data entry for MVP
- JSON seed files for initial data

### Browser Support
- Chrome/Edge (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- No IE11 support

---

## Out of Scope for MVP

### Features NOT in MVP
- **User accounts and authentication** (Phase 9: Research Workspace)
- **Personal saved searches** (Phase 9: Research Workspace)
- **Collaborative workspaces** (Phase 9: Research Workspace)
- **Save cases/paragraphs functionality** (Phase 9: Research Workspace)
- **Research project organization** (Phase 9: Research Workspace)
- Email alerts for new cases
- Mobile applications
- Advanced AI search
- Semantic legal search
- Automatic document parsing
- PDF upload and OCR
- Case law analytics
- Visualization tools
- API for third-party integrations
- Multi-language support

### Future Considerations
These features are valuable but deferred:
- AI-powered case discovery
- Natural language legal queries
- Automated authority verification
- Citation conflict detection
- Memorial drafting assistance
- Oral advocacy preparation tools

---

## Initial Dataset Requirements

### MVP Dataset Scope

**10-20 Landmark ICJ Cases** covering core moot topics:

**State Responsibility & Attribution:**
1. Nicaragua v United States (1986) — Use of force, intervention, attribution
2. Bosnia and Herzegovina v Serbia and Montenegro (2007) — Genocide Convention, attribution
3. Democratic Republic of Congo v Uganda (2005) — Armed activities, occupation

**Use of Force & Self-Defence:**
4. Nicaragua v United States (1986) — Article 2(4), Article 51
5. Oil Platforms (Iran v United States) (2003) — Self-defence
6. Armed Activities on the Territory of the Congo (2005) — Use of force

**Jurisdiction & Immunities:**
7. Arrest Warrant (DRC v Belgium) (2002) — Immunities
8. Jurisdictional Immunities (Germany v Italy) (2012) — State immunity

**Maritime Law:**
9. North Sea Continental Shelf (1969) — Continental shelf, customary law
10. Maritime Delimitation in the Black Sea (2009) — EEZ delimitation

**Other Key Cases:**
11. LaGrand (Germany v United States) (2001) — Consular relations, remedies
12. Avena (Mexico v United States) (2004) — Consular relations
13. Gabčíkovo-Nagymaros Project (1997) — Treaties, state responsibility
14. Pulp Mills (Argentina v Uruguay) (2010) — Environmental law
15. Whaling in the Antarctic (2014) — Treaty interpretation

**Advisory Opinions:**
16. Legality of the Threat or Use of Nuclear Weapons (1996)
17. Legal Consequences of the Construction of a Wall (2004)

### Dataset Requirements

For each case:
- ✅ Full official case name
- ✅ Short case name
- ✅ Court (ICJ)
- ✅ Date of judgment
- ✅ Parties
- ✅ Procedural stage
- ✅ Official citation (ICJ Reports)
- ✅ Official URL
- ✅ Key paragraphs (at least 20 per case)
- ✅ Legal topic tags (3-8 per case)
- ⚠️ Full text (link only if copyright restrictions)

### Data Format

Store as structured JSON for seed data:
```json
{
  "id": "icj-1986-nicaragua",
  "fullName": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v. United States of America)",
  "shortName": "Nicaragua v United States",
  "court": "ICJ",
  "year": 1986,
  "date": "1986-06-27",
  "parties": {
    "applicant": "Nicaragua",
    "respondent": "United States of America"
  },
  "documentType": "Judgment",
  "officialCitation": "ICJ Reports 1986, p. 14",
  "officialUrl": "https://www.icj-cij.org/case/70",
  "topics": ["use-of-force", "self-defence", "intervention", "attribution", "state-responsibility"],
  "paragraphs": [
    {
      "number": 115,
      "text": "[Original paragraph text]",
      "page": 65,
      "topics": ["attribution", "effective-control"]
    }
  ]
}
```

---

## Success Criteria for MVP

### Functional Success
- ✅ User can search by legal topic and find relevant cases
- ✅ User can filter results by court, year, and topic
- ✅ User can view full case metadata and key paragraphs
- ✅ User can navigate to specific paragraphs
- ✅ User can copy paragraphs with one click
- ✅ User can generate OSCOLA and Bluebook citations
- ✅ User can copy citations with paragraph references
- ✅ All citations link to verifiable official sources

### Quality Success
- ✅ All case data verified against official sources
- ✅ All citations tested against manual reference examples
- ✅ Zero fabricated legal authorities or paragraphs
- ✅ Professional visual design matching legal research platforms
- ✅ Fast search performance (< 2 seconds)
- ✅ No critical bugs in core workflows

### Usability Success
- ✅ New user can find a case by topic in < 30 seconds
- ✅ User can copy a formatted citation in < 10 seconds
- ✅ Interface is clear and professional
- ✅ No confusion about what actions do

---

## Risks and Mitigation

### Risk 1: Data Acquisition
**Risk:** Difficult to obtain full-text judgments legally  
**Mitigation:** Link to official sources, provide metadata and key paragraphs only

### Risk 2: Citation Complexity
**Risk:** Citation rules are complex and vary by jurisdiction  
**Mitigation:** Start with two well-documented styles, use validated templates, clearly mark limitations

### Risk 3: Search Relevance
**Risk:** Simple keyword search may not find topically relevant cases  
**Mitigation:** Manual legal topic tagging, synonym expansion, topic-based browsing

### Risk 4: Scope Creep
**Risk:** Feature requests expand beyond MVP  
**Mitigation:** Strict MVP scope, phased development plan, defer non-critical features

### Risk 5: Source Verification Burden
**Risk:** Manually verifying all authorities is time-consuming  
**Mitigation:** Start with 10-20 cases only, prioritize quality over quantity

---

## Timeline Estimate

### Phase 1: Foundation (Weeks 1-2)
- Requirements and architecture (COMPLETE)
- Database design
- Project scaffolding
- Development environment setup

### Phase 2: Core Infrastructure (Weeks 3-4)
- Database schema implementation
- Seed data structure
- Basic Next.js app setup
- UI component library setup (shadcn/ui)

### Phase 3: Search & Browse (Weeks 5-6)
- Search interface
- Legal topic taxonomy
- Filters
- Search results page
- PostgreSQL full-text search

### Phase 4: Document Reader (Weeks 7-8)
- Case detail page
- Paragraph navigation
- Copy functionality
- Document metadata display

### Phase 5: Citation Generator (Weeks 9-10)
- Citation engine architecture
- OSCOLA format
- Bluebook format
- Citation copy integration
- Testing against reference examples

### Phase 6: Initial Dataset (Weeks 11-12)
- Manual case data entry (10-20 cases)
- Source verification
- Paragraph extraction
- Topic tagging
- Database seeding

### Phase 7: Polish & Testing (Weeks 13-14)
- UI/UX refinement
- Bug fixes
- Performance optimization
- Comprehensive testing
- Documentation

**Total MVP Timeline:** 14 weeks

---

## Future Phases (Post-MVP)

### Phase 9: Research Workspace (4 weeks) — POST-MVP

**Priority:** HIGH for Post-MVP  
**Status:** Explicitly EXCLUDED from MVP

#### Feature: Research Workspace

Personal research organization for moot court preparation.

**5.1 Project Organization**

Users can create research projects:
- Project name (e.g., "Jessup 2027 — Applicant Memorial")
- Project description
- Creation date
- Related competition/course

**5.2 Issue-Based Organization**

Within each project:
- Issue I: [Legal Issue Name]
- Issue II: [Legal Issue Name]
- Issue III: [Legal Issue Name]

Under each issue:
- Saved cases
- Saved paragraphs
- Treaties and provisions
- Research notes
- Legal arguments

**5.3 Saved Content**

**Saved Case:**
- Full case metadata
- Link to document
- Custom tags
- Personal notes
- Date saved

**Saved Paragraph:**
- Paragraph text
- Paragraph number
- Parent case
- Citation
- Personal annotation
- Relevant to which issue(s)

**5.4 Export and Sharing**

**Export Options:**
- Export issue outline with authorities (Word/PDF)
- Export all citations (formatted list)
- Export research notes
- Print research summary

**Sharing:** (Future)
- Share project with team members
- Collaborative research spaces
- Comment and discussion threads

**Technical Requirements for Phase 9:**
- User authentication (Supabase Auth)
- User database tables
- Saved content management
- Project organization logic
- Export functionality

---

### Phase 10: Extended Dataset (Ongoing)
### Phase 10: Extended Dataset (Ongoing)
- Expand from 5 to 15-20+ verified ICJ cases
- Add 50+ more cases beyond initial 20
- Include ICTY/ICTR cases
- Add ICC cases
- Include PCA awards
- Regional court cases

### Phase 11: Treaties & Documents (6 weeks)
- Treaty database
- Article-level citation
- UN resolutions
- ILC materials

### Phase 12: Advanced Search (4 weeks)
- Meilisearch integration
- Semantic search
- Synonym expansion
- Better relevance ranking
- Search suggestions

### Phase 13: Competition Profiles (3 weeks)
- Custom citation profiles
- Competition-specific rules
- Citation validation
- Memorial export templates

### Phase 7: AI Features (8 weeks)
- Legal concept extraction
- Case similarity
- Authority recommendations
- Argument structuring assistance

---

## Appendix: Example User Flows

### Flow 1: Find Case by Legal Topic
1. User visits homepage
2. Clicks "Browse by Legal Topic"
3. Expands "USE OF FORCE" → "Self-Defence under Article 51"
4. Sees list of tagged cases
5. Clicks on "Nicaragua v United States"
6. Views case page with relevant paragraphs highlighted
7. Reads paragraph 195 about self-defence
8. Clicks "Copy Paragraph + Citation (OSCOLA)"
9. Pastes into Word document

**Result:** User has correctly formatted citation in < 2 minutes

### Flow 2: Search for Legal Principle
1. User searches "effective control test"
2. Sees results filtered by relevance
3. First result: Nicaragua v United States, para 115
4. Second result: Bosnia v Serbia, para 400-406
5. Clicks first result
6. Jumps directly to paragraph 115
7. Reads paragraph about attribution
8. Switches citation style to Bluebook
9. Copies citation
10. Saves paragraph to "Applicant Memorial — Issue II" (future)

**Result:** User discovers key authority and saves for later

### Flow 3: Browse by Court
1. User clicks "International Court of Justice"
2. Sees all ICJ cases (chronological)
3. Filters by year: 2000-2010
4. Filters by topic: "State Responsibility"
5. Sees 5 relevant cases
6. Opens "Bosnia and Herzegovina v Serbia and Montenegro"
7. Reviews case metadata
8. Clicks official source link to verify on ICJ website

**Result:** User discovers and verifies authority

---

**END OF REQUIREMENTS DOCUMENT**
