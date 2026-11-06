# MootMood Technical Conventions

## Technology Stack

### Frontend
- **Framework:** Next.js (App Router)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS
- **UI Components:** shadcn/ui
- **State Management:** React hooks + Server Components

### Backend
- **API:** Next.js API routes and Server Actions
- **Database:** PostgreSQL
- **ORM/Query:** Prisma or direct SQL (to be decided)
- **Authentication:** Supabase Auth (future phase)

### Search
- **Phase 1:** PostgreSQL full-text search
- **Future:** Meilisearch or similar (design with migration in mind)
- **Strategy:** Legal topic tagging + synonym expansion

### Deployment
- **Hosting:** Vercel
- **Database:** Supabase or separate PostgreSQL instance
- **Version Control:** GitHub

## Code Quality Standards

### TypeScript
- Use strict type checking
- Define interfaces for all data structures
- No `any` types without explicit justification
- Export types for reusability

### Component Structure
```
src/
├── app/              # Next.js App Router pages
├── components/       # React components
│   ├── ui/          # shadcn/ui base components
│   ├── legal/       # Legal-specific components
│   └── search/      # Search-related components
├── lib/             # Utility functions
│   ├── db/          # Database queries
│   ├── citation/    # Citation generation
│   └── search/      # Search logic
├── types/           # TypeScript type definitions
└── data/            # Initial seed data (JSON)
```

### Naming Conventions
- **Components:** PascalCase (e.g., `SearchBar.tsx`)
- **Files:** kebab-case for non-components (e.g., `citation-generator.ts`)
- **Functions:** camelCase (e.g., `generateCitation`)
- **Constants:** UPPER_SNAKE_CASE (e.g., `DEFAULT_CITATION_STYLE`)
- **Types/Interfaces:** PascalCase (e.g., `CitationStyle`, `LegalAuthority`)

### Error Handling
- Always handle potential errors
- Use try-catch for async operations
- Provide meaningful error messages
- Log errors appropriately
- Return structured error responses from APIs

### Environment Variables
- Store secrets in `.env.local`
- Provide `.env.example` with placeholder values
- Never commit actual secrets
- Prefix public variables with `NEXT_PUBLIC_`

### Testing Strategy
- Unit tests for citation formatting
- Unit tests for search logic
- Integration tests for critical workflows
- Test against manually verified reference examples
- Test edge cases: missing metadata, special characters, etc.

## Git Workflow

### Branch Strategy
- `main` branch is production-ready
- Feature branches: `feature/description`
- Bug fixes: `fix/description`
- Documentation: `docs/description`

### Commit Messages
Format: `type: brief description`

Types:
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `style:` Formatting, no code change
- `refactor:` Code restructuring
- `test:` Adding tests
- `chore:` Maintenance tasks

Example: `feat: add OSCOLA citation generator`

## Performance Considerations

- Use Server Components by default
- Client Components only when interactivity required
- Lazy load heavy components
- Optimize images (Next.js Image component)
- Index database columns used in searches
- Implement pagination for large result sets

## Accessibility

- Semantic HTML
- ARIA labels where appropriate
- Keyboard navigation support
- Sufficient color contrast
- Responsive design (desktop-first for research platform)

## Documentation Requirements

Every module should include:
- Purpose and responsibility
- Input/output specifications
- Example usage
- Edge cases and limitations

Citation generators must document:
- Citation style rules applied
- Required metadata fields
- Output format
- Validation rules
