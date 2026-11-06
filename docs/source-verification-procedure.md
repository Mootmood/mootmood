# MootMood — Source Verification Procedure

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Approved for MVP Implementation

---

## Purpose

This document defines the mandatory procedure for verifying legal authorities before including them in the MootMood database. **Every case and paragraph must be verified against official sources** to maintain the platform's legal accuracy integrity.

---

## Core Principle

**Never fabricate or infer legal content.**

All case metadata, paragraph text, and citation information must be traceable to official sources. If verification cannot be completed, the case must not be included in the database.

---

## Verification Levels

### Level 1: Metadata Verification (Minimum Required)

✅ **Required for all cases**

**Checklist:**
- [ ] Visit official court website
- [ ] Verify full case name (exact spelling, including parenthetical)
- [ ] Verify parties (Applicant vs Respondent, exact names)
- [ ] Verify judgment date (day, month, year)
- [ ] Verify official citation (ICJ Reports year and page)
- [ ] Verify case number (court's internal reference)
- [ ] Copy official source URL
- [ ] Check PDF availability
- [ ] Record verification date

**Source Priority:**
1. Official court website (e.g., icj-cij.org)
2. Official reports (e.g., ICJ Reports)
3. UN Official Document System
4. Court's official case repository

**Output:** Metadata verification record

---

### Level 2: Paragraph Verification (Standard for MVP)

✅ **Required for MVP**

**Checklist:**

For each paragraph:
- [ ] Open official PDF or court website
- [ ] Locate paragraph number in document
- [ ] Copy paragraph text (exact wording, character-for-character)
- [ ] Verify page number (if applicable)
- [ ] Note section heading (if applicable)
- [ ] Confirm paragraph is publicly accessible
- [ ] Check for tables, footnotes, or special formatting
- [ ] Record extraction method (PDF copy, OCR, manual transcription)

**Extraction Methods:**

**Method 1: Direct PDF Copy (Preferred)**
- Open official PDF
- Select paragraph text
- Copy to plain text editor
- Verify no character corruption
- Paste into JSON file

**Method 2: Official Website Copy**
- Navigate to judgment on court website
- Locate paragraph
- Copy text from HTML
- Verify against PDF if available

**Method 3: Manual Transcription (Only if necessary)**
- Type paragraph from official document
- Double-check every word
- Have second person verify
- Mark as "manually transcribed" in notes

**DO NOT:**
- ❌ Paraphrase or summarize
- ❌ Correct grammar or spelling
- ❌ Add explanatory text
- ❌ Translate (use original language)
- ❌ Infer paragraph content from summaries

**Output:** Paragraph-level verification record

---

### Level 3: Full Verification (Gold Standard)

🌟 **Optional but recommended**

**Additional Requirements:**
- [ ] All metadata verified against multiple sources
- [ ] All paragraphs extracted and verified
- [ ] Both OSCOLA and Bluebook citations tested
- [ ] Independent verification by second reviewer
- [ ] PDF archived locally (if copyright permits)
- [ ] Verification notes comprehensive

**Output:** Complete verification dossier

---

## Verification Record Template

### Case-Level Verification Record

Create `docs/verification/[case-id].json`:

```json
{
  "caseId": "icj-1986-nicaragua",
  "verificationDate": "2026-11-15",
  "verifiedBy": "Your Name",
  "verificationLevel": "standard",
  
  "sources": {
    "primarySource": "https://www.icj-cij.org/case/70",
    "pdfUrl": "https://www.icj-cij.org/public/files/case-related/70/070-19860627-JUD-01-00-EN.pdf",
    "alternativeSources": [
      "https://www.icj-cij.org/en/case/70"
    ],
    "officialReportsCitation": "ICJ Reports 1986, p. 14"
  },
  
  "metadataVerification": {
    "fullNameVerified": true,
    "fullNameSource": "ICJ official case list",
    "actualFullName": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v. United States of America)",
    
    "partiesVerified": true,
    "applicant": "Nicaragua",
    "respondent": "United States of America",
    
    "dateVerified": true,
    "judgmentDate": "1986-06-27",
    "dateSource": "ICJ Reports 1986",
    
    "officialCitationVerified": true,
    "officialCitation": "ICJ Reports 1986, p. 14",
    "citationSource": "ICJ Reports (official)",
    
    "caseNumberVerified": true,
    "caseNumber": "70",
    "caseNumberSource": "ICJ website"
  },
  
  "paragraphVerification": {
    "method": "direct_pdf_copy",
    "pdfVersion": "EN (English official translation)",
    "paragraphsVerified": [115, 176, 188, 190, 194, 195, 200, 211, 228, 292],
    "totalParagraphsInJudgment": 292,
    "extractionDate": "2026-11-15",
    
    "paragraphDetails": {
      "115": {
        "verified": true,
        "pageNumber": 65,
        "sectionHeading": "V. Use of Force",
        "hasSpecialFormatting": false,
        "extractionMethod": "pdf_copy",
        "notes": "Attribution paragraph, effective control test"
      },
      "195": {
        "verified": true,
        "pageNumber": 103,
        "sectionHeading": "V. Use of Force - Self-Defence",
        "hasSpecialFormatting": false,
        "extractionMethod": "pdf_copy",
        "notes": "Key self-defence requirements paragraph"
      }
    },
    
    "extractionNotes": "All paragraphs copied directly from official PDF. No OCR required. Paragraph numbering verified against PDF. No tables or footnotes in selected paragraphs."
  },
  
  "citationVerification": {
    "oscolaVerified": true,
    "oscolaReference": "OSCOLA 4th ed., section 2.1.1 (ICJ cases)",
    "oscolaTestCitation": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14",
    "oscolaVerifiedAgainst": "Official OSCOLA guide examples",
    
    "bluebookVerified": true,
    "bluebookReference": "Bluebook 21st ed., Rule 21.5 (ICJ)",
    "bluebookTestCitation": "Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14 (June 27)",
    "bluebookVerifiedAgainst": "Bluebook official examples",
    
    "testParagraph": 195,
    "oscolaPinpointCitation": "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14, para 195",
    "bluebookPinpointCitation": "Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14, ¶ 195 (June 27)"
  },
  
  "issues": [],
  "warnings": [],
  "nextReviewDate": "2027-11-15",
  
  "overallStatus": "verified",
  "confidence": "high",
  "notes": "Full verification completed. All metadata and paragraphs verified against official ICJ PDF. Both citation styles tested and confirmed correct."
}
```

---

## Step-by-Step Verification Workflow

### Step 1: Identify Target Case

**Before starting:**
- Determine which case to include
- Confirm it's available from official sources
- Check copyright/access restrictions

**Output:** Case selected and prioritized

---

### Step 2: Obtain Official Documents

**Actions:**
1. Navigate to official court website
2. Locate case by name or number
3. Download official PDF (if available)
4. Bookmark official case page
5. Check for multiple document versions (judgment, separate opinions, orders)
6. Identify the correct document (usually: Judgment on Merits)

**For ICJ:**
- Website: https://www.icj-cij.org
- Navigate to: Cases → List of Cases → Select case
- Download: "Judgment" document (usually PDF)

**Output:** Official source obtained and accessible

---

### Step 3: Verify Metadata

**Actions:**
1. Open verification record template
2. Fill in case metadata from official source
3. Cross-check multiple official references
4. Copy exact spelling and formatting
5. Record source URLs
6. Note any discrepancies

**Common Metadata Issues:**
- Party name variations (use official version)
- Date format differences (use YYYY-MM-DD in database)
- Citation format variations (use ICJ Reports official format)
- Multiple case numbers (use primary court reference)

**Output:** Completed metadata section of verification record

---

### Step 4: Select and Extract Paragraphs

**Selection Criteria:**
- Legal significance (key holdings, tests, principles)
- Relevance to common moot topics
- Clarity and quotability
- Representative of different legal issues
- Operative paragraphs (dispositif)

**Extraction Process:**
1. Open official PDF
2. Navigate to paragraph
3. Note paragraph number and page number
4. Select paragraph text (entire paragraph)
5. Copy to plain text editor
6. Verify no character corruption
7. Paste into JSON structure
8. Repeat for each paragraph
9. Double-check all paragraph numbers

**Quality Checks:**
- ✅ Paragraph number matches PDF
- ✅ Text is exact (not paraphrased)
- ✅ No added commentary
- ✅ Formatting preserved (line breaks, emphasis)
- ✅ Special characters correct (quotes, dashes, symbols)

**Output:** Verified paragraph text with source references

---

### Step 5: Test Citation Generation

**Actions:**
1. Generate OSCOLA citation from metadata
2. Compare against OSCOLA guide examples
3. Generate Bluebook citation from metadata
4. Compare against Bluebook manual examples
5. Test pinpoint citations (with paragraph numbers)
6. Paste into Microsoft Word to check formatting
7. Document any ambiguities or edge cases

**Reference Materials:**
- OSCOLA 4th ed.: https://www.law.ox.ac.uk/research-subject-groups/publications/oscola
- Bluebook 21st ed.: Available through subscription or library

**Output:** Verified citation formats

---

### Step 6: Create Case Data File

**Actions:**
1. Create `src/data/cases/[case-id].json`
2. Include verified metadata
3. Include verified paragraphs
4. Include topic associations
5. Include verification status
6. Include source references

**File Structure:**
```json
{
  "id": "icj-1986-nicaragua",
  "courtId": "icj",
  "fullName": "...",
  "shortName": "...",
  "applicant": "...",
  "respondent": "...",
  "judgmentDate": "1986-06-27",
  "year": 1986,
  "documentType": "Judgment",
  "officialCitation": "ICJ Reports 1986, p. 14",
  "officialUrl": "https://www.icj-cij.org/case/70",
  "sourceVerified": true,
  "sourceVerifiedDate": "2026-11-15",
  "verificationLevel": "standard",
  "verificationRecord": "docs/verification/icj-1986-nicaragua.json",
  "paragraphs": [
    {
      "number": 115,
      "text": "[exact paragraph text]",
      "pageNumber": 65,
      "topics": ["attribution-effective-control"]
    }
  ],
  "topics": ["self-defence", "non-intervention", "attribution-effective-control"]
}
```

**Output:** Complete case data file ready for database seeding

---

### Step 7: Independent Review (Recommended)

**Actions:**
1. Have second person review verification record
2. Spot-check paragraphs against PDF
3. Verify citations independently
4. Confirm source URLs work
5. Document review in verification record

**Output:** Reviewed and confirmed verification

---

## Database Integration

### Verification Status Fields

Add to `cases` table:

```sql
source_verified BOOLEAN DEFAULT false,
source_verified_date DATE,
source_verification_level VARCHAR(50), -- 'metadata', 'standard', 'full'
source_notes TEXT,
verification_record_path VARCHAR(500), -- Link to JSON verification record
```

### Display Verification Status

**On case pages, show:**

✅ **Verified** — "Verified against official source (ICJ Reports 1986)"  
⚠️ **Pending** — "Verification in progress"  
ℹ️ **Incomplete** — "Metadata verified, paragraphs pending"

---

## Quality Assurance Checklist

Before marking a case as "verified":

- [ ] Full case name matches official source exactly
- [ ] Date matches official judgment date
- [ ] Official citation verified
- [ ] Official URL tested and works
- [ ] All paragraph numbers verified against PDF
- [ ] All paragraph text is exact (not paraphrased)
- [ ] OSCOLA citation tested
- [ ] Bluebook citation tested
- [ ] Verification record created and saved
- [ ] No fabricated or inferred content

---

## Error Handling

### If Official Source is Unavailable
- **Do not proceed** with case inclusion
- Document issue in project notes
- Select alternative case
- Wait until source becomes available

### If Paragraph Numbers Are Ambiguous
- Use primary official document as reference
- Note ambiguity in verification record
- Include alternative paragraph references if exist
- Mark with warning in database

### If Citation Format Is Unclear
- Follow official citation guide strictly
- Document ambiguity in verification notes
- Provide warning in UI
- Do not guess format

---

## Re-verification Schedule

**Recommended:**
- Re-verify all cases annually
- Check official URLs still work
- Update if official citation changes
- Archive verification records for audit trail

---

## MVP Timeline Estimate

**Per Case:**
- Metadata verification: 15-30 minutes
- Paragraph extraction (10 paragraphs): 30-60 minutes
- Citation testing: 15-30 minutes
- Verification record creation: 15-30 minutes

**Total per case: 1.5-2.5 hours**

**For 5 cases: 7.5-12.5 hours** of verification work

---

**This procedure is mandatory. Never skip verification to save time.**

---

**END OF SOURCE VERIFICATION PROCEDURE**
