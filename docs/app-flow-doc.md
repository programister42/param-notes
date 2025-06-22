# Application Flow Document (app-flow-doc)

## 1. Purpose

Explain the objectives and scope of app flows, focusing on user efficiency and AI augmentation.

## 2. High-Level User Journeys

- **Journey A:** Create a New Note with AI-Powered Autocomplete
- **Journey B:** Organize and Navigate Existing Notes (tags, search)
- **Journey C:** Chat Contextually with Notes (AI Q&A)

## 3. Detailed Flows

### 3.1 Creating a New Note

1. User Authentication ➔ Dashboard
2. Click "New Note" ➔ Blank editor opens
3. Typing begins ➔ AI suggestions appear inline
4. Accept/Reject suggestions ➔ Editor content updates
5. Save Note ➔ Persist to database, update UI

### 3.2 Organizing Notes

1. View Notes List ➔ Filters & Search available
2. Select Note ➔ Open in editor
3. Apply or Remove Tags ➔ UI reflects changes
4. Bulk actions (delete, archive, share)

### 3.3 Contextual AI Chat

1. User opens Chat panel ➔ Sidebar on the right
2. Chat input ➔ AI processes query with note context
3. AI Response ➔ Display in chat window
4. User can insert AI output into notes or follow up

## 4. Navigation & Screen Map

- Dashboard (chat list)
- Note Editor Screen
- Chat Interface (right-hand panel/sidebar)
- Settings & Profile

## 5. Data & State Management Flow

- Client State (React context, TanStack Query caches)
- API Calls (CRUD, chat)
- Local cache & optimistic updates

## 6. AI Integration Points

- Autocomplete provider (as-you-type hooks)
- Chat endpoint (RAG using Neon PostgreSQL vectors)
- Background enrichment tasks

## 7. PWA & Offline Mode

- The app is a Progressive Web App (PWA) with offline support.
- Notes can be created, edited, deleted, and viewed offline via service worker and local cache.
- AI-powered features (autocomplete and chat) will be disabled when offline.
- On network restoration, offline changes sync to the server and AI features reactivate.
