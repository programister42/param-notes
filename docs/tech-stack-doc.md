# Technology Stack Document (tech-stack-doc)

## 1. Overview

Describe the high-level architecture and rationale for chosen technologies.

## 2. Frontend

- **Framework:** React 19 with Next.js (React Compiler)
- **UI Library:** shadcn/ui + Tailwind CSS
- **State Management & Data Fetching:** TanStack Query, React Context
- **PWA & Offline Support:** Next.js PWA plugin or custom service worker via Workbox
- **TypeScript:** end-to-end type safety

## 3. Backend / API

- **Runtime:** Node.js on Vercel (or serverless functions)
- **Authentication:** BetterAuth
- **ORM:** Drizzle ORM
- **API Routes:** Next.js API Routes (REST or tRPC)
- **Business Logic:** modular services layer

## 4. Database & Data Layer

- **Primary Database:** Neon PostgreSQL
- **Full-Text & Vector Search:** PostgreSQL extensions for vector similarity and RAG workflows
- **Connection Pooling & Migrations:** Drizzle Migrations

## 5. AI & Integrations

- **LLM Provider:** Gemini Flash
- **Retrieval Augmented Generation:** vector search against personal note embeddings
- **Autocomplete Hooks:** custom React hooks to fetch streaming completions
- **Chat Service:** integrated via API Route with context retrieval

## 6. DevOps & Infrastructure

- **Hosting:** Vercel (frontend + serverless)
- **CI/CD:** GitHub Actions (lint, test, build, deploy)
- **Environment Management:** dotenv + Vercel environment variables
- **Monitoring & Logging:** Sentry, Logflare, or similar

## 7. Tooling & Developer Experience

- **Linting:** ESLint (with TypeScript & Tailwind plugins)
- **Formatting:** Prettier
- **Pre-commit Hooks:** Husky + lint-staged
- **IDE Setup:** Recommended VSCode extensions (TypeScript, Tailwind, shadcn/ui snippets)

## 8. Security & Compliance

- **Auth Best Practices:** JWT, cookie security, CSRF protection
- **Data Encryption:** TLS in transit, encryption at rest (via Neon)
- **Access Controls:** Role-based access if needed

## 9. Rationale & Trade-offs

Explain why each major technology was selected and any known limitations or future considerations.
