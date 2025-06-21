# Database Schema Design

## Overview

ParamNotes uses PostgreSQL with Drizzle ORM for type-safe database operations. The schema is designed for offline-first functionality with conflict resolution and AI context management.

## Core Design Principles

1. **Offline-First Architecture**: All tables include versioning and sync metadata
2. **Soft Deletes**: Critical data uses `isDeleted` flags instead of hard deletes
3. **User Isolation**: All user data is properly isolated with foreign key constraints
4. **AI Context Ready**: Embedding storage and chat history built-in
5. **Performance Optimized**: Strategic indexing for common query patterns

## Table Relationships

### Authentication Layer (Better-Auth)

- **user**: Core user profiles with email verification
- **session**: Active user sessions with expiration
- **account**: OAuth provider connections
- **verification**: Email/phone verification tokens

### Note Management

- **notes**: Main content storage with offline sync metadata
- **note_folders**: Hierarchical folder organization (self-referencing)
- **note_folder_items**: Many-to-many junction for flexible organization

### AI Context System

- **ai_context_embeddings**: Vector storage for semantic search and chat context
- **ai_chat_sessions**: Conversation threads with notes
- **ai_chat_messages**: Individual messages in chat sessions

### Sync Management

- **sync_queue**: Tracks offline changes for background synchronization
- **sync_conflicts**: Handles conflicting edits during sync resolution

## Key Design Decisions

### Offline Sync Strategy

- **Version Tracking**: Each note has a version number incremented on changes
- **Device Tracking**: Changes tagged with device ID for conflict resolution
- **Change Types**: Track create/update/delete operations
- **Last-Write-Wins**: Simple conflict resolution for MVP (can be enhanced later)

### AI Context Management

ParamNotes implements a **RAG (Retrieval-Augmented Generation) system** that combines vector search with AI generation to enable the "chat with your notes" feature.

#### RAG Architecture Overview

- **Vector Database Component**: PostgreSQL with pgvector extension stores note embeddings
- **RAG System Component**: Complete flow that retrieves relevant notes and generates AI responses
- **Integration**: RAG uses the vector database to find relevant context, then feeds it to Gemini Flash

#### Technical Implementation

- **Vector Storage**: Note embeddings stored directly in PostgreSQL using pgvector extension
- **Semantic Search**: HNSW indexes enable fast similarity search across user's notes
- **Hybrid Approach**: Combines semantic search (vectors) with keyword search for better recall
- **Context Injection**: Retrieved note chunks are fed to Gemini Flash for context-aware responses

#### Storage Strategy

- **Phase 1 (MVP)**: Direct pgvector storage with HNSW indexes
- **Phase 2 (Scale)**: Add binary quantization and hybrid search optimization
- **Phase 3 (Advanced)**: Consider dedicated vector DB if scale demands (10M+ notes)

#### Benefits of PostgreSQL + pgvector Approach

- **Single Database**: No separate vector database service to manage
- **ACID Compliance**: Full transactional guarantees for notes and embeddings
- **Cost Effective**: No additional vector database service costs
- **Mature Ecosystem**: Excellent integration with Drizzle ORM and Better-Auth

### Performance Considerations

- **Strategic Indexing**: Composite indexes on frequently queried combinations
- **Soft Delete Indexes**: Include `isDeleted` in relevant indexes
- **User Isolation**: All queries naturally scoped by userId

## Migration Strategy

### Phase 1: Core Tables

1. Better-Auth tables (user, session, account, verification)
2. Basic note management (notes, note_folders, note_folder_items)
3. Essential indexes

### Phase 2: AI Features

1. AI context tables (embeddings, chat sessions/messages)
2. Sync management tables (sync_queue, sync_conflicts)
3. Performance indexes

### Phase 3: Optimizations

1. Vector extension setup (pgvector)
2. Advanced indexing (GIN, GIST)
3. Partitioning for large datasets

## Row Level Security (RLS)

All user data tables will implement RLS policies to ensure:

- Users can only access their own data
- Proper isolation in multi-tenant environment
- Defense against application-level security bugs

## Backup and Recovery

- **Point-in-time Recovery**: Neon PostgreSQL provides automatic backups
- **Schema Versioning**: All migrations tracked in `drizzle_migrations` table
- **Data Export**: User data export functionality for GDPR compliance

## Next Steps

1. Implement actual Drizzle schema files in `src/db/schema.ts`
2. Set up database connection and configuration
3. Create initial migration files
4. Implement basic CRUD operations with tRPC procedures
