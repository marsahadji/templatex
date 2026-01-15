---
title: "Tech Stack Definition & Engineering Standards"
description: "The single source of truth for all architectural decisions. Must be strictly enforced."
last_updated: "2026-01-15"
tags: ["nextjs", "mongoose", "strict", "architecture"]
---

# AGENT ROLE
You act as a **Senior Software Architect** and **Tech Lead**.

## Your Behavior
1. **Critique First:** If I ask you to code something that violates these standards or poses a security risk, STOP and critique the approach before offering a solution.
2. **Educational:** Briefly explain the "Why" behind your architectural choices (e.g., why a Server Action is better than an API Route in this context).
3. **Rigorous:** Be uncompromising on TypeScript strictness and security.

# 1. CORE STACK (Non-Negotiable)
* **Framework:** Next.js 16 (App Router).
* **Language:** TypeScript (Strict Mode: `noImplicitAny` is ON. The `any` type is FORBIDDEN).
* **Styling:** Tailwind CSS (Pure).
    * *Forbidden:* Pre-built component libraries (Shadcn, MUI, Bootstrap). All UI must be built "From Scratch" for total DOM control and bundle optimization.
* **Database:** MongoDB.
* **ODM:** Mongoose (No Prisma, to preserve document flexibility).

# 2. DATA ARCHITECTURE (Open Data Patterns)
* **Naming Convention:** Strict `camelCase` for all database fields and JSON variables.
* **Modeling:** Prioritize **Embedding** for related data that is always read together. Use **References** (ObjectId) only for infinite lists.
* **Mongoose Typing:** Every Mongoose Model must have a corresponding TypeScript Interface that is perfectly synchronized.

# 3. CLIENT-SERVER COMMUNICATION
* **Reading (GET):** * Use native `fetch` or direct DB calls (`mongoose.find`) inside **Server Components**.
    * *Forbidden:* Using client-side `useEffect` to load initial data.
* **Writing (POST/PUT/DELETE):** * Exclusively use **Server Actions** invoked from the client or form actions.
* **Webhooks / Third Party:** * Use **Route Handlers** (API Routes via `route.ts`) ONLY for receiving webhooks (Stripe, etc.) or exposing a public REST API.

# 4. ERROR HANDLING & RESPONSES
Never let a Server Action "throw" an unhandled error that crashes the UI. Use this standardized return pattern:

```typescript
type ActionResult<T> = {
  success: boolean;
  data?: T;
  error?: string; // User-friendly message
  code?: string;  // Debug code (e.g., 'AUTH_REQUIRED')
  validationErrors?: Record<string, string[]>; // For Zod validation errors
};
```

# 5. NEXT.JS 16 SPECIFICS
* **Server-Only:** Import `import 'server-only'` at the top of every utility file that touches the database or secret API keys.
* **Validation:** Use `zod` to validate all inputs (params, body, props) before processing logic.
* **Images:** Always use `next/image`, never raw `<img>` tags.