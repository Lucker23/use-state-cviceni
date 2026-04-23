# CLAUDE.md — Dota AI Coach

## Project
Dota 2 AI coach. 3 revenue tiers:
1. B2C pubs — $9.99/mo, 3–6k MMR players
2. B2B coach tool — $5–15k/mo for pro teams (CHILLZER is first customer)
3. Unranked/bot training simulator — legal playground, "Aim Lab for Dota"

Builder: Yuriy (Lucker23), YK Nanotech Trading s.r.o., Prague.
Brand face: NONEK.
Design partner: CHILLZER.

## Stack (locked)
- Frontend: Next.js 14 App Router, React, Tailwind, TypeScript strict
- Frontend editing env: Replit (existing project)
- Backend: Supabase (Postgres + auth + realtime)
- Payments: Stripe
- Data: OpenDota API + Stratz GraphQL + Skadi Clarity parser
- Live state: Valve GSI (Game State Integration)
- Custom games: Lua via Workshop Tools
- AI: claude-sonnet-4-20250514 via /v1/messages

## Legal boundaries (non-negotiable)
- Replay analysis (always)
- GSI in unranked/bot/custom (Valve-sanctioned)
- GSI in ranked -> auto-disable on match_type detect
- Memory reading, injection, auto-input -> never

## Code rules
- TypeScript strict
- Server components default, client opt-in
- Zod schemas for every external payload
- Error boundaries on every API call
- File size <500 lines — split if larger
- No comments that just restate code; only why-comments
- One responsibility per module

## Style
Dark theme. Colors: `#0a0d14` bg, `#c8aa6e` gold, `#b8282d` Dire red, `#3fb950` safe green. Fonts: Cinzel, Rubik, JetBrains Mono. Tone: direct, Dota-native slang, use "brat" naturally.

## Team terminology
- LUCKER23 = Yuriy (me, builder)
- NONEK = brand face, pro player
- CHILLZER = coach, first B2B customer
- Company: **YK Nanotech Trading s.r.o.** (NOT DLYK — that's stale)

## Validation loop (every feature)
1. Lint: `npm run lint`
2. Typecheck: `npm run typecheck`
3. Unit tests: `npm test`
4. E2E: `npm run test:e2e`
Every feature PRP must include these gates.

## When unsure
Ask LUCKER23. Do not invent stack choices. Do not pick NONEK or CHILLZER names for features without confirming.
