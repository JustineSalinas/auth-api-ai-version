This is the exact prompt written from memory (per Stage 7 of the assignment)
and given to a fresh AI assistant with no access to the hand-built
`auth-api` code, to generate an independent second implementation for
comparison.

---

Build a Node.js + Express REST API secured with Supabase Auth. Use the
`@supabase/supabase-js` SDK and a `.env` file for `SUPABASE_URL`,
`SUPABASE_KEY`, and `PORT`.

Routes:
- `POST /auth/signup` — body `{ email, password }`. Calls
  `supabase.auth.signUp()`. Missing fields -> 400. Success -> 201 with the
  user object.
- `POST /auth/login` — body `{ email, password }`. Calls
  `supabase.auth.signInWithPassword()`. Missing fields -> 400. Wrong
  credentials -> 401 with `{ "error": "Invalid login credentials" }`.
  Success -> 200 with the access token and refresh token.
- `POST /auth/logout` — protected. Calls `supabase.auth.signOut()`.
  Success -> 204.
- `GET /public/info` — no auth. Returns
  `{ "message": "Welcome stranger! This info is public." }`.
- `GET /protected/profile` — protected. Returns the user's id, email, and
  created_at.

Protected routes must read the token from an `Authorization: Bearer <token>`
header, verify it with `supabase.auth.getUser(token)`, and return 401 with
a clear error if the header is missing, malformed, or the token is invalid
or expired. Extract this check into reusable Express middleware rather than
repeating it per route.

Also add Swagger UI at `/docs` with a bearer-token security scheme, so
protected routes show a lock icon and can be tested with an "Authorize"
button.

---
