# MootMood — Phase 1 Implementation Instructions

**Date:** November 6, 2026  
**Status:** Documentation Complete — Ready for Local Implementation  
**Environment:** This sandbox cannot install npm packages, so Phase 1 must be completed on your local machine

---

## ✅ Phase 0 Complete — All Documentation Ready

I have completed all planning and documentation work. Everything is ready for you to begin implementation on your local development machine.

### What Has Been Delivered

**Core Planning Documents (7 files):**
1. ✅ requirements.md — Complete product requirements
2. ✅ architecture.md — Technical architecture
3. ✅ database-schema.md — Database design
4. ✅ development-roadmap.md — Development plan
5. ✅ PROJECT-OVERVIEW.md — Project summary
6. ✅ README.md — Project introduction
7. ✅ AUDIT-REPORT.md — Comprehensive audit (15,000+ words)

**Supplementary Documentation (4 files):**
8. ✅ docs/first-milestone.md — First prototype definition (142 acceptance criteria)
9. ✅ docs/source-verification-procedure.md — Verification workflow
10. ✅ docs/legal-topic-taxonomy.md — Complete 3-level taxonomy
11. ✅ docs/citation-metadata-requirements.md — Citation requirements & fallbacks

**Configuration Files (2 files):**
12. ✅ .gitignore — Git ignore rules
13. ✅ .env.example — Environment variable template

**Steering Files (4 files in `.kiro/steering/`):**
14. ✅ mootmood-product-vision.md
15. ✅ ui-ux-standards.md
16. ✅ legal-research-accuracy.md
17. ✅ technical-conventions.md

**Total: 17 comprehensive documents ready for implementation**

---

## 🚀 Next Steps: What You Need to Do

### Step 1: Download/Clone This Repository

If this is in a Git repository:
```bash
git clone [repository-url]
cd mootmood
```

Or manually copy all files to your local machine, preserving the directory structure.

---

### Step 2: Set Up Your Local Environment

**Required Software:**
- Node.js 20+ LTS (https://nodejs.org/)
- npm 10+ (comes with Node.js)
- Git (https://git-scm.com/)
- Code editor (VS Code recommended)
- PostgreSQL client (for Supabase connection)

**Verify Installation:**
```bash
node --version  # Should be v20.x or higher
npm --version   # Should be 10.x or higher
git --version
```

---

### Step 3: Create External Accounts

**1. GitHub Account** (if you don't have one)
- Go to: https://github.com/signup
- Create account
- Verify email

**2. Supabase Account** (for database)
- Go to: https://supabase.com/
- Sign in with GitHub (recommended)
- Create new project:
  - Project name: "mootmood" or "mootmood-dev"
  - Database password: [choose strong password, save it]
  - Region: Choose closest to you
  - Plan: Free tier is sufficient for MVP

**3. Vercel Account** (for deployment - can wait until Phase 8)
- Go to: https://vercel.com/signup
- Sign in with GitHub
- No setup needed yet

---

### Step 4: Initialize the Next.js Project

**Open terminal in the project directory and run:**

```bash
# Navigate to your project directory
cd /path/to/mootmood

# Initialize Next.js 14 with TypeScript and Tailwind
npx create-next-app@latest . --typescript --tailwind --app --eslint --import-alias "@/*"

# Answer the prompts:
# ✔ Would you like to use TypeScript? › Yes
# ✔ Would you like to use ESLint? › Yes
# ✔ Would you like to use Tailwind CSS? › Yes
# ✔ Would you like to use `src/` directory? › No
# ✔ Would you like to use App Router? › Yes
# ✔ Would you like to customize the default import alias? › No (@/*)

# This will create:
# - app/ directory (App Router)
# - package.json with dependencies
# - tsconfig.json (TypeScript config)
# - tailwind.config.ts (Tailwind config)
# - next.config.js (Next.js config)
```

---

### Step 5: Install Additional Dependencies

```bash
# Install Prisma for database
npm install prisma @prisma/client

# Install shadcn/ui CLI and components
npx shadcn-ui@latest init

# Answer shadcn prompts:
# ✔ Which style would you like to use? › Default
# ✔ Which color would you like to use as base color? › Slate
# ✔ Would you like to use CSS variables for colors? › Yes

# Install Lucide React for icons
npm install lucide-react

# Install date handling
npm install date-fns

# Development dependencies
npm install -D @types/node
```

---

### Step 6: Configure Database Connection

**Get Supabase Connection String:**
1. Open your Supabase project dashboard
2. Go to: Settings → Database
3. Find "Connection string" section
4. Copy the "URI" connection string (starts with `postgresql://`)
5. Replace `[YOUR-PASSWORD]` with your actual database password

**Create `.env.local` file:**
```bash
# Copy the example file
cp .env.example .env.local

# Edit .env.local and add your Supabase credentials:
DATABASE_URL="postgresql://postgres:[YOUR-PASSWORD]@db.[YOUR-PROJECT-REF].supabase.co:5432/postgres"
DIRECT_URL="postgresql://postgres:[YOUR-PASSWORD]@db.[YOUR-PROJECT-REF].supabase.co:5432/postgres"
```

**Important:** Never commit `.env.local` to Git!

---

### Step 7: Initialize Prisma

```bash
# Initialize Prisma
npx prisma init

# This creates:
# - prisma/schema.prisma
# - Updates .env with DATABASE_URL

# The schema.prisma file should be created with the schema from database-schema.md
```

**You'll need to manually create the Prisma schema based on `database-schema.md`.** I can provide this in the next step.

---

### Step 8: Create Project Structure

```bash
# Create directory structure
mkdir -p app/{search,cases,topics,courts}
mkdir -p components/{ui,legal,search,browse,layout}
mkdir -p lib/{db,citation,search}
mkdir -p types
mkdir -p data/{cases,verification}
mkdir -p prisma/migrations
```

---

### Step 9: Test the Setup

```bash
# Start the development server
npm run dev

# Open browser to http://localhost:3000
# You should see the default Next.js page

# In another terminal, test Prisma connection:
npx prisma studio

# This should open Prisma Studio in your browser at http://localhost:5555
```

If everything works, you're ready for Phase 1 implementation!

---

## 📋 Phase 1 Detailed Tasks

Once the setup is complete, implement these in order:

### Task 1: Configure Tailwind (30 min)

**Edit `tailwind.config.ts`:**
```typescript
import type { Config } from 'tailwindcss'

const config: Config = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        // MootMood color palette
        navy: {
          DEFAULT: '#1e3a5f',
          dark: '#142945',
          light: '#2a5080',
        },
        'muted-blue': {
          DEFAULT: '#4a90e2',
          light: '#6ba3e8',
          dark: '#3a7dce',
        },
        'off-white': '#f8f9fa',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'Fira Code', 'monospace'],
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}

export default config
```

### Task 2: Create Prisma Schema (1 hour)

**Edit `prisma/schema.prisma`:**

Use the complete schema from `database-schema.md`. I can provide the full Prisma schema file if needed.

Key tables:
- Courts
- Cases  
- Paragraphs
- LegalTopics
- CaseTopics (join table)
- ParagraphTopics (join table)
- CitationStyles

### Task 3: Run Database Migration (15 min)

```bash
# Generate Prisma Client
npx prisma generate

# Create and run initial migration
npx prisma migrate dev --name init

# Verify in Prisma Studio
npx prisma studio
```

### Task 4: Install shadcn/ui Components (30 min)

```bash
# Install base components
npx shadcn-ui@latest add button
npx shadcn-ui@latest add input
npx shadcn-ui@latest add card
npx shadcn-ui@latest add badge
npx shadcn-ui@latest add dropdown-menu
npx shadcn-ui@latest add checkbox
npx shadcn-ui@latest add dialog
npx shadcn-ui@latest add toast
```

### Task 5: Create Root Layout (30 min)

**Edit `app/layout.tsx`:**
```typescript
import type { Metadata } from 'next'
import { Inter } from 'next/font/google'
import './globals.css'

const inter = Inter({ subsets: ['latin'] })

export const metadata: Metadata = {
  title: 'MootMood — Search Smarter. Plead Stronger.',
  description: 'International Law Legal Research & Moot Court Platform',
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        {children}
      </body>
    </html>
  )
}
```

### Task 6: Create Basic Homepage (30 min)

**Edit `app/page.tsx`:**
```typescript
export default function Home() {
  return (
    <main className="min-h-screen bg-off-white">
      <div className="container mx-auto px-4 py-16">
        <h1 className="text-4xl font-bold text-navy text-center mb-4">
          MootMood
        </h1>
        <p className="text-lg text-center text-gray-600 mb-8">
          Search Smarter. Plead Stronger.
        </p>
        <div className="text-center text-sm text-gray-500">
          Phase 1: Core Infrastructure Complete
        </div>
      </div>
    </main>
  )
}
```

### Task 7: Test Build (15 min)

```bash
# Test production build
npm run build

# Check for TypeScript errors
npx tsc --noEmit

# Run linter
npm run lint
```

---

## ✅ Phase 1 Completion Checklist

**Phase 1 is complete when:**
- [ ] Next.js app runs on `localhost:3000`
- [ ] TypeScript compiles without errors
- [ ] Tailwind CSS is working (styles apply correctly)
- [ ] shadcn/ui components installed
- [ ] Prisma schema created
- [ ] Database connected (Prisma Studio opens)
- [ ] Initial migration successful
- [ ] Production build succeeds (`npm run build`)
- [ ] Project structure created (all directories)
- [ ] `.env.local` configured (not in Git)
- [ ] Basic homepage displays

---

## 📸 Expected Result

**After Phase 1, you should have:**
1. A working Next.js 14 application with TypeScript
2. Database connected to Supabase
3. Tailwind CSS configured with MootMood colors
4. shadcn/ui components ready to use
5. Project structure established
6. Development environment fully functional

**What you can do:**
- Run `npm run dev` → see homepage at `localhost:3000`
- Run `npx prisma studio` → view database
- Edit components and see hot reload
- Ready to build Phase 2 features

---

## 🎯 What's Next: Phase 2

After Phase 1 is complete and tested, Phase 2 will implement:
- Homepage with search bar
- Browse by Topics page
- Browse by Courts page
- Basic navigation
- Layout components (Header, Footer)

---

## ❓ Common Issues & Solutions

### Issue 1: npm install fails
**Solution:** Check Node.js version (`node --version`), should be 20+

### Issue 2: Prisma can't connect to database
**Solution:** Verify `DATABASE_URL` in `.env.local`, test connection in Supabase dashboard

### Issue 3: TypeScript errors
**Solution:** Run `npm install` again, restart VS Code, check `tsconfig.json`

### Issue 4: Tailwind styles not applying
**Solution:** Check `globals.css` has Tailwind directives, restart dev server

### Issue 5: Port 3000 already in use
**Solution:** Kill process using port 3000, or run `npm run dev -- -p 3001`

---

## 📞 Summary

**Phase 0 is complete.** All planning and documentation is finished.

**Phase 1 must be done on your local machine** because this Kiro Web sandbox cannot install npm packages.

**Follow the steps above** to set up your development environment and complete Phase 1.

**Once Phase 1 is done,** you'll have a working Next.js application ready for Phase 2 feature implementation.

---

## 📁 Repository Organization Recommendation

**Before starting Phase 1**, I recommend:

1. Create a GitHub repository
2. Push all planning documents to the repository
3. Then initialize Next.js in the same repository
4. This way, documentation and code live together

**Git workflow:**
```bash
# On your local machine
git init
git add .
git commit -m "chore: Phase 0 planning and documentation complete"
git branch -M main
git remote add origin [your-github-repo-url]
git push -u origin main

# Then proceed with Phase 1 setup
```

---

**You are ready to begin Phase 1 implementation on your local machine.**

**Let me know when Phase 1 is complete, and I'll help with Phase 2!**

---

**MootMood — Search Smarter. Plead Stronger.**
