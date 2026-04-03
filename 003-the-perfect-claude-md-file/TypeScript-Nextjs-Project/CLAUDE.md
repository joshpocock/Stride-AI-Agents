# Commands
- Dev: pnpm dev
- Build: pnpm build
- Test: pnpm vitest run
- Test single: pnpm vitest run -t "test name"
- Typecheck: pnpm tsc --noEmit
- Lint: pnpm eslint .
- Format: pnpm prettier --write .

# Code Standards
- MUST use TypeScript strict mode
- MUST use Server Components by default, "use client" only when needed
- Use ES modules (import/export), not CommonJS
- Prefer early returns over nested conditionals
- Use unknown and narrow types, NEVER use any

# Architecture
- App routes: src/app/
- Components: src/components/
- Server logic: src/server/
- Utilities: src/lib/
- See @docs/architecture.md for full system design

# Workflow
- Create feature branches from main
- NEVER commit directly to main
- PR titles follow conventional commits (feat:, fix:, chore:)

# After Every Change
1. pnpm tsc --noEmit
2. pnpm vitest run
3. pnpm eslint .

# Common Mistakes
- Auth tokens expire every 5 min - do not cache them
- The /api/webhook endpoint requires raw body parsing
- Use shadcn/ui components - do not install new UI libraries

# Do Nots
- NEVER modify package.json without asking
- NEVER skip error handling - always show user feedback
- NEVER hardcode config values - they live in .env
