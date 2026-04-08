# Resilient Roots Insight — MCFE Japan Dashboard

## Overview
Dashboard built for MCFE (Multicultural Field Experience) consulting project at Babson. Features AI insight panels, Japan-focused analytics, Gen Z category analysis, global mapping, and company/domain selectors. Built with Lovable.

## Tech Stack
- **Framework:** Vite + React + TypeScript
- **Styling:** Tailwind CSS + shadcn/ui
- **Backend:** Supabase
- **Testing:** Vitest + Playwright
- **Package Manager:** Bun

## Project Structure
```
src/
├── pages/
│   └── Index.tsx              # Main dashboard page
├── components/
│   ├── dashboard/
│   │   ├── DashboardLayout.tsx     # Main layout
│   │   ├── AIInsightPanel.tsx      # AI-powered insights
│   │   ├── JapanFocusPanel.tsx     # Japan market focus
│   │   ├── GenZFocusPanel.tsx      # Gen Z analytics
│   │   ├── GenZCategorySelector.tsx # Category filtering
│   │   ├── GlobalMap.tsx           # World map visualization
│   │   ├── CompanySelector.tsx     # Company picker
│   │   ├── DomainSelector.tsx      # Domain filter
│   │   ├── MindsetSelector.tsx     # Mindset category picker
│   │   └── ModeToggle.tsx          # Dark/light mode
│   └── ui/                    # shadcn/ui base components
```

## Key Commands
```bash
bun dev          # Start dev server
bun run build    # Production build
bun run test     # Run tests
```

## Context
- Part of Inan's MCFE course at Babson College (Spring 2026)
- Team project — consulting with Japan-based client
- Course docs in Documents/Babson/MCFE/
- Note: "resilient-roots-insight" is a Lovable auto-generated name. The project IS the MCFE Japan dashboard.

## GitHub
- **Repo:** https://github.com/inanalbert/resilient-roots-insight (private)
- **Duplicate to ignore:** resilient-roots-insight-dad1810b (should be deleted)

## Owner
Inan Kocatepe — Babson MCFE team
