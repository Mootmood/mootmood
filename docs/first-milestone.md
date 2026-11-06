# MootMood — First Development Milestone

**Milestone Name:** Self-Defence Search Prototype  
**Goal:** Prove the core research workflow with one complete example  
**Timeline:** Weeks 1-10 (Phases 0-5)  
**Status:** Planning Complete, Ready for Implementation

---

## Milestone Overview

This milestone represents the **minimum viable prototype** that demonstrates MootMood's core value proposition: enabling law students to search for legal topics, find relevant authorities, navigate to specific paragraphs, and copy citations.

**Success Criteria:** A user can search for "self-defence", find Nicaragua v United States, read paragraph 195, and copy it with a correct OSCOLA citation — all verified against official sources.

---

## Exact Scope

### Cases Included
1. **Nicaragua v United States (1986)** — Military and Paramilitary Activities in and against Nicaragua (Nicaragua v. United States of America), Judgment (Merits)

### Paragraphs Included (10 key paragraphs)
- **Para 115:** Effective control test for attribution
- **Para 176:** Armed attack vs mere frontier incident
- **Para 188:** Necessity and proportionality in self-defence
- **Para 191:** Collective self-defence requirements
- **Para 194:** Right of self-defence under customary law
- **Para 195:** Requirements for exercise of self-defence (★ PRIMARY TEST PARAGRAPH)
- **Para 200:** Reporting to Security Council
- **Para 211:** Prohibition of intervention
- **Para 228:** Humanitarian intervention not justified
- **Para 292:** Dispositif (judgment summary)

### Legal Topics (4 topics)
1. **Use of Force → Self-Defence (Article 51)**
2. **Use of Force → Non-Intervention**
3. **State Responsibility → Attribution of Conduct → Effective Control Test**
4. **Use of Force → Collective Self-Defence**

### Citation Styles
- **OSCOLA** (Oxford Standard for Citation of Legal Authorities)
- **Bluebook** (The Bluebook: A Uniform System of Citation, 21st ed.)

---

## Features Included in Milestone

### 1. Homepage
- Search bar (prominent hero element)
- "Browse Legal Topics" section
- "Browse by Court" section
- Recent cases display (shows Nicaragua case)

### 2. Search Functionality
- Keyword search
- Topic filtering (hierarchical)
- Court filtering
- Search results with excerpts
- Pagination (even with 1 case, implement the structure)

### 3. Case Detail Page
- Case metadata display
- Official source link
- Verification badge
- Topic tags
- Related paragraphs list

### 4. Document Reader
- Paragraph-numbered display
- Paragraph numbers in left gutter
- "Jump to Paragraph" functionality
- Paragraph anchors in URL
- Copy paragraph button

### 5. Citation Generator
- Citation style selector
- OSCOLA formatter (full and pinpoint)
- Bluebook formatter (full and pinpoint)
- Copy citation button
- Copy paragraph + citation button
- Citation validation and warnings

---

## User Stories

### Story 1: Keyword Search Workflow

**As a** law student preparing for a moot court competition,  
**I want to** search for "self-defence" and find relevant ICJ cases,  
**So that** I can cite authoritative jurisprudence in my memorial.

**Acceptance Criteria:**
1. I open MootMood homepage
2. I type "self-defence" in the search bar
3. I press Enter or click Search
4. I see Nicaragua v United States case in results
5. Result card shows case name, court, date, and relevant excerpt
6. I click on the case name
7. Case detail page loads
8. I see complete case metadata and paragraphs

**Expected Time:** < 30 seconds to find case

---

### Story 2: Topic Browse Workflow

**As a** law student researching use of force doctrines,  
**I want to** browse cases by legal topic,  
**So that** I can discover all cases related to self-defence.

**Acceptance Criteria:**
1. I open MootMood homepage
2. I click "Browse Legal Topics"
3. I see hierarchical topic list
4. I expand "Use of Force"
5. I click "Self-Defence (Article 51)"
6. I see Nicaragua v United States case listed
7. Case count shows "1 case"
8. I click case name → opens case detail page

**Expected Time:** < 45 seconds to navigate to case

---

### Story 3: Paragraph Navigation & Citation

**As a** law student writing about self-defence requirements,  
**I want to** find and cite paragraph 195 of the Nicaragua case,  
**So that** I can support my legal argument with proper citation.

**Acceptance Criteria:**
1. I am on Nicaragua case detail page
2. I see "Jump to Paragraph" input
3. I type "195"
4. I press Enter
5. Page scrolls to paragraph 195
6. URL updates to include `#para-195`
7. I read: "...the exercise of the right of self-defence..."
8. I select "OSCOLA" citation style
9. I click "Copy Paragraph + Citation"
10. I paste into Microsoft Word
11. Both paragraph text and citation appear correctly formatted
12. Citation reads: "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195"

**Expected Time:** < 15 seconds to copy citation

---

### Story 4: Effective Control Research

**As a** law student researching attribution in state responsibility,  
**I want to** find the effective control test,  
**So that** I can understand when conduct is attributed to a state.

**Acceptance Criteria:**
1. I search for "effective control"
2. I see Nicaragua case (paragraph 115 match)
3. I open case and jump to paragraph 115
4. I read about effective control test
5. I see topic tag "Attribution of Conduct → Effective Control Test"
6. I click tag → see all cases with this topic (just Nicaragua for now)
7. I copy paragraph with Bluebook citation
8. Citation reads: "Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14, ¶ 115 (June 27)"

---

## Detailed Acceptance Criteria

### Homepage (9 criteria)
- [ ] Page loads in < 2 seconds
- [ ] Search bar is prominently displayed
- [ ] Search bar is functional (typing works)
- [ ] "Browse Legal Topics" section exists
- [ ] "Browse by Court" section exists
- [ ] Nicaragua case appears in "Recent Cases"
- [ ] SEO metadata present (title, description, Open Graph)
- [ ] Responsive layout works on desktop, tablet, mobile
- [ ] No console errors

### Search Results (12 criteria)
- [ ] Search "self-defence" returns Nicaragua case
- [ ] Search "nicaragua" returns Nicaragua case
- [ ] Search "effective control" returns Nicaragua case
- [ ] Search "attribution" returns Nicaragua case
- [ ] Search "intervention" returns Nicaragua case
- [ ] Search with no results shows "No results found" message
- [ ] Result card shows case name (clickable)
- [ ] Result card shows court and date
- [ ] Result card shows relevant excerpt
- [ ] Clicking case name navigates to case page
- [ ] Search is case-insensitive
- [ ] Loading state shown while searching

### Topic Browse (8 criteria)
- [ ] Legal topics page loads
- [ ] Topics displayed in hierarchical structure
- [ ] "Use of Force" is expandable
- [ ] "Self-Defence (Article 51)" is visible under "Use of Force"
- [ ] Clicking topic shows cases tagged with that topic
- [ ] Case count displayed next to topic name
- [ ] Nicaragua case appears under relevant topics
- [ ] Breadcrumb navigation works

### Case Detail Page (15 criteria)
- [ ] Page loads in < 2 seconds
- [ ] URL format: `/cases/icj-1986-nicaragua`
- [ ] Full case name displayed correctly
- [ ] Short case name displayed
- [ ] Court: "International Court of Justice (ICJ)"
- [ ] Date: "27 June 1986" or "1986-06-27"
- [ ] Parties: "Nicaragua v. United States of America"
- [ ] Document type: "Judgment"
- [ ] Official citation: "ICJ Reports 1986, p. 14"
- [ ] Official URL linked: https://www.icj-cij.org/case/70
- [ ] "View Official Source" button opens URL in new tab
- [ ] Verification badge: "✅ Verified against official source"
- [ ] 4 topic tags displayed (clickable)
- [ ] SEO metadata appropriate for the case
- [ ] Responsive layout

### Document Reader (14 criteria)
- [ ] All 10 paragraphs displayed
- [ ] Paragraph numbers in left gutter (not inline)
- [ ] Paragraph numbers styled distinctly (grey, smaller font)
- [ ] Paragraph text is readable (16px minimum, good line height)
- [ ] Text is selectable (user can highlight)
- [ ] "Jump to Paragraph" input exists
- [ ] Entering "195" and pressing Enter scrolls to para 195
- [ ] Smooth scrolling animation
- [ ] URL updates to `/cases/icj-1986-nicaragua#para-195`
- [ ] Direct URL with anchor works (sharable link)
- [ ] Page loads with anchor scrolls to correct paragraph
- [ ] Each paragraph has visible "Copy Paragraph" button
- [ ] "Copy Paragraph" button shows hover state
- [ ] No layout shift when buttons appear

### Copy Functionality (12 criteria)
- [ ] Click "Copy Paragraph" on any paragraph
- [ ] Visual feedback appears (toast notification or checkmark icon)
- [ ] Feedback disappears after 2-3 seconds
- [ ] Paste into Word → paragraph text appears
- [ ] Paste into Notepad → plain text appears (no HTML)
- [ ] Pasted text preserves line breaks if any
- [ ] No weird characters or formatting issues
- [ ] Copy works in Chrome, Firefox, Safari
- [ ] Copy works on Mac and Windows
- [ ] Copy works on mobile (if tested)
- [ ] Multiple paragraphs can be copied sequentially
- [ ] No errors in console when copying

### Citation Generator - OSCOLA (15 criteria)
- [ ] Citation style selector visible on case page
- [ ] Dropdown shows "OSCOLA" and "Bluebook"
- [ ] "OSCOLA" is default selection
- [ ] Full citation preview displays when no paragraph selected:
  ```
  Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14
  ```
- [ ] Citation uses correct punctuation and spacing
- [ ] "Copy Citation" button exists
- [ ] Click "Copy Citation" → citation copied to clipboard
- [ ] Visual feedback on copy
- [ ] When paragraph 195 is in focus (via jump or scroll), citation updates to pinpoint:
  ```
  Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195
  ```
- [ ] Pinpoint citation includes "para 195" (not "¶ 195" for OSCOLA)
- [ ] "Copy Paragraph + Citation" button exists
- [ ] Click "Copy Paragraph + Citation" → both copied:
  ```
  [Paragraph text]
  
  Citation: Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195.
  ```
- [ ] Format is clean and ready to paste into Word
- [ ] Manually verified against OSCOLA 4th ed. guide
- [ ] Citation matches official OSCOLA ICJ judgment format

### Citation Generator - Bluebook (15 criteria)
- [ ] Select "Bluebook" from dropdown
- [ ] Full citation preview displays:
  ```
  Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14 (June 27)
  ```
- [ ] Party names abbreviated correctly ("Nicar." and "U.S.")
- [ ] Court abbreviation: "I.C.J." (with periods)
- [ ] Date format: "(June 27)" — month abbreviated, day only
- [ ] When paragraph selected, pinpoint citation displays:
  ```
  Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14, ¶ 115 (June 27)
  ```
- [ ] Paragraph symbol "¶" used (not "para")
- [ ] Paragraph number follows page number
- [ ] "Copy Citation" works
- [ ] "Copy Paragraph + Citation" works with Bluebook format
- [ ] Manually verified against Bluebook 21st ed., Rule 21.5
- [ ] Citation matches official Bluebook ICJ format
- [ ] Short-form citation option available (future: can defer)
- [ ] Full and short forms distinguished
- [ ] Works for all 10 paragraphs

### Data Verification (10 criteria)
- [ ] Case metadata verified against https://www.icj-cij.org/case/70
- [ ] Full case name matches official source exactly
- [ ] Date matches official judgment date
- [ ] Official citation matches ICJ Reports
- [ ] All 10 paragraphs verified against official PDF
- [ ] Paragraph numbers confirmed correct
- [ ] Paragraph text is exact (no paraphrasing)
- [ ] No fabricated content
- [ ] Verification record documented in database
- [ ] Verification date recorded

### Performance (8 criteria)
- [ ] Homepage loads in < 2 seconds
- [ ] Search results appear in < 2 seconds
- [ ] Case page loads in < 2 seconds
- [ ] Paragraph scrolling is smooth (60fps)
- [ ] Copy actions complete in < 500ms
- [ ] No blocking JavaScript
- [ ] Lighthouse Performance score > 80
- [ ] No memory leaks (test with Chrome DevTools)

### Cross-Browser Compatibility (6 criteria)
- [ ] Works in Chrome (latest)
- [ ] Works in Firefox (latest)
- [ ] Works in Safari (latest)
- [ ] Works in Edge (latest)
- [ ] Mobile responsive (tested in Chrome DevTools)
- [ ] No JavaScript errors in any browser

### Deployment (8 criteria)
- [ ] Deployed to Vercel
- [ ] HTTPS working (automatic via Vercel)
- [ ] Database connected to Supabase
- [ ] Public URL accessible: `https://mootmood.vercel.app` (or custom domain)
- [ ] Environment variables set in Vercel
- [ ] No errors in Vercel deployment logs
- [ ] Build succeeds without warnings (or only acceptable warnings)
- [ ] Can access from different networks (not just localhost)

---

## Testing Checklist

### Manual Testing Script

**Test 1: Happy Path**
1. Open homepage
2. Search "self-defence"
3. Click Nicaragua case
4. Jump to paragraph 195
5. Copy paragraph + OSCOLA citation
6. Paste into Word
7. ✅ Success if citation is correctly formatted

**Test 2: Topic Browse**
1. Homepage → Browse Legal Topics
2. Expand "Use of Force"
3. Click "Self-Defence (Article 51)"
4. Verify Nicaragua case appears
5. Click case
6. ✅ Success if case page loads correctly

**Test 3: Different Paragraphs**
1. Open Nicaragua case
2. Jump to paragraph 115
3. Copy with Bluebook citation
4. Jump to paragraph 228
5. Copy with OSCOLA citation
6. ✅ Success if both citations correct

**Test 4: Direct Link**
1. Share URL: `https://mootmood.vercel.app/cases/icj-1986-nicaragua#para-195`
2. Open in new browser window
3. ✅ Success if page loads and scrolls to para 195

**Test 5: Mobile**
1. Open on mobile device (or Chrome DevTools mobile view)
2. Search "nicaragua"
3. Open case
4. Copy paragraph
5. ✅ Success if all functions work

---

## Definition of Done

This milestone is **COMPLETE** when:

1. ✅ All 142 acceptance criteria are met
2. ✅ All 5 manual tests pass
3. ✅ Nicaragua case data verified against official source
4. ✅ Both OSCOLA and Bluebook citations tested and verified
5. ✅ Deployed to Vercel and publicly accessible
6. ✅ No critical bugs
7. ✅ Reviewed and approved by project owner

---

## Out of Scope for This Milestone

### Not Included (Save for Later Phases)

❌ Additional cases beyond Nicaragua  
❌ User accounts or authentication  
❌ Save functionality  
❌ Export to Word/PDF  
❌ Advanced search features (boolean, proximity)  
❌ Search suggestions/autocomplete  
❌ Within-document search with highlighting (browser Ctrl+F is sufficient)  
❌ Citation profiles for specific competitions  
❌ Multiple document types (focus on ICJ judgments only)  
❌ Advisory opinions (will add in Phase 6)  
❌ Other courts besides ICJ  
❌ Email sharing  
❌ Print stylesheet  
❌ Dark mode  

---

## Success Metrics

### Quantitative
- Homepage load time: < 2 seconds ✅
- Search response time: < 2 seconds ✅
- Case page load time: < 2 seconds ✅
- Copy action time: < 500ms ✅
- Zero critical bugs ✅
- 100% of acceptance criteria met ✅

### Qualitative
- User can complete research workflow intuitively
- Citations are accurate and properly formatted
- Interface looks professional (not like a student project)
- Data is trustworthy (verified against official source)
- Platform is a genuine research tool (not just a demo)

---

## Next Steps After Milestone Completion

Once this milestone is achieved:

1. **Phase 6:** Add 4 more cases (total 5 cases)
   - Oil Platforms
   - Armed Activities (DRC v Uganda)
   - Legal Consequences of Wall (Advisory Opinion)
   - Certain Activities (Nicaragua v Costa Rica)

2. **Phase 7:** Testing and polish
   - Comprehensive testing
   - UI/UX refinements
   - Performance optimization
   - Bug fixes

3. **Phase 8:** MVP Launch
   - Announce to initial users
   - Gather feedback
   - Monitor usage

4. **Phase 9:** Research Workspace (user accounts)

---

## Timeline

| Week | Phase | Focus |
|------|-------|-------|
| 1-2 | Phase 0 | Planning (✅ COMPLETE) |
| 3-4 | Phase 1 | Infrastructure (database, UI components) |
| 5-6 | Phase 2 | Homepage & Browse |
| 7-8 | Phase 3 | Search functionality |
| 9-10 | Phase 4 | Document reader |
| **10** | **Milestone Review** | **Test against all acceptance criteria** |

**Target Completion:** End of Week 10

---

## Risk Mitigation

### Risk: Data extraction takes longer than expected
**Mitigation:** Nicaragua case is well-documented, paragraphs are clearly numbered, official PDF is available

### Risk: Citation formatting edge cases
**Mitigation:** Start with standard format, handle edge cases in Phase 7

### Risk: PostgreSQL full-text search doesn't work well
**Mitigation:** With only 1 case and 10 paragraphs, even simple LIKE queries would work; plenty of time to optimize

### Risk: Cross-browser compatibility issues
**Mitigation:** Use standard React/Next.js patterns, test early and often

---

## Appendix: Case Metadata Template

**For Reference:**

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
  "documentType": "Judgment",
  "proceduralStage": "Merits",
  "officialCitation": "ICJ Reports 1986, p. 14",
  "caseNumber": "70",
  "officialUrl": "https://www.icj-cij.org/case/70",
  "pdfUrl": "https://www.icj-cij.org/public/files/case-related/70/070-19860627-JUD-01-00-EN.pdf",
  "citationPageNumber": 14,
  "sourceVerified": true,
  "sourceVerifiedDate": "2026-11-15",
  "sourceVerificationLevel": "full",
  "topics": [
    "use-of-force-self-defence",
    "use-of-force-non-intervention",
    "state-responsibility-attribution-effective-control",
    "use-of-force-collective-self-defence"
  ]
}
```

---

**This is your North Star for Phases 1-5. All development should aim to satisfy this milestone.**

---

**END OF FIRST MILESTONE DOCUMENT**
