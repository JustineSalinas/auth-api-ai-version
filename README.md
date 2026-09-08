# Auth API (AI Rematch)

This is the Stage 7 bonus for the Auth assignment: the same API, generated
from a written-from-memory prompt (see [PROMPT.md](PROMPT.md)) instead of
built by hand. It's tested against the same Supabase project as
[`auth-api`](https://github.com/JustineSalinas/auth-api) so the comparison
is apples to apples. Findings live in that repo's README under "AI vs me" —
this folder is just the generated code and the record of what was actually
tested.

## Setup

Same as the hand-built version: `cp .env.example .env`, fill in your
Supabase URL/anon key, `npm install`, `npm start`.

## What was actually tested against this code

- `POST /auth/signup` / `POST /auth/login` against a real Supabase project — 201 / 200, correct
- `GET /protected/profile` with a valid token — 200 with real user data
- Same route with a tampered token — 401, correct
- `POST /auth/logout` with a valid token — 204, correct
- `GET /protected/profile` with `Authorization: Basic <valid-token>` (wrong scheme) — **200, incorrectly authenticated**
- `POST /auth/signup` with no request body at all — **500 with a leaked stack trace**, instead of 400

See the main repo's README for the full analysis.
