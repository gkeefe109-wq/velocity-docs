# Velocity Stack

## Framework & Runtime
- **Next.js 16.2.4** — App Router, server components, server actions, Turbopack dev
- **React 19.2.4** — with concurrent features
- **TypeScript 5** — strict mode
- **Node.js** (runtime)

## Database & ORM
- **PostgreSQL 18** — local; Railway-hosted in prod
- **Prisma 7.8** — ORM with `@prisma/adapter-pg` (native pg driver adapter)
- **pg 8.20** — raw PostgreSQL driver

## Auth
- **jose 6.2** — JWT signing/verification
- **bcryptjs 3.0** — password hashing
- Custom session management via `app/lib/session.ts`

## AI / LLM
- **Vercel AI SDK (`ai` 6.0)** — streaming, `useChat`
- **`@ai-sdk/anthropic` 3.0** — Claude models
- **`@ai-sdk/openai` 3.0** — OpenRouter / OpenAI-compatible
- **`@ai-sdk/react` 3.0** — React hooks (`useChat`)

## UI Component System
- **shadcn 4.8** — component library (CLI-managed)
- **Radix UI 1.4** — headless primitives (shadcn's backbone)
- **Lucide React 1.16** — icons
- **`class-variance-authority` 0.7** — variant-based className composition
- **`clsx` + `tailwind-merge`** — className utilities

## Styling
- **Tailwind CSS 4** — utility-first, with `@tailwindcss/postcss`
- **`tw-animate-css`** — animation utilities
- Custom design token system in `design-system/tokens.json` with CSS vars in `globals.css`

## Layout & Drag-and-Drop
- **`@dnd-kit/core`, `/sortable`, `/utilities`** — drag-and-drop for card canvas
- **`react-rnd` 10.5** — resizable + draggable card windows

## State Management
- **Zustand 5.0** — client-side global store (SetupState, etc.)

## External APIs & Data
- **YouTube Data API v3** — via `YOUTUBE_API_KEY`
- **`youtube-transcript`** — fetches video transcripts
- **OpenRouter** — multi-model LLM routing via `OPENROUTER_API_KEY`
- **`@tcgdex/sdk` 2.9** — Pokémon TCG card data

## Content
- **`react-markdown` 10.1** — renders LLM output as markdown

## Validation
- **Zod 4.4** — schema validation

## Dev Tools
- **ESLint 9** + `eslint-config-next`
- **tsx 4.22** — TypeScript script runner (used by `scripts/import-*.ts`)
- **dotenv** — env var loading in scripts

## Deployment
- **Railway** — hosted production environment
