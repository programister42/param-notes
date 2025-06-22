# Backend Structure Document (backend-structure)

## 1. Overview

- High-level backend architecture: Next.js App Router (App Directory) with API routes under `app/api/`, running serverless functions
- Key responsibilities: authentication, note CRUD, AI chat, sync, migrations

## 2. Folder & Module Organization

- `app/api/` for API endpoints (App Router)
- `services/` for business logic (auth, notes, chat)
- `db/` for Drizzle schema definitions and migrations
- `lib/utils/` for shared utilities (error handling, logging)
- `middleware/` for request validation and authentication
- `types/` for TypeScript interfaces and domain models

## 3. API Endpoints

- **Auth Routes:** register, login, logout, refresh token
- **Note Routes:** create, read, update, delete, list, tag operations
- **Tag Routes:** list all tags, assign/remove tag
- **Chat Routes:** send message, fetch history, RAG query
- **Sync Routes:** offline changes sync

## 4. Data Models & Schema

- **User:** id, email, passwordHash, createdAt
- **Note:** id, userId, title, content, createdAt, updatedAt
- **Tag:** id, userId, name
- **NoteTag:** join table for many-to-many
- **Embedding:** id, noteId, vector, updatedAt
- **ChatSession** (optional): id, userId, context, messages

## 5. Service Layer

- **AuthService:** JWT issuance, token refresh, password hashing
- **NoteService:** business logic for note operations, tag management
- **ChatService:** context retrieval, vector store lookup, LLM calls
- **SyncService:** diff calculation, conflict resolution, upserts

## 6. Database Migrations & ORM

- Drizzle schema definitions
- Versioned migrations folder structure
- Seed scripts for development

## 7. Integrations & External Dependencies

- **Database:** Neon PostgreSQL
- **LLM Provider:** Gemini Flash API client
- **Search:** PostgreSQL vector extension
- **Auth:** BetterAuth or custom JWT middleware

## 8. Error Handling & Logging

- Centralized error classes and handlers
- Logging strategy (structured logs, error levels)
- Integration with monitoring (Sentry)

## 9. Security Considerations

- Input validation and sanitization
- Authentication and authorization flows
- Rate limiting and abuse prevention
- Data encryption in transit

## 10. Deployment & Scaling

- Vercel serverless function limitations
- Connection pooling through PgBouncer/Neon's proxy
- Caching layers (optional)
