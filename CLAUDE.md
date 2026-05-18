# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Root
- Build all projects: `pnpm build`
- Type-check all projects: `pnpm typecheck`

### API Server (`artifacts/api-server`)
- Development: `pnpm run dev`
- Build: `pnpm run build`
- Start: `pnpm run start`
- Type-check: `pnpm run typecheck`

### Art Gallery (`artifacts/art-gallery`)
- Development: `pnpm run dev`
- Build: `pnpm run build`
- Serve: `pnpm run serve`
- Type-check: `pnpm run typecheck`

### Mockup Sandbox (`artifacts/mockup-sandbox`)
- Development: `pnpm run dev`
- Build: `pnpm run build`
- Preview: `pnpm run preview`
- Type-check: `pnpm run typecheck`

## Architecture & Structure

This is a `pnpm` monorepo containing a backend API, multiple frontend applications, and shared libraries.

### Shared Libraries (`lib/`)
- `db`: Database schema and configuration using Drizzle ORM.
- `api-spec`: Central OpenAPI specification used to generate clients and types via Orval.
- `api-zod`: Zod schemas generated from the API specification for type-safe validation.
- `api-client-react`: Auto-generated React hooks for interacting with the API.

### Artifacts (Applications)
- `api-server`: An Express.js server that implements the API defined in `api-spec`. It uses `lib/db` for data access and `lib/api-zod` for request validation.
- `art-gallery`: A Vite-based React application. It uses Supabase for authentication and storage, and consumes the generated API client from `lib/api-client-react`.
- `mockup-sandbox`: A Vite-based React application for prototyping and mockup previews.

### Key Workflows
- **API Evolution**: Changes should start in `lib/api-spec/openapi.yaml`, then run the generation scripts (via Orval) to update `lib/api-zod` and `lib/api-client-react` before implementing changes in `api-server` or the frontends.
- **Database Changes**: Defined in `lib/db/src/schema`.
