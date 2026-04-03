# CLAUDE.md - BLOATED EXAMPLE (FOR VIDEO DEMO)

This file provides guidance to Claude Code when working with code in this repository.

## Project Overview

This is a modern full-stack web application built with Next.js 15, React 19, TypeScript, and Tailwind CSS 4. The application serves as a SaaS platform for project management, allowing teams to collaborate on tasks, track progress, and manage deadlines. It features real-time updates via WebSockets, a REST API backend, PostgreSQL database with Prisma ORM, and authentication via NextAuth.js. The platform supports multiple workspaces, role-based access control, and integrations with third-party services like Slack, GitHub, and Linear.

The project was started in January 2026 and is currently in active development with a team of 4 developers. We follow agile methodology with 2-week sprints. The product manager is Sarah and the tech lead is Mike. We do code reviews on all PRs and deploy to Vercel on merge to main.

## Tech Stack

- **Frontend:** Next.js 15 (App Router), React 19, TypeScript 5.7
- **Styling:** Tailwind CSS 4, shadcn/ui components
- **State Management:** Zustand for client state, React Query for server state
- **Backend:** Next.js API routes + tRPC for type-safe APIs
- **Database:** PostgreSQL 16 via Prisma ORM 6.x
- **Authentication:** NextAuth.js v5 with Google, GitHub, and email providers
- **Real-time:** Socket.io for WebSocket connections
- **File Storage:** AWS S3 via @aws-sdk/client-s3
- **Email:** Resend for transactional emails
- **Monitoring:** Sentry for error tracking, Vercel Analytics
- **Testing:** Vitest for unit tests, Playwright for E2E
- **CI/CD:** GitHub Actions, Vercel for deployment
- **Package Manager:** pnpm 9.x

## Project Structure

```
src/
├── app/                    # Next.js App Router pages
│   ├── (auth)/            # Authentication pages (login, register, forgot-password)
│   ├── (dashboard)/       # Protected dashboard pages
│   │   ├── projects/      # Project management views
│   │   ├── tasks/         # Task management views
│   │   ├── settings/      # User and workspace settings
│   │   └── analytics/     # Analytics and reporting
│   ├── api/               # API routes
│   │   ├── trpc/          # tRPC endpoint
│   │   ├── webhooks/      # Webhook handlers (Stripe, GitHub)
│   │   └── auth/          # NextAuth routes
│   └── layout.tsx         # Root layout
├── components/            # React components
│   ├── ui/                # shadcn/ui base components
│   ├── forms/             # Form components with react-hook-form
│   ├── layouts/           # Layout components (sidebar, header, footer)
│   ├── projects/          # Project-specific components
│   ├── tasks/             # Task-specific components
│   └── shared/            # Shared/reusable components
├── lib/                   # Shared utilities
│   ├── api/               # API client utilities
│   ├── auth/              # Authentication utilities
│   ├── db/                # Database utilities and Prisma client
│   ├── email/             # Email templates and sending
│   ├── hooks/             # Custom React hooks
│   ├── stores/            # Zustand stores
│   ├── trpc/              # tRPC router and procedures
│   ├── utils/             # General utility functions
│   └── validations/       # Zod schemas for validation
├── types/                 # TypeScript type definitions
│   ├── api.ts             # API request/response types
│   ├── database.ts        # Database model types
│   └── global.d.ts        # Global type declarations
├── styles/                # Global styles
│   └── globals.css        # Tailwind directives and custom CSS
└── middleware.ts          # Next.js middleware for auth and redirects
prisma/
├── schema.prisma          # Database schema
├── migrations/            # Database migrations
└── seed.ts               # Database seeding script
```

## Commands

- Install dependencies: `pnpm install`
- Start development server: `pnpm dev`
- Build for production: `pnpm build`
- Start production server: `pnpm start`
- Run all tests: `pnpm test`
- Run unit tests: `pnpm test:unit`
- Run E2E tests: `pnpm test:e2e`
- Run a single test: `pnpm vitest run -t "test name"`
- Type check: `pnpm tsc --noEmit`
- Lint: `pnpm eslint .`
- Format: `pnpm prettier --write .`
- Lint and fix: `pnpm eslint . --fix`
- Generate Prisma client: `pnpm prisma generate`
- Run migrations: `pnpm prisma migrate dev`
- Reset database: `pnpm prisma migrate reset`
- Open Prisma Studio: `pnpm prisma studio`
- Seed database: `pnpm prisma db seed`
- Analyze bundle: `pnpm analyze`
- Clean build cache: `rm -rf .next && rm -rf node_modules/.cache`

## Code Style Guidelines

### General Principles
- Write clean, readable, and maintainable code
- Follow the DRY principle (Don't Repeat Yourself)
- Use meaningful variable and function names
- Keep functions small and focused on a single responsibility
- Write self-documenting code - add comments only when the logic isn't obvious
- Prefer composition over inheritance
- Use early returns to reduce nesting

### TypeScript Conventions
- MUST use TypeScript strict mode at all times
- MUST use functional components with hooks, never class components
- Use `interface` for object shapes that can be extended, `type` for unions and intersections
- Use ES modules (import/export), not CommonJS (require)
- Prefer `const` over `let`, never use `var`
- Use template literals instead of string concatenation
- Use optional chaining (`?.`) and nullish coalescing (`??`) operators
- Prefer `unknown` over `any` - if you must use `any`, add a comment explaining why
- Use `as const` for literal types where appropriate
- Prefer `satisfies` over type assertions where possible
- Use discriminated unions for complex state management
- Always use strict equality (`===`) not loose equality (`==`)
- Prefer `Array.isArray()` over `instanceof Array`
- Use `Record<string, T>` instead of `{ [key: string]: T }`

### React Patterns
- Use Server Components by default, add "use client" only when needed
- Prefer named exports over default exports
- Use the `use` hook for data fetching in Server Components
- Implement error boundaries for graceful error handling
- Use React.memo() only when profiling shows it's needed
- Keep component props interfaces in the same file as the component
- Use the `children` prop pattern for layout components
- Prefer controlled components over uncontrolled components
- Use `useCallback` and `useMemo` judiciously - premature optimization is bad
- Use fragments (`<>...</>`) instead of unnecessary wrapper divs
- Keep JSX clean - extract complex logic into helper functions or hooks

### Naming Conventions
- Components: PascalCase (e.g., `TaskCard.tsx`)
- Utilities/hooks: camelCase (e.g., `useAuth.ts`, `formatDate.ts`)
- Constants: UPPER_SNAKE_CASE (e.g., `MAX_FILE_SIZE`)
- Types/Interfaces: PascalCase with descriptive names (e.g., `TaskWithAssignee`)
- API routes: kebab-case directories (e.g., `api/webhook-handlers/`)
- CSS classes: Use Tailwind utilities, custom classes follow BEM convention
- Environment variables: UPPER_SNAKE_CASE with prefix (e.g., `NEXT_PUBLIC_API_URL`)
- Test files: `*.test.ts` or `*.test.tsx` co-located with source files
- Prisma models: PascalCase singular (e.g., `model User`, not `model Users`)

### Import Order
Organize imports in this exact order, with blank lines between groups:
1. React and Next.js imports
2. Third-party libraries
3. Internal aliases (@/ imports)
4. Relative imports
5. Type imports (using `import type`)
6. CSS/style imports

### Error Handling
- Always handle errors gracefully - never swallow errors silently
- Use try/catch blocks for async operations
- Log errors with context using our logger utility
- Show user-friendly error messages, never expose raw error details
- Use Sentry for error reporting in production
- Implement retry logic for network requests with exponential backoff
- Use Zod for input validation at API boundaries
- Return appropriate HTTP status codes (400, 401, 403, 404, 500)

## Database Conventions

### Prisma Schema
- All models must have `id`, `createdAt`, and `updatedAt` fields
- Use UUID for primary keys: `id String @id @default(uuid())`
- Add `@@index` for commonly queried fields
- Use `@relation` with explicit names for all relations
- Soft delete using `deletedAt DateTime?` field instead of hard deletes
- Use enums for fields with fixed options

### Query Patterns
- Always use `select` or `include` to limit returned fields
- Use transactions for operations that modify multiple tables
- Implement cursor-based pagination, not offset pagination
- Use `findUniqueOrThrow` when the record must exist
- Always handle the `PrismaClientKnownRequestError` for unique constraint violations

## API Conventions

### tRPC Procedures
- Group related procedures in routers (e.g., `taskRouter`, `projectRouter`)
- Use Zod schemas for all input validation
- Always return typed responses
- Implement proper authorization checks using middleware
- Use `protectedProcedure` for authenticated routes
- Handle errors with `TRPCError` and appropriate error codes

### REST API Routes
- Use proper HTTP methods: GET (read), POST (create), PUT (full update), PATCH (partial update), DELETE
- Return consistent response shapes: `{ data, error, message }`
- Use appropriate HTTP status codes
- Implement rate limiting on public endpoints
- Validate request body with Zod
- Add CORS headers for cross-origin requests

## Testing Guidelines

### Unit Tests (Vitest)
- Write tests for all utility functions and hooks
- Use `describe` blocks to group related tests
- Name tests descriptively: `it("should return null when user is not found")`
- Use `beforeEach` and `afterEach` for setup/teardown
- Mock external dependencies using `vi.mock()`
- Aim for 80% code coverage on business logic
- Don't test implementation details, test behavior

### E2E Tests (Playwright)
- Write E2E tests for critical user flows (auth, CRUD operations, payments)
- Use page objects pattern for reusable test helpers
- Run E2E tests in CI before deployment
- Use test fixtures for common setup
- Take screenshots on failure for debugging

## Git Workflow

- Create feature branches from `main` with naming: `feat/description`, `fix/description`, `chore/description`
- Write meaningful commit messages following Conventional Commits format
- Keep commits small and focused
- Squash commits before merging
- NEVER commit directly to main
- NEVER force push to main or shared branches
- Always request at least one review before merging
- Delete branches after merging
- Update your branch with `git rebase main` before creating a PR
- PR titles should follow: `type(scope): description`

## Environment Variables

Required environment variables for development:
- `DATABASE_URL` - PostgreSQL connection string
- `NEXTAUTH_SECRET` - Random string for NextAuth encryption
- `NEXTAUTH_URL` - Application URL (http://localhost:3000 for dev)
- `GOOGLE_CLIENT_ID` - Google OAuth client ID
- `GOOGLE_CLIENT_SECRET` - Google OAuth client secret
- `GITHUB_CLIENT_ID` - GitHub OAuth client ID
- `GITHUB_CLIENT_SECRET` - GitHub OAuth client secret
- `RESEND_API_KEY` - Resend email API key
- `AWS_ACCESS_KEY_ID` - AWS S3 access key
- `AWS_SECRET_ACCESS_KEY` - AWS S3 secret key
- `S3_BUCKET_NAME` - S3 bucket for file uploads
- `SENTRY_DSN` - Sentry error tracking DSN
- `STRIPE_SECRET_KEY` - Stripe API secret key
- `STRIPE_WEBHOOK_SECRET` - Stripe webhook signing secret

Copy `.env.example` to `.env.local` and fill in the values.

## Deployment

We deploy to Vercel. The deployment pipeline works as follows:
1. Push to a feature branch creates a preview deployment
2. Merging to `main` triggers a production deployment
3. Database migrations run automatically via a GitHub Action
4. Environment variables are managed in the Vercel dashboard

### Pre-deployment Checklist
- [ ] All tests pass locally
- [ ] No TypeScript errors
- [ ] No ESLint warnings
- [ ] Database migrations are up to date
- [ ] Environment variables are set in Vercel
- [ ] Bundle size is reasonable (check with `pnpm analyze`)

## Common Gotchas

- The WebSocket server runs on a separate port (3001) in development
- Auth tokens expire every 15 minutes - the client auto-refreshes them
- The `/api/webhooks/stripe` endpoint needs raw body parsing, not JSON
- Prisma Client must be regenerated after schema changes (`pnpm prisma generate`)
- The `middleware.ts` file must stay in the `src/` directory root, not in `app/`
- Socket.io connections don't work in Server Components - use client components
- Image uploads are limited to 10MB by the API route config
- The search index rebuilds nightly at 3am UTC via a cron job

## Performance Guidelines

- Use `next/image` for all images with proper `width` and `height`
- Implement lazy loading for below-the-fold content
- Use `dynamic()` imports for heavy components
- Minimize client-side JavaScript - prefer Server Components
- Use `React.Suspense` with appropriate loading states
- Cache API responses with React Query's stale-while-revalidate
- Implement virtual scrolling for long lists (use `@tanstack/react-virtual`)
- Optimize database queries - use `EXPLAIN ANALYZE` for slow queries
