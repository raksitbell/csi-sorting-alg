# Sorting Match

Sorting Match is a full-stack SvelteKit application for learning and competing with classic sorting algorithms. It includes algorithm education pages, a practice sandbox, real-time multiplayer rooms, guest play, account-based profiles, and ranked match history.

## Core Flows

- **Education**: visual walkthrough pages for Bubble, Selection, Insertion, Quick, Merge, and Heap Sort.
- **Practice**: a standalone practice mode for experimenting with sortable data.
- **Competition**: Socket.IO-powered lobby, private/public rooms, readiness checks, live rounds, scoring, and leaderboard updates.
- **Accounts**: Better Auth email/password login, social providers, password reset email, guest players, and profile pages.

## Tech Stack

- Svelte 5 and SvelteKit
- TypeScript
- Tailwind CSS 4
- Socket.IO
- Better Auth
- Drizzle ORM with PostgreSQL
- Cloudflare Turnstile for sign-in/sign-up protection
- ESLint and Prettier

## Requirements

- Node.js compatible with the versions used by SvelteKit/Vite in `package.json`
- npm
- PostgreSQL database
- Email credentials for password reset mail
- OAuth provider credentials if social login is enabled
- Cloudflare Turnstile site key and secret

## Environment Variables

Create a local `.env` file before running the app:

```env
DATABASE_URL=postgres://user:password@localhost:5432/sorting_match
ORIGIN=http://localhost:5173
PUBLIC_ORIGIN=http://localhost:5173
BETTER_AUTH_SECRET=change-me

EMAIL_USER=
EMAIL_PASS=

GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
DISCORD_CLIENT_ID=
DISCORD_CLIENT_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
ROBLOX_CLIENT_ID=
ROBLOX_CLIENT_SECRET=

PUBLIC_APP_NAME=Sorting Match
PUBLIC_SITE_KEY=
SECRET_KEY=
```

`SECRET_KEY` is the Turnstile secret used by the server hook. `PUBLIC_SITE_KEY` is the Turnstile site key used by the sign-in and sign-up pages.

## Getting Started

Install dependencies:

```bash
npm install
```

Push the current Drizzle schema to the configured database:

```bash
npm run db:push
```

Start the development server:

```bash
npm run dev
```

The default local app URL is `http://localhost:5173`.

## Scripts

- `npm run dev`: start the Vite development server.
- `npm run build`: create a production build.
- `npm run preview`: preview the production build.
- `npm run check`: sync SvelteKit types and run `svelte-check`.
- `npm run lint`: run Prettier checks and ESLint.
- `npm run format`: format the codebase with Prettier.
- `npm run db:push`: push the Drizzle schema to the database.
- `npm run db:generate`: generate Drizzle migration files.
- `npm run db:migrate`: run Drizzle migrations.
- `npm run db:studio`: open Drizzle Studio.
- `npm run auth:schema`: regenerate Better Auth schema output.

## Project Structure

```text
src/routes/                         SvelteKit routes and pages
src/routes/api/                     HTTP API endpoints
src/routes/competition/[id]/        Competition room lobby page
src/routes/competition/[id]/play/   Live competition play page
src/routes/education/               Algorithm learning pages
src/routes/lobby/                   Public/private room lobby
src/lib/components/                 Shared UI and layout components
src/lib/server/                     Server-side auth, database, sockets, and API helpers
src/lib/server/db/                  Drizzle schema and database client
src/lib/server/socket/              Socket.IO handlers, services, middleware, and game state
src/lib/utils/                      Sorting array and solution-step utilities
static/                             Static assets
```

## Development Notes

- This project uses Svelte 5 runes mode by default.
- Server-only code should stay under `src/lib/server` or in `.server.ts` modules.
- Database schema lives in `src/lib/server/db/schema.ts`.
- Room and game events are handled through Socket.IO under `src/lib/server/socket`.
- Run `npm run check` and `npm run lint` before submitting changes once dependencies are installed.

