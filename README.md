# Odyssey Studio

An interactive web app to practise the **value curve**, the core tool of HEC Paris' course *Reinventing Your Business Model (Odyssey 3.14)*.

- **Explore** eight cases (four from the textbook, one student analysis, three built from course concepts).
- **Practice**: predict a curve, then reveal the course's reading and get scored.
- **Build** your own curve with a live, rule-based coach, plus an optional AI second opinion from **Gemini**.

A student project built on the course framework and cases. Not an official HEC tool.

## Structure

```
index.html        the whole front end (no build step)
api/ai.js         Vercel serverless function that calls Gemini
api/_course.js    the course frame sent to Gemini (rules, 14 directions, textbook curves)
```

The browser never sees the API key. It sends only the company facts and the curve to `/api/ai`; the prompts are built on the server, so the endpoint cannot be used as a free general-purpose Gemini proxy. The function also accepts same-origin requests only and rate-limits each IP (best effort).

## Deploy on Vercel

1. Import this repository in Vercel (framework preset: **Other**, no build command, no output directory).
2. In **Settings → Environment Variables** add:
   - `GEMINI_API_KEY` — your key from Google AI Studio (required)
   - `GEMINI_MODEL` — optional (default: `gemini-3.6-flash`, then `gemini-2.5-flash`, then `gemini-flash-latest`)
   - `AI_RATE_LIMIT` — optional, requests per IP every 10 minutes (default `12`)
3. Redeploy so the variables take effect, then add your domain in **Settings → Domains**.

## Run locally

```
npm i -g vercel
vercel dev
```

Put `GEMINI_API_KEY=...` in a `.env.local` file (already git-ignored).
