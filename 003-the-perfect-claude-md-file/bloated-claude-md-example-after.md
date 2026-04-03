# CLAUDE.md

## Commands

```bash
pnpm test:unit                    # unit tests (Vitest)
pnpm test:e2e                     # E2E tests (Playwright)
pnpm vitest run -t "test name"    # single test
pnpm prisma generate              # regenerate client after schema changes
pnpm prisma migrate dev           # run migrations
pnpm analyze                      # bundle size analysis
```

## Code Standards

- Prefer `unknown` over `any` — if `any` is unavoidable, add a comment explaining why
- Use `satisfies` over type assertions where possible
- Named exports only, no default exports
- Soft delete via `deletedAt DateTime?` — never hard delete records
- All Prisma models must have `id` (UUID), `createdAt`, `updatedAt` fields
- Use cursor-based pagination, not offset-based
- API responses follow shape: `{ data, error, message }`

## Architecture

- Server Components by default; add `"use client"` only when needed
- Client state: Zustand. Server state: React Query. Type-safe APIs: tRPC
- Auth: NextAuth.js v5 — use `protectedProcedure` for authenticated tRPC routes
- Real-time: Socket.io on port 3001 (dev) — client components only, not Server Components

## Workflow

- Branch naming: `feat/description`, `fix/description`, `chore/description`
- Commit format: Conventional Commits. PR titles: `type(scope): description`
- Squash commits before merging. Rebase on main before opening PR
- NEVER commit directly to main. NEVER force push to main or shared branches

## Common Mistakes

- `/api/webhooks/stripe` needs raw body parsing, not JSON — Stripe signature verification will fail otherwise
- `middleware.ts` must stay in `src/` root, NOT inside `app/`
- Prisma Client must be regenerated after every schema change (`pnpm prisma generate`)
- Auth tokens expire every 15 minutes — client auto-refreshes, but don't cache tokens server-side
- Image uploads are limited to 10MB by API route config

## Do Nots

- NEVER use `any` without a justifying comment
- NEVER hard delete database records — always soft delete with `deletedAt`
- NEVER use offset pagination — always cursor-based
- NEVER use Socket.io in Server Components — it requires client components
- NEVER expose raw error details to users — log with context, show friendly messages
