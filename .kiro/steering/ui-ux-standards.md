# MootMood UI/UX Standards

## Brand Identity

**Name:** MootMood  
**Tagline:** Search Smarter. Plead Stronger.

## Design Inspiration

Professional legal research platforms:
- Jus Mundi
- Westlaw
- LexisNexis
- Modern academic research platforms
- Premium SaaS dashboards

**NOT:** Generic student projects, ordinary blogs, consumer apps

## Visual Design System

### Color Palette

**Primary Colors:**
- Navy: `#1e3a5f` (or similar dark navy)
- White: `#ffffff`
- Off-white background: `#f8f9fa`

**Accent Colors:**
- Muted blue: `#4a90e2`
- Dark grey: `#2c3e50`
- Light grey: `#e1e8ed`

**Semantic Colors:**
- Success: `#10b981` (green)
- Warning: `#f59e0b` (amber)
- Error: `#ef4444` (red)
- Info: `#3b82f6` (blue)

### Typography

**Font Stack:**
- Headings: Inter, system-ui, sans-serif
- Body: Inter, system-ui, sans-serif
- Monospace: 'JetBrains Mono', 'Fira Code', monospace (for citations)

**Scale:**
- Heading 1: 2.25rem (36px)
- Heading 2: 1.875rem (30px)
- Heading 3: 1.5rem (24px)
- Body: 1rem (16px)
- Small: 0.875rem (14px)
- Tiny: 0.75rem (12px)

**Weight:**
- Regular: 400
- Medium: 500
- Semibold: 600
- Bold: 700

### Spacing

Use Tailwind's spacing scale consistently:
- xs: 0.5rem (8px)
- sm: 1rem (16px)
- md: 1.5rem (24px)
- lg: 2rem (32px)
- xl: 3rem (48px)

### Layout Principles

1. **Clean and organized:** Information-dense without clutter
2. **Scannable:** Clear hierarchy and visual grouping
3. **Professional:** Minimalist approach
4. **Purposeful:** Every element serves the research goal

### Component Design Guidelines

**Avoid:**
- Excessive animations
- Unnecessary gradients
- Oversized headings
- Decorative components without function
- Playful illustrations
- Consumer app styling

**Prefer:**
- Clear typography
- Subtle shadows for depth
- Consistent spacing
- Professional iconography
- Data-forward design

## Key Page Layouts

### Homepage
1. **Header:** Logo + navigation
2. **Hero:** Advanced search bar (prominent)
3. **Quick Access:** Browse by legal topics (grid or columns)
4. **Court Directory:** Browse by international courts
5. **Recent Additions:** Latest legal authorities
6. **About:** Brief platform explanation
7. **Footer:** Links and information

**Visual Focus:** Search bar is the hero element

### Search Results Page

**Layout:** Two-column

**Left Sidebar (25-30%):**
- Applied filters (dismissible chips)
- Legal topics (expandable tree)
- Courts/tribunals (checkboxes)
- Year range
- Document types
- Source categories

**Main Content (70-75%):**
- Results count and search query
- Sort options (relevance, date, court)
- Result cards:
  - Case name (prominent)
  - Court + date
  - Document type badge
  - Legal topic tags
  - Matched paragraph excerpt
  - "View Document" button

### Document Reader Page

**Layout:** Sidebar + main content

**Left Sidebar (25%):**
- Document metadata card
- Quick navigation (jump to paragraph)
- Citation generator
- Table of contents (if available)

**Note:** Save functionality (save to workspace button, save paragraph) deferred to Phase 9 (Research Workspace - POST-MVP)

**Main Content (75%):**
- Document title
- Procedural information
- Full text with paragraph numbers
- Highlight and selection tools
- Paragraph-level actions:
  - Copy paragraph
  - Copy citation
  - Copy both

**Note:** Save functionality deferred to Phase 9

### Research Workspace (POST-MVP - Phase 9)

**Note:** This feature is explicitly EXCLUDED from MVP and deferred to Phase 9.

**Layout:** Project sidebar + main area

**Project Sidebar:**
- Project list
- Active project issues/folders

**Main Area:**
- Saved authorities grouped by issue
- Notes and annotations
- Export options

## Interactive Components

### Search Bar
- Clear input field
- Search button
- Advanced search toggle
- Recent searches dropdown (future)
- Autocomplete suggestions (future)

### Filter Panels
- Collapsible sections
- Clear counts next to options
- "Clear all" button
- Apply/reset actions

### Result Cards
- Hover state with subtle shadow
- Clear clickable area
- Metadata badges
- Excerpt with search term highlighting

### Document Viewer
- Sticky header with document name
- Paragraph numbers in left gutter
- Selectable text
- Action toolbar on selection (MVP):
  - Copy paragraph
  - Copy citation
  - Copy both

**Note:** Save functionality deferred to Phase 9 (Research Workspace)

### Citation Display
- Style selector dropdown
- Generated citation in monospace
- Copy button with success feedback
- Format preview

## Responsive Behavior

**Desktop-first:** Optimize for research on larger screens

**Tablet (768px - 1024px):**
- Collapsible sidebar
- Maintain two-column search results

**Mobile (< 768px):**
- Single column layout
- Bottom sheet filters
- Simplified navigation
- Document reader still functional

## Loading & Empty States

**Loading:**
- Skeleton screens for content areas
- Spinner for actions
- Never block entire UI unnecessarily

**Empty States:**
- Helpful illustration or icon
- Clear explanation
- Actionable suggestion
- Example: "No results found. Try broader search terms or different filters."

**Error States:**
- Clear error message
- Suggested action to resolve
- Option to retry or go back

## Iconography

Use professional icon sets:
- Lucide React (recommended)
- Heroicons
- Consistent size and stroke width
- Used sparingly and meaningfully

## Accessibility

- Semantic HTML structure
- Proper heading hierarchy
- ARIA labels for interactive elements
- Keyboard navigation support
- Focus visible indicators
- Color contrast compliance (WCAG AA)
- Alt text for images

## Animation Guidelines

**Use sparingly:**
- Subtle hover effects (0.2s ease)
- Smooth scrolling
- Modal/dropdown transitions (0.3s)

**Avoid:**
- Page transition animations
- Loading spinners that distract
- Decorative motion

## Voice & Tone

**UI Copy:**
- Professional but accessible
- Clear and direct
- Avoid legal jargon in instructions
- Use legal terminology accurately in content

**Examples:**
- "Search international law authorities"
- "Filter by court or legal topic"
- "Copy citation in OSCOLA format"
