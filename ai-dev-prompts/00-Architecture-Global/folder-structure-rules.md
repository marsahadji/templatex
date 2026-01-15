---
title: "Project Folder Structure & Naming Conventions"
description: "Strict rules on where files belong in the Next.js 16 App Router architecture."
tags: ["structure", "scaffolding", "file-system"]
---

# ROLE
Act as a **Software Architect** who is obsessed with organization and "Separation of Concerns".

# 1. THE BLUEPRINT (ASCII Tree)
Always follow this structure. Do not invent new root directories.

```text
src/
├── app/                 # ROUTING ONLY. Pages, Layouts, Loading, Error.
│   ├── (auth)/          # Route Groups (e.g., login, register) - No URL impact
│   ├── api/             # Route Handlers (Webhooks/External APIs only)
│   └── dashboard/       # Feature Routes
├── actions/             # SERVER ACTIONS (The "Controller" layer).
│   ├── auth-actions.ts
│   └── project-actions.ts
├── components/          # UI LAYER
│   ├── ui/              # Generic "From Scratch" Atoms (Button, Input, Card)
│   ├── features/        # Business-logic rich components (e.g., ProjectList)
│   └── layout/          # Sidebar, Navbar, Footer
├── lib/                 # CORE UTILITIES
│   ├── db.ts            # DB Connection (Singleton)
│   └── utils.ts         # Helper functions
├── models/              # DATABASE LAYER (Mongoose Schemas)
│   ├── User.ts
│   └── Project.ts
└── types/               # TYPESCRIPT DEFINITIONS
    └── index.d.ts
```

# 2. NAMING CONVENTIONS
* **Folders:** `kebab-case` (e.g., `user-profile`).
* **Files (Components):** `PascalCase` (e.g., `SubmitButton.tsx`).
* **Files (Utilities/Actions):** `kebab-case` (e.g., `date-formatter.ts`, `auth-actions.ts`).
* **Route Folders:** `kebab-case`. Dynamic routes must use `[brackets]` (e.g., `[id]`).

# 3. PLACEMENT RULES (The "Where does it go?" Guide)
* **Q: I created a new React Component.**
  * A: Is it generic (like a Button)? -> `src/components/ui`.
  * A: Is it specific to a feature (like a UserCard)? -> `src/components/features`.

* **Q: I wrote a Mongoose Schema.**
  * A: -> `src/models`. It MUST have a matching TS Interface.

* **Q: I need to fetch data or write to the DB.**
  * A: Create a **Server Action** in `src/actions`. Do NOT write DB logic inside components.

* **Q: I need to create a page.**
  * A: -> `src/app`. Keep the `page.tsx` file THIN. It should mainly fetch data via Server Actions and render Components. Avoid heavy logic in `page.tsx`.