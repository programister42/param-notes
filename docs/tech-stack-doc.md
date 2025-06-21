# Technology Stack Documentation

## Overview

ParamNotes uses a modern, type-safe stack optimized for AI-native features and offline-first functionality. The architecture prioritizes developer experience, performance, and seamless integration between components.

## Core Stack

### Frontend Framework: Next.js 15 App Router + React 19

**Why Next.js:**

- **Mature Ecosystem**: Extensive community support and documentation
- **Server Components**: Perfect for AI data prefetching and SEO
- **API Routes**: Clean integration with our backend stack
- **PWA Support**: Multiple solutions available for Progressive Web App features
- **Deployment**: Optimized for Vercel deployment with edge functions

**Integration Points:**

- Hono API routes via official adapters (`hono/vercel`)
- tRPC client with Server Components support
- Vercel AI SDK native integration
- Shadcn/ui components with App Router

### Backend API: Hono + tRPC

**Hono Framework:**

- **Performance**: Ultra-fast web framework for API routes
- **Type Safety**: Full TypeScript support with context typing
- **Next.js Integration**: Official adapters for seamless integration
- **Middleware Ecosystem**: Rich middleware for auth, CORS, validation

**tRPC Integration:**

- **End-to-End Type Safety**: Shared types between client and server
- **React Server Components**: Prefetching support for optimal performance
- **Developer Experience**: Excellent TypeScript inference and autocomplete
- **Validation**: Zod integration for runtime type checking

### Database: PostgreSQL + Drizzle ORM

**PostgreSQL with Neon:**

- **Serverless**: Auto-scaling with edge support
- **pgvector Extension**: Native vector storage for AI embeddings
- **ACID Compliance**: Full transactional guarantees
- **Performance**: Optimized for both relational and vector operations

**Drizzle ORM:**

- **Type Safety**: Schema-first approach with TypeScript inference
- **Performance**: Minimal overhead with SQL-like query builder
- **Migrations**: Automatic migration generation and management
- **Integration**: Excellent Better-Auth adapter support

### Authentication: Better-Auth

**Why Better-Auth:**

- **Modern**: Built for modern React applications
- **Flexible**: Supports multiple providers and custom flows
- **Type Safe**: Full TypeScript support throughout
- **Database Agnostic**: Works seamlessly with Drizzle ORM

### AI Integration: Vercel AI SDK + Gemini Flash

**Vercel AI SDK:**

- **React Integration**: `useChat` and `useCompletion` hooks
- **Streaming**: Built-in streaming UI components
- **Multi-Model**: Support for multiple AI providers
- **Server Actions**: Seamless Next.js integration

**Google Gemini Flash:**

- **Performance**: Fast response times for real-time suggestions
- **Cost Effective**: Competitive pricing for high-volume usage
- **Large Context**: Handles extensive note context for RAG
- **Reliability**: Enterprise-grade availability and performance

### UI Framework: Shadcn/ui + Tailwind CSS

**Shadcn/ui:**

- **Copy-Paste Components**: Full control over component code
- **Accessibility**: Built-in ARIA support and keyboard navigation
- **Customizable**: Easy theming and variant management
- **Modern**: Latest React patterns and best practices

**Tailwind CSS:**

- **Performance**: Purged CSS for minimal bundle size
- **Developer Experience**: Utility-first approach
- **Consistency**: Design system enforcement
- **Responsive**: Mobile-first responsive design

## Architecture Patterns

### API Layer Architecture

```
Next.js App Router
├── app/api/trpc/[...trpc]/route.ts (tRPC handler)
├── app/api/auth/[...auth]/route.ts (Better-Auth handler)
└── lib/
    ├── hono.ts (Hono app configuration)
    ├── trpc.ts (tRPC router and procedures)
    └── auth.ts (Better-Auth configuration)
```

### Database Layer

```
Database Layer
├── schema.ts (Drizzle schema definitions)
├── migrations/ (Auto-generated migrations)
├── seed.ts (Development data seeding)
└── connection.ts (Database connection setup)
```

### AI Integration Pattern

```
AI Features
├── Chat System (RAG)
│   ├── Vector Search (pgvector)
│   ├── Context Retrieval (tRPC procedures)
│   └── Response Generation (Vercel AI SDK + Gemini)
└── Typing Suggestions
    ├── Context Analysis (note content + cursor position)
    ├── Suggestion Generation (Gemini Flash)
    └── Streaming UI (useCompletion hook)
```

## Integration Benefits

### Type Safety Chain

1. **Database**: Drizzle schema provides TypeScript types
2. **API**: tRPC procedures use database types
3. **Client**: React components get full type inference
4. **AI**: Zod validation ensures type safety for AI inputs/outputs

### Performance Optimizations

1. **Server Components**: AI data prefetching before client hydration
2. **Edge Functions**: Hono APIs deployed to edge for low latency
3. **Vector Search**: pgvector with HNSW indexes for fast similarity search
4. **Streaming**: Real-time AI responses with Vercel AI SDK

### Developer Experience

1. **Hot Reload**: Next.js dev server with instant updates
2. **Type Checking**: Full stack type safety with immediate feedback
3. **Database Introspection**: Drizzle Studio for database visualization
4. **API Testing**: tRPC's built-in type-safe client testing

## Deployment Architecture

### Vercel Deployment

- **Frontend**: Next.js app with static generation where possible
- **API Routes**: Hono handlers deployed as serverless functions
- **Edge Functions**: AI suggestion endpoints for low latency
- **Database**: Neon PostgreSQL with connection pooling

### Environment Configuration

- **Development**: Local PostgreSQL with Docker
- **Staging**: Neon branch database for testing
- **Production**: Neon main branch with read replicas

## Security Considerations

### Authentication Security

- **Session Management**: Better-Auth with secure HTTP-only cookies
- **CSRF Protection**: Built-in CSRF tokens and validation
- **Rate Limiting**: Hono middleware for API protection

### Data Security

- **Row Level Security**: PostgreSQL RLS for user data isolation
- **API Validation**: Zod schemas for all inputs
- **Environment Variables**: Secure secret management

### AI Security

- **Input Sanitization**: Validation before AI processing
- **Content Filtering**: Inappropriate content detection
- **Usage Limits**: Rate limiting for AI API calls

## Performance Metrics

### Target Performance

- **Time to First Byte**: < 200ms
- **First Contentful Paint**: < 1.5s
- **AI Response Time**: < 3s for suggestions, < 5s for chat
- **Database Queries**: < 100ms for typical operations

### Monitoring

- **Vercel Analytics**: Core web vitals and performance metrics
- **Database Monitoring**: Neon's built-in performance insights
- **AI Usage Tracking**: Custom metrics for AI feature adoption

## Next Steps

1. **Project Initialization**: Set up Next.js project with TypeScript
2. **Database Setup**: Configure Neon PostgreSQL and Drizzle ORM
3. **Authentication**: Implement Better-Auth with basic providers
4. **API Layer**: Set up Hono + tRPC integration
5. **UI Foundation**: Configure Shadcn/ui and basic components
6. **AI Integration**: Implement Vercel AI SDK with Gemini Flash
7. **PWA Features**: Add service worker and offline capabilities
