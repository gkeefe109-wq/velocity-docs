# Velocity Stack

## Framework & Runtime
- **SvelteKit 2.57** — file-based routing, server load functions, layout guards
- **Svelte 5.55** — Runes mode (`$state`, `$derived`, `$effect`, `$props`)
- **TypeScript 6** — strict mode
- **Vite 8** — dev server and production build
- **Node.js** — runtime (`@sveltejs/adapter-node`)

## Backend & Database
- **Convex 1.39** — reactive document store, replaces SQL + ORM entirely
  - Queries, mutations, and HTTP actions run on Convex cloud
  - Real-time reactive updates via subscriptions
  - Schema defined in `convex/schema.ts`

## Auth
- **better-auth 1.6** — email/password authentication
  - Runs inside Convex HTTP actions (not SvelteKit server)
  - SvelteKit proxies `/api/auth/*` to Convex to handle CORS and cookies
  - Session stored in Convex `sessions` table, validated via `ConvexHttpClient`

## AI / LLM
- **Vercel AI SDK (`ai` 6.0)** — streaming, model orchestration
- **`@ai-sdk/anthropic` 3.0** — Claude models
- **`@ai-sdk/openai` 3.0** — OpenRouter / OpenAI-compatible
- **`@ai-sdk/svelte` 4.0** — Svelte-native streaming hooks

## UI & Components
- No component library — all components written in-house
- Custom design token system (`design-system/tokens.json`) — CSS vars for color, type, spacing
- **AppSidebar** — collapsible, drag-to-resize, nav sections, user menu
- **StatusBar** — top bar

## Drag & Drop
- **`@neodrag/svelte` 2.3** — draggable elements (cards)

## Tables
- **`@tanstack/table-core` 8.21** — headless table logic

## Content
- **`marked` 18.0** — renders LLM markdown output

## Validation
- **Zod 4.4** — schema validation

## Styling
- **Tailwind CSS 4** — utility-first, via `@tailwindcss/vite`
- Design tokens in `design-system/tokens.json`, surfaced as CSS vars

## Dev Tools
- **ESLint 10** + `eslint-plugin-svelte`
- **Prettier** + `prettier-plugin-svelte` + `prettier-plugin-tailwindcss`
- **Vitest 4** — unit tests
- **Playwright** — end-to-end tests
- **svelte-check** — TypeScript checking for `.svelte` files

## Deployment
- **`@sveltejs/adapter-node`** — builds a Node.js server
- Target: TBD
