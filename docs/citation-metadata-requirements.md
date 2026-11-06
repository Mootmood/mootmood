# MootMood — Citation Metadata Requirements

**Version:** 1.0  
**Date:** November 6, 2026  
**Status:** Approved for MVP Implementation

---

## Purpose

This document specifies the **exact metadata requirements** for generating citations in different styles and document types. It defines which fields are required, which are optional, and what fallback strategies to use when metadata is incomplete.

---

## General Principles

1. **Never fabricate missing metadata** — If required data is missing, return error
2. **Use fallback strategies for optional fields** — Generate simplified citation with warning
3. **Validate before generation** — Check all required fields exist
4. **Provide transparency** — Tell user what metadata is missing

---

## Document Types

### ICJ Judgment (Priority 1 - MVP)

**Full Citation Requirements:**

#### OSCOLA Format
**Pattern:** `[Full Case Name], [Document Type], [Official Citation]`

**Example:** `Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14`

**Required Metadata:**
- ✅ `fullName` — Full official case name with parties in parentheses
- ✅ `documentType` — "Judgment", "Order", or "Advisory Opinion"
- ✅ `officialCitation` — "ICJ Reports [Year], p [Page]"

**Optional Metadata:**
- `proceduralStage` — "Merits", "Preliminary Objections", etc. (rarely needed in OSCOLA)

**Fallback Strategy (if officialCitation missing):**
```
[Full Case Name], [Document Type], ICJ, [Date]
Warning: "Official citation not available. Using simplified format."
```

**Pinpoint Citation Requirements:**
- Add: `, para [Number]`
- Required: `paragraphNumber` (integer)

---

#### Bluebook Format
**Pattern:** `[Short Case Name], [Year] [Court] [Page], [Pinpoint] ([Date])`

**Example:** `Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14, ¶ 195 (June 27)`

**Required Metadata:**
- ✅ `shortName` — Parties only, abbreviated (e.g., "Nicar. v. U.S.")
- ✅ `year` — Judgment year (integer)
- ✅ `court` — "ICJ" → format as "I.C.J." (with periods)
- ✅ `citationPageNumber` — Starting page in ICJ Reports
- ✅ `judgmentDate` — Full date for "(Month Day)" format

**Optional Metadata:**
- `procedural Stage` — Usually omitted in Bluebook

**Fallback Strategy (if shortName missing):**
- Auto-generate from `fullName`: Extract party names, abbreviate countries
- Example: "Nicaragua v. United States of America" → "Nicar. v. U.S."

**Fallback Strategy (if citationPageNumber missing):**
```
[Short Name], [Court] ([Date])
Warning: "Page number not available. Using simplified format."
```

**Pinpoint Citation Requirements:**
- Add: `, ¶ [Number]` (paragraph symbol, not "para")
- Required: `paragraphNumber` (integer)

---

### ICJ Advisory Opinion (Priority 2 - MVP)

**Differences from Judgment:**
- **No parties** — No Applicant vs Respondent
- **documentType** = "Advisory Opinion"
- **fullName** is just the title (e.g., "Legality of the Threat or Use of Nuclear Weapons")

#### OSCOLA Format
**Pattern:** `[Title], Advisory Opinion, [Official Citation]`

**Example:** `Legality of the Threat or Use of Nuclear Weapons, Advisory Opinion, ICJ Reports 1996, p 226`

**Required Metadata:**
- ✅ `fullName` — Title of advisory opinion
- ✅ `documentType` — Must be "Advisory Opinion"
- ✅ `officialCitation`

**No `shortName` or `applicant`/`respondent` fields**

---

#### Bluebook Format
**Pattern:** `[Title], Advisory Opinion, [Year] I.C.J. [Page] ([Date])`

**Example:** `Legality of the Threat or Use of Nuclear Weapons, Advisory Opinion, 1996 I.C.J. 226 (July 8)`

**Required Metadata:**
- ✅ `fullName` — Title
- ✅ `year`
- ✅ `citationPageNumber`
- ✅ `judgmentDate`

---

### ICJ Order (Priority 3 - Post-MVP)

**Similar to Judgment but:**
- **documentType** = "Order"
- Usually shorter
- Often procedural

**OSCOLA Example:** `Application of the Convention on the Prevention and Punishment of the Crime of Genocide (The Gambia v Myanmar), Provisional Measures, Order, ICJ Reports 2020, p 3`

**Bluebook Example:** `Application of the Convention on the Prevention and Punishment of the Crime of Genocide (Gam. v. Myan.), Order, 2020 I.C.J. 3 (Jan. 23)`

---

## Metadata Field Definitions

### Case Identification

```typescript
interface CaseMetadata {
  // REQUIRED FOR ALL CASES
  id: string;                    // Database ID (e.g., "icj-1986-nicaragua")
  fullName: string;              // Official full case name
  court: string;                 // Court ID (e.g., "icj")
  year: number;                  // Judgment year
  judgmentDate: Date;            // Full judgment date
  documentType: 'Judgment' | 'Order' | 'Advisory Opinion';
  officialUrl: string;           // Official source URL
  
  // HIGHLY RECOMMENDED (for proper citations)
  officialCitation?: string;     // "ICJ Reports 1986, p. 14"
  citationPageNumber?: number;   // 14
  
  // RECOMMENDED (improves citation quality)
  shortName?: string;            // "Nicaragua v United States" or "Nicar. v. U.S."
  
  // CONTENTIOUS CASES ONLY (not Advisory Opinions)
  applicant?: string;            // "Nicaragua"
  respondent?: string;           // "United States of America"
  
  // OPTIONAL (context/organization)
  caseNumber?: string;           // ICJ internal number "70"
  proceduralStage?: string;      // "Merits", "Preliminary Objections"
  
  // VERIFICATION (internal)
  sourceVerified: boolean;
  sourceVerifiedDate?: Date;
  verificationLevel?: string;
}
```

---

## Citation Validation

### Validation Levels

```typescript
interface ValidationResult {
  isValid: boolean;              // Can we generate ANY citation?
  canGenerateCitation: boolean;  // Same as isValid
  style: string;                 // "oscola" or "bluebook"
  errors: string[];              // Missing REQUIRED fields (blocking)
  warnings: string[];            // Missing OPTIONAL fields (non-blocking)
  fallbackUsed: boolean;         // Did we use simplified format?
}
```

### Example Validation Function

```typescript
function validateForOSCOLA(metadata: CaseMetadata): ValidationResult {
  const errors: string[] = [];
  const warnings: string[] = [];
  let fallbackUsed = false;
  
  // Check required fields
  if (!metadata.fullName) errors.push('Case name is required');
  if (!metadata.documentType) errors.push('Document type is required');
  
  // Check highly recommended fields (allow fallback)
  if (!metadata.officialCitation) {
    warnings.push('Official citation missing. Using simplified format.');
    fallbackUsed = true;
    
    // Check if we have fallback data
    if (!metadata.judgmentDate) {
      errors.push('Cannot generate citation without official citation or judgment date');
    }
  }
  
  return {
    isValid: errors.length === 0,
    canGenerateCitation: errors.length === 0,
    style: 'oscola',
    errors,
    warnings,
    fallbackUsed
  };
}
```

---

## Fallback Strategies

### Strategy 1: Official Citation Missing (OSCOLA)

**Scenario:** `officialCitation` is `null` or empty

**Fallback:**
```
[Full Name], [Document Type], ICJ, [Judgment Date]
```

**Example:**
```
Instead of: "Nicaragua v United States, Judgment, ICJ Reports 1986, p 14"
Generate:   "Nicaragua v United States, Judgment, ICJ, 27 June 1986"
```

**Warning Displayed:**
```
⚠️ Official ICJ Reports citation not available. Using court and date reference.
```

---

### Strategy 2: Short Name Missing (Bluebook)

**Scenario:** `shortName` is `null` or empty

**Fallback:** Auto-generate from `fullName`

**Rules:**
1. Extract party names from parentheses
2. Abbreviate country names:
   - "United States" → "U.S."
   - "Nicaragua" → "Nicar."
   - "United Kingdom" → "U.K."
   - "Germany" → "Ger."
   - Use standard Bluebook abbreviations
3. Keep vs. connector

**Example:**
```typescript
function generateShortName(fullName: string): string {
  // Extract: "Nicaragua v. United States of America"
  const partyMatch = fullName.match(/\((.+?)\)/);
  if (!partyMatch) return fullName; // Use full name as fallback
  
  const parties = partyMatch[1];
  // Apply abbreviation rules
  return parties
    .replace('United States of America', 'U.S.')
    .replace('United Kingdom', 'U.K.')
    .replace('Nicaragua', 'Nicar.');
}
```

---

### Strategy 3: Page Number Missing (Bluebook)

**Scenario:** `citationPageNumber` is `null`

**Fallback:** Use year and court only

```
[Short Name], [Court] ([Date])
```

**Example:**
```
"Nicar. v. U.S., I.C.J. (June 27, 1986)"
```

**Warning:**
```
⚠️ ICJ Reports page number not available. Citation may be incomplete.
```

---

## Pinpoint Citations (Paragraph References)

### Requirements

**OSCOLA:**
- Format: `para [Number]`
- Example: `para 195`
- Required: Integer `paragraphNumber`

**Bluebook:**
- Format: `¶ [Number]`
- Example: `¶ 195`
- Required: Integer `paragraphNumber`
- Note: Use paragraph symbol `¶` (Unicode U+00B6), not "para"

### Multiple Paragraphs

**Single paragraph:** `para 195`  
**Consecutive paragraphs:** `paras 195-197`  
**Non-consecutive:** `paras 195, 200, 228`

**Implementation:**
```typescript
interface PinpointReference {
  type: 'single' | 'range' | 'multiple';
  paragraphs: number[];  // [195] or [195, 196, 197] or [195, 200, 228]
}

function formatPinpoint(ref: PinpointReference, style: 'oscola' | 'bluebook'): string {
  const symbol = style === 'bluebook' ? '¶' : 'para';
  
  if (ref.type === 'single') {
    return `${symbol} ${ref.paragraphs[0]}`;
  }
  
  if (ref.type === 'range') {
    return `${symbol}${style === 'bluebook' ? '¶' : 's'} ${ref.paragraphs[0]}-${ref.paragraphs[ref.paragraphs.length - 1]}`;
  }
  
  // multiple non-consecutive
  return `${symbol}${style === 'bluebook' ? '¶' : 's'} ${ref.paragraphs.join(', ')}`;
}
```

---

## Citation Templates (Hard-Coded for MVP)

### OSCOLA Templates

```typescript
class OSCOLAFormatter {
  formatFullICJJudgment(metadata: CaseMetadata): string {
    const validation = this.validate(metadata);
    if (!validation.isValid) {
      throw new CitationError(validation.errors);
    }
    
    if (metadata.officialCitation) {
      return `${metadata.fullName}, ${metadata.documentType}, ${metadata.officialCitation}`;
    }
    
    // Fallback
    const dateStr = this.formatDate(metadata.judgmentDate, 'long');
    return `${metadata.fullName}, ${metadata.documentType}, ICJ, ${dateStr}`;
  }
  
  formatPinpointICJJudgment(metadata: CaseMetadata, paragraph: number): string {
    return `${this.formatFullICJJudgment(metadata)}, para ${paragraph}`;
  }
  
  private formatDate(date: Date, format: 'long' | 'short'): string {
    if (format === 'long') {
      const day = date.getDate();
      const month = date.toLocaleDateString('en-GB', { month: 'long' });
      const year = date.getFullYear();
      return `${day} ${month} ${year}`; // "27 June 1986"
    }
    return date.toISOString().split('T')[0]; // "1986-06-27"
  }
}
```

### Bluebook Templates

```typescript
class BluebookFormatter {
  formatFullICJJudgment(metadata: CaseMetadata): string {
    const validation = this.validate(metadata);
    if (!validation.isValid) {
      throw new CitationError(validation.errors);
    }
    
    const shortName = metadata.shortName || this.generateShortName(metadata.fullName);
    const courtAbbrev = 'I.C.J.'; // Always with periods for Bluebook
    
    if (metadata.citationPageNumber) {
      const dateStr = this.formatDate(metadata.judgmentDate);
      return `${shortName}, ${metadata.year} ${courtAbbrev} ${metadata.citationPageNumber} (${dateStr})`;
    }
    
    // Fallback
    const dateStr = this.formatDateFull(metadata.judgmentDate);
    return `${shortName}, ${courtAbbrev} (${dateStr})`;
  }
  
  formatPinpointICJJudgment(metadata: CaseMetadata, paragraph: number): string {
    const base = this.formatFullICJJudgment(metadata);
    // Insert paragraph before date parentheses
    const parts = base.split(' (');
    if (parts.length === 2) {
      return `${parts[0]}, ¶ ${paragraph} (${parts[1]}`;
    }
    return `${base}, ¶ ${paragraph}`;
  }
  
  private formatDate(date: Date): string {
    const month = date.toLocaleDateString('en-US', { month: 'short' }); // "Jun"
    const day = date.getDate();
    return `${month}. ${day}`; // "June 27" or abbreviated if needed
  }
  
  private generateShortName(fullName: string): string {
    // Extract parties from parentheses
    const match = fullName.match(/\((.+?)\)/);
    if (!match) return fullName;
    
    let parties = match[1];
    
    // Apply common abbreviations
    parties = parties
      .replace(/United States of America/g, 'U.S.')
      .replace(/United Kingdom/g, 'U.K.')
      .replace(/Nicaragua/g, 'Nicar.')
      .replace(/Germany/g, 'Ger.');
    
    return parties;
  }
}
```

---

## Error Messages

### User-Facing Error Messages

**Missing Required Field:**
```
❌ Cannot generate citation: Case name is missing.
```

**Missing Optional Field (with warning):**
```
⚠️ Citation generated with limited information. Official ICJ Reports citation not available.
```

**Invalid Paragraph Number:**
```
❌ Cannot generate pinpoint citation: Paragraph number must be a positive integer.
```

**Unknown Citation Style:**
```
❌ Citation style 'harvard' is not supported. Available styles: OSCOLA, Bluebook.
```

---

## Testing Requirements

### Test Cases for Citation Generation

**Test 1: Complete Metadata**
```typescript
const completeCase: CaseMetadata = {
  fullName: "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v. United States of America)",
  shortName: "Nicar. v. U.S.",
  documentType: "Judgment",
  officialCitation: "ICJ Reports 1986, p. 14",
  citationPageNumber: 14,
  year: 1986,
  judgmentDate: new Date('1986-06-27'),
  // ... other fields
};

// Expected OSCOLA: "Military and Paramilitary Activities in and against Nicaragua (Nicaragua v United States of America), Judgment, ICJ Reports 1986, p 14"
// Expected Bluebook: "Military and Paramilitary Activities in and Against Nicaragua (Nicar. v. U.S.), 1986 I.C.J. 14 (June 27)"
```

**Test 2: Missing Official Citation (Fallback)**
```typescript
const noOfficialCitation: CaseMetadata = {
  fullName: "...",
  documentType: "Judgment",
  officialCitation: null, // MISSING
  year: 1986,
  judgmentDate: new Date('1986-06-27'),
  // ... other fields
};

// Expected OSCOLA: "[Full Name], Judgment, ICJ, 27 June 1986"
// Expected Warning: "⚠️ Official citation not available"
```

**Test 3: Pinpoint Citation**
```typescript
const withParagraph = {
  ...completeCase,
  paragraphNumber: 195
};

// Expected OSCOLA: "[...], ICJ Reports 1986, p 14, para 195"
// Expected Bluebook: "[...], 1986 I.C.J. 14, ¶ 195 (June 27)"
```

---

## Future Document Types (Post-MVP)

### ICC Judgment
- Different citation format
- Case number instead of parties
- Example: `Prosecutor v Lubanga, ICC-01/04-01/06, Judgment, 14 March 2012`

### Arbitral Award (PCA)
- Different format
- Example: `South China Sea Arbitration (Philippines v China), PCA Case No 2013-19, Award, 12 July 2016`

### UN Security Council Resolution
- Simple format
- Example: `UNSC Res 1441 (8 November 2002)`

**Defer these to Phase 10+**

---

**This document defines the contract between the database and the citation engine. Follow it strictly.**

---

**END OF CITATION METADATA REQUIREMENTS**
