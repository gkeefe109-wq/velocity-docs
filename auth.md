# Authorization

Velocity uses [better-auth](https://better-auth.com) for authentication, backed by Convex as the data store.

## How it works

### Sign in flow

1. The browser submits email and password to `/api/auth/sign-in/email`
2. SvelteKit receives the request and proxies it to Convex (`*.convex.site/api/auth/sign-in/email`)
3. Convex runs better-auth, which validates the credentials against the `accounts` table
4. On success, better-auth creates a session record and returns a session cookie
5. The proxy strips the `__Secure-` cookie prefix (required for HTTP on localhost) before forwarding the response to the browser
6. The browser stores the cookie and redirects to `/dashboard`

### Session validation (every page load)

1. SvelteKit's layout server reads the `better-auth.session_token` cookie
2. Extracts the token (the part before the `.` in `TOKEN.SIGNATURE`)
3. Calls Convex directly via `ConvexHttpClient` to look up the session and user
4. If no valid session is found, redirects to `/login`

## Convex tables

| Table | Purpose |
|---|---|
| `users` | One record per registered user. Stores `email`, `screenName`, `avatarInitials`. |
| `accounts` | One record per login method. Stores the hashed password for email/password auth. |
| `sessions` | Active login sessions. Keyed by token, linked to a user. |
| `verifications` | Email verification tokens (reserved for future use). |

## Key files

| File | Role |
|---|---|
| `convex/http.ts` | Mounts better-auth as a Convex HTTP action at `/api/auth/*` |
| `convex/authAdapter.ts` | Bridges better-auth's database interface to Convex queries/mutations |
| `convex/authInternal.ts` | Internal Convex queries and mutations for users, sessions, accounts |
| `convex/auth.ts` | Public Convex query to validate a session token |
| `src/routes/api/auth/[...path]/+server.ts` | SvelteKit proxy — forwards auth requests to Convex, fixes cookies |
| `src/routes/(main)/+layout.server.ts` | Auth guard — validates session on every protected page load |

## Adding a user

Users are created via the seed script (no in-app signup UI yet):

```bash
node scripts/seed-user.mjs <email> <password> "Full Name"
```

This calls better-auth's sign-up endpoint which creates both the `users` and `accounts` records.

## Environment variables

| Variable | Where set | Purpose |
|---|---|---|
| `BETTER_AUTH_SECRET` | Convex env | Signs session tokens |
| `BETTER_AUTH_URL` | Convex env | better-auth base URL (`https://*.convex.site`) |
| `APP_URL` | Convex env | Trusted origin for CORS (`http://localhost:5173`) |
| `PUBLIC_CONVEX_URL` | `.env.local` | Convex query/mutation endpoint |
| `PUBLIC_CONVEX_SITE_URL` | `.env.local` | Convex HTTP action endpoint |
