# Claude Code Configuration - Full Stack Development

This is a Claude Code configuration file for building full stack applications with React/TypeScript frontend and Go backend using Ent ORM.

## Project Overview

**Stack:** Astro + React + TypeScript + Shadcn/ui | Go + Ent | Supabase Auth
**Testing:** Jest + React Testing Library | Go testing + Testify
**Quality:** WCAG 2.3 AA | Security Analysis | Performance Optimization | SEO Optimized

## Core Technologies

### Frontend
- **Astro 4+** as the meta-framework with SSR/SSG capabilities
- **React 18+** with TypeScript 5+ for interactive components
- **Shadcn/ui** component library with Tailwind CSS
- **Astro routing** for file-based routing and SEO optimization
- **Supabase JavaScript SDK** for auth and real-time features
- **View Transitions API** for smooth page transitions

### Backend
- **Go 1.21+** with idiomatic patterns
- **Gin** web framework for HTTP routing
- **Ent** (entgo.io) for database schema and queries
- **Standard library** following effective Go principles
- **Supabase Go Client** for server-side operations

### Database & Auth
- **Supabase** (PostgreSQL) as primary database
- **Ent** for schema definition and type-safe queries
- **Supabase Auth** for user management
- **Row Level Security (RLS)** for data protection

### Testing & Quality
- **Jest + React Testing Library** for frontend testing
- **jest-axe** for accessibility testing
- **Go testing package + Testify** for backend testing
- **Playwright** for end-to-end testing

## Project Structure

```
project/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/              # Shadcn components
│   │   │   ├── react/           # Interactive React components
│   │   │   └── astro/           # Static Astro components
│   │   ├── hooks/               # Custom React hooks
│   │   ├── lib/
│   │   │   ├── supabase.ts      # Supabase client
│   │   │   └── utils.ts         # Utility functions
│   │   ├── layouts/             # Astro layout components
│   │   ├── pages/               # File-based routing (Astro)
│   │   ├── content/             # Content collections
│   │   ├── types/               # TypeScript type definitions
│   │   └── __tests__/           # Test files
│   ├── public/
│   ├── package.json
│   ├── tsconfig.json
│   ├── astro.config.mjs
│   ├── tailwind.config.js
│   ├── components.json          # Shadcn config
│   └── jest.config.js
├── backend/
│   ├── cmd/
│   │   └── server/
│   │       └── main.go
│   ├── internal/
│   │   ├── auth/                # Authentication middleware
│   │   ├── handlers/            # HTTP handlers
│   │   ├── middleware/          # Custom middleware
│   │   └── services/            # Business logic
│   ├── ent/                     # Ent generated code
│   │   ├── schema/              # Entity schemas
│   │   ├── migrate/             # Migrations
│   │   └── ...                  # Generated files
│   ├── pkg/                     # Shared packages
│   ├── tests/                   # Test files
│   ├── go.mod
│   ├── go.sum
│   └── ent.go                   # Ent configuration
├── docker-compose.yml
├── .github/workflows/
├── Claude.md                    # This configuration file
└── README.md
```

## Code Generation Capabilities

### React Components with TypeScript
- Generate SEO-friendly Astro components with optional React interactivity
- Implement proper accessibility attributes (ARIA, semantic HTML)
- Create custom hooks for Supabase integration
- Build forms with validation and error handling
- Implement responsive layouts with Tailwind CSS
- Generate meta tags and structured data for SEO
- Create content collections for blog posts and dynamic content

### Go Backend with Ent
- Generate HTTP handlers following Go conventions
- Create Ent entity schemas with proper relationships
- Implement middleware for authentication and logging
- Build type-safe database queries with Ent
- Generate API documentation and OpenAPI specs

### Authentication & Authorization
- Implement Supabase auth flows (login, register, password reset)
- Create protected routes and middleware
- Handle JWT token validation
- Implement role-based access control (RBAC)
- Generate social authentication providers

## Testing Strategy

### Frontend Testing
```javascript
// Jest configuration for Astro + React Testing Library
{
  "testEnvironment": "jsdom",
  "setupFilesAfterEnv": ["<rootDir>/src/setupTests.ts"],
  "moduleNameMapping": {
    "^@/(.*)$": "<rootDir>/src/$1",
    "^astro:(.*)$": "<rootDir>/src/test-utils/astro-mocks.ts"
  },
  "collectCoverageFrom": [
    "src/**/*.{ts,tsx,astro}",
    "!src/**/*.d.ts"
  ],
  "transform": {
    "^.+\\.astro$": "astro/jest-transformer"
  }
}
```

**Test Types:**
- Unit tests for React components and Astro components
- Integration tests for Supabase client and API routes
- Accessibility tests with jest-axe
- SEO tests for meta tags and structured data
- Performance tests for Core Web Vitals
- Mock implementations for external dependencies

### Backend Testing
```go
// Go testing with Ent test client
func TestHandler(t *testing.T) {
    client := enttest.Open(t, "sqlite3", "file:ent?mode=memory&cache=shared&_fk=1")
    defer client.Close()
    
    // Test implementation
}
```

**Test Types:**
- Unit tests for handlers and services
- Integration tests with test database
- Ent schema and migration testing
- Middleware testing with test contexts
- API endpoint testing with httptest

## SEO Optimization with Astro

### Core SEO Features
- **Server-Side Rendering (SSR):** Dynamic content rendered on the server
- **Static Site Generation (SSG):** Pre-built pages for maximum performance
- **Hybrid Rendering:** Mix of SSR and SSG based on route requirements
- **Automatic Sitemap:** Generated XML sitemaps for search engines
- **Built-in SEO Components:** Meta tags, Open Graph, Twitter Cards

### Astro Configuration
```javascript
// astro.config.mjs
import { defineConfig } from 'astro/config'
import react from '@astrojs/react'
import tailwind from '@astrojs/tailwind'
import sitemap from '@astrojs/sitemap'

export default defineConfig({
  site: 'https://yourdomain.com',
  integrations: [
    react(),
    tailwind(),
    sitemap(),
  ],
  output: 'hybrid', // Enable both SSR and SSG
  adapter: '@astrojs/node', // For deployment
  prefetch: {
    prefetchAll: true,
    defaultStrategy: 'viewport'
  }
})
```

### Content Collections
```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content'

const blogCollection = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    pubDate: z.date(),
    author: z.string(),
    tags: z.array(z.string()),
    image: z.object({
      url: z.string(),
      alt: z.string()
    }).optional()
  })
})

export const collections = {
  'blog': blogCollection
}
```

## Database Schema with Ent

### Entity Definition Example
```go
// ent/schema/user.go
package schema

import (
    "entgo.io/ent"
    "entgo.io/ent/schema/field"
    "entgo.io/ent/schema/edge"
)

type User struct {
    ent.Schema
}

func (User) Fields() []ent.Field {
    return []ent.Field{
        field.String("id").Unique(),
        field.String("email").Unique(),
        field.String("name"),
        field.Time("created_at"),
        field.Time("updated_at"),
    }
}

func (User) Edges() []ent.Edge {
    return []ent.Edge{
        edge.To("posts", Post.Type),
    }
}
```

### Ent Configuration
- **Code Generation:** Automatic struct and query generation
- **Type Safety:** Compile-time query validation
- **Migrations:** Automatic schema migration generation
- **Hooks:** Before/after hooks for data validation
- **Privacy:** Built-in privacy layer for access control

## Accessibility Standards (WCAG 2.3 AA)

### Requirements
- **Semantic HTML:** Proper heading hierarchy, landmarks, lists
- **ARIA Attributes:** Labels, roles, states, and properties
- **Keyboard Navigation:** Full functionality without mouse
- **Color Contrast:** Minimum 4.5:1 for normal text, 3:1 for large text
- **Focus Management:** Visible focus indicators and logical order
- **Screen Reader Support:** Meaningful alternative text and descriptions

### Testing Tools
```javascript
// jest-axe setup
import { axe, toHaveNoViolations } from 'jest-axe'
expect.extend(toHaveNoViolations)

test('should not have accessibility violations', async () => {
  const { container } = render(<Component />)
  const results = await axe(container)
  expect(results).toHaveNoViolations()
})
```

## Security Analysis

### Frontend Security
- **XSS Prevention:** Content sanitization and CSP headers
- **CSRF Protection:** SameSite cookies and token validation
- **Secure Storage:** Secure token storage practices
- **Input Validation:** Client-side validation with server verification
- **Dependency Scanning:** Regular vulnerability assessments

### Backend Security
- **SQL Injection:** Ent's type-safe queries prevent injection
- **Authentication:** JWT validation and refresh token rotation
- **Authorization:** Role-based access control and permissions
- **Rate Limiting:** Request throttling and DDoS protection
- **Input Validation:** Server-side validation and sanitization

## Performance Optimization

### Frontend Performance
- **Static Generation:** Pre-built pages for optimal loading speeds
- **Partial Hydration:** Only interactive components are hydrated
- **Image Optimization:** Built-in responsive images with lazy loading
- **Code Splitting:** Automatic splitting by route and component
- **Prefetching:** Intelligent link prefetching for faster navigation
- **View Transitions:** Smooth page transitions with minimal JavaScript
- **Core Web Vitals:** Optimized for LCP, FID, and CLS metrics

### Backend Performance
- **Database Optimization:** Ent query optimization and indexing
- **Connection Pooling:** Efficient database connection management
- **Caching:** Redis integration for frequently accessed data
- **Memory Management:** Garbage collection tuning
- **Profiling:** CPU and memory profiling with pprof

## Development Commands

### Setup Commands
```bash
# Initialize Astro project
npm create astro@latest

# Setup integrations
npx astro add react tailwind sitemap

# Setup Ent schema
go run entgo.io/ent/cmd/ent init User Post

# Install dependencies
npm install @supabase/supabase-js @radix-ui/react-* class-variance-authority

# Generate Ent code
go generate ./ent
```

### Development Commands
```bash
# Start development servers
npm run dev              # Astro dev server (SSR)
go run cmd/server/main.go # Backend API

# Build commands
npm run build            # Production build
npm run preview          # Preview production build

# Run tests
npm test                 # Frontend tests
go test ./...           # Backend tests
```

### Quality Assurance
```bash
# Accessibility audit
npm run test:a11y

# SEO audit
npm run test:seo

# Security scan
npm audit && go list -json -m all | nancy sleuth

# Performance analysis
npm run build:analyze
lighthouse --only-categories=performance,seo,accessibility http://localhost:4321

# Core Web Vitals
npm run test:vitals
go tool pprof -http=:8080 cpu.prof
```

## Environment Configuration

### Development Environment
```env
# Supabase
SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_anon_key

# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/dbname

# Backend
PORT=8080
JWT_SECRET=your_jwt_secret
CORS_ORIGINS=http://localhost:5173

# Ent
ENT_DEBUG=true
```

### Production Environment
```env
# Supabase
SUPABASE_URL=your_production_url
SUPABASE_SERVICE_KEY=your_service_key

# Database
DATABASE_URL=your_production_db_url

# Backend
PORT=8080
JWT_SECRET=your_production_secret
CORS_ORIGINS=https://yourdomain.com

# SSL
SSL_CERT_PATH=/path/to/cert.pem
SSL_KEY_PATH=/path/to/key.pem
```

## Quality Gates

All code must pass these quality checks before deployment:

1. **Tests:** 100% test suite passing with >80% coverage
2. **Accessibility:** Zero axe-core violations
3. **Security:** No high/critical vulnerabilities
4. **Performance:** Core Web Vitals within thresholds
5. **Type Safety:** TypeScript strict mode compliance
6. **Go Quality:** `go vet` and `golangci-lint` passing
7. **Bundle Size:** Frontend bundle under size limits

## Integration Patterns

### Astro + Supabase Integration
```typescript
// src/lib/supabase.ts
import { createClient } from '@supabase/supabase-js'

export const supabase = createClient(
  import.meta.env.PUBLIC_SUPABASE_URL,
  import.meta.env.PUBLIC_SUPABASE_ANON_KEY
)

// Server-side client for API routes
export const supabaseServer = createClient(
  import.meta.env.SUPABASE_URL,
  import.meta.env.SUPABASE_SERVICE_KEY
)
```

### API Routes with Astro
```typescript
// src/pages/api/auth/login.ts
import type { APIRoute } from 'astro'
import { supabaseServer } from '../../../lib/supabase'

export const POST: APIRoute = async ({ request }) => {
  const { email, password } = await request.json()
  
  const { data, error } = await supabaseServer.auth.signInWithPassword({
    email,
    password
  })
  
  if (error) {
    return new Response(JSON.stringify({ error: error.message }), {
      status: 400,
      headers: { 'Content-Type': 'application/json' }
    })
  }
  
  return new Response(JSON.stringify({ user: data.user }), {
    status: 200,
    headers: { 'Content-Type': 'application/json' }
  })
}
```

### API Design Patterns
- RESTful endpoints following OpenAPI 3.0 specification
- GraphQL integration with Ent (optional)
- Real-time subscriptions via Supabase
- Proper HTTP status codes and error handling
- API versioning and backward compatibility

## AI Assistant Behavior

When generating code, always:
- Provide complete TypeScript type definitions
- Include comprehensive error handling
- Add proper accessibility attributes
- Generate corresponding test files
- Follow established architectural patterns
- Include detailed code comments and documentation
- Suggest performance optimizations
- Validate against security best practices
- Ensure WCAG 2.3 AA compliance

This configuration enables Claude Code to assist with building production-ready full stack applications that are secure, accessible, performant, and maintainable.