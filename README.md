# CivicConnect – Smart Public Issue Reporting and Resolution Platform

React 18 + Vite + React Router + Axios + Bootstrap 5. Citizens report civic issues, admins assign them to departments, officers resolve them.

## Run
```bash
npm install
npm run dev      # http://localhost:5173
```
Demo logins: `admin@civic.test / admin123`, `officer@civic.test / officer123`, `citizen@civic.test / citizen123`.

## Mock API (important)
By default the app uses `src/api/mockServer.js`, a **browser-only mock** (data in localStorage, SHA-256 hashing, fake token). It is **not a production backend** and offers no real security.
To use a real Java backend: copy `.env.example` to `.env`, set `VITE_USE_MOCK=false` and `VITE_API_URL`, and implement the endpoints listed in `src/api/config.js`. Components do not change; only the Axios adapter is swapped.

## Structure
`api/` config, Axios client + interceptors, mock server · `services/` one function per endpoint · `context/` auth · `hooks/useFetch` · `components/` shared UI · `pages/` screens · `layouts/` shell · `database/schema.sql` MySQL schema.

## Endpoints
POST /auth/register, /auth/login · GET/POST /complaints · GET/PUT/DELETE /complaints/{id} · PATCH /complaints/{id}/status · GET/POST /departments · GET /users, /users/{id} · GET /analytics/dashboard

## Backend must enforce
BCrypt password hashes, JWT validation and expiry, role checks on every endpoint (frontend route guards are only UX), file type/size validation, input validation.

## Deploy
`npm run build`, then upload `dist/` to Netlify/Vercel (add an SPA fallback to `index.html`).
