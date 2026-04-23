## FEATURE

Build MVP v1 of the Dota AI Coach — the B2C chat coach tier.

User flow:
1. Player signs up with Steam OAuth → we import their last 50 matches from OpenDota.
2. Player pastes a match ID OR picks from their recent matches.
3. Coach chat opens. Claude has the match context loaded (heroes, build, timing of events, deaths, GPM/XPM).
4. Player asks questions like "why did I lose lane?" or "what should I have built instead of Daedalus?"
5. Coach replies in Dota-native slang, 2–4 sentences, references specific timestamps.

Must include:
- Steam OAuth (via Supabase Auth + Steam OpenID provider)
- OpenDota match ingestion job (queue, stores parsed match in Postgres)
- Match selector UI (grid of last 50 matches with win/loss color)
- Chat UI (streaming Claude responses)
- Rate limiting (10 messages per hour free tier, unlimited paid)
- Stripe checkout for $9.99/mo paid tier

## EXAMPLES

See `examples/` folder:
- `examples/opendota-fetch.ts` — pattern for OpenDota API calls with rate limit handling
- `examples/claude-stream.ts` — how to stream Claude responses via Vercel AI SDK
- `examples/supabase-rls.sql` — row-level security policies for user data
- `examples/coach-prompt.md` — system prompt with Dota lingo rules
- `examples/match-context-builder.ts` — how to compress a parsed match into ~2k tokens

## DOCUMENTATION

- OpenDota API: https://docs.opendota.com/
- Stratz GraphQL: https://stratz.com/api
- Skadi Clarity (Java replay parser): https://github.com/skadistats/clarity
- OpenDota parser (Node, easier): https://github.com/odota/parser
- Valve GSI (for phase 2): https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Game_State_Integration
- Supabase Steam OpenID: https://supabase.com/docs/guides/auth/social-login
- Vercel AI SDK: https://sdk.vercel.ai/docs
- Anthropic Messages API: https://docs.anthropic.com/en/api/messages

## OTHER CONSIDERATIONS

Gotchas:
- OpenDota free tier: 2000 requests/day, rate limit 60/min. Cache aggressively.
- Steam OpenID returns SteamID64, need to convert to Dota account_id (SteamID64 - 76561197960265728).
- Parsed replays can be 50MB+ — never send full replay to Claude. Build a match-context summary (~2k tokens) first.
- Hero names: use Dota's internal names (`npc_dota_hero_nevermore`) in DB, display names (`Shadow Fiend`) in UI.
- OpenDota parses replays on-demand — first parse can take 1-5 min. Show loading state.
- Claude Sonnet 4 model ID: `claude-sonnet-4-20250514` (not `claude-sonnet-4-5-20250514`, different model).
- NEVER store Steam auth tokens longer than session. We only need SteamID permanently.
