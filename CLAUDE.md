# CLAUDE.md — portfolio-data

## Purpose

This repo contains a single file, `projects.json`, which is the source of
truth for the projects shown on my portfolio (https://razs.dev). It is
fetched live by `portfolio-api` (a separate service running on my Mac
server) and cached for ~5 minutes before serving it to the frontend.

Because of this, **every edit here goes live on my public portfolio within
minutes**. Treat this file with the same care as production code, not as a
scratch config.

## Non-negotiable rules

1. **English only.** Every text field — `title`, `subtitle`, `tech`,
   `description`, and any future text field — must be written in English,
   regardless of what language we're using in conversation. Never mix
   languages within a field.

2. **No dirty comments or leftover scaffolding.** JSON doesn't support
   comments natively, so never introduce `// TODO`, placeholder text like
   `"description": "TODO"`, half-finished entries, or debug fields. If an
   entry isn't ready, don't add it — propose it in chat first instead of
   committing a draft.

3. **Never leak secrets.** Never copy real IPs, internal hostnames, tunnel
   IDs, credentials, API keys, environment variable values, absolute
   filesystem paths, or usernames into this file — even inside a
   `description`. If a project's description would naturally reference
   infrastructure details, describe them in general terms
   (e.g. "exposed via a reverse tunnel with per-service subdomains") rather
   than exact values. When unsure whether something is sensitive, leave it
   out and ask.

4. **Keep existing entries accurate and up to date.** Don't just append new
   projects — when asked to update the list, check whether any existing
   entry's `description`, `tech`, `github`, `demo`, or `appstore` link is
   stale (renamed repo, changed URL, deprecated project, updated stack) and
   fix it. Don't delete or rewrite an entry's `id` without being told to —
   the frontend and any external references may depend on it.

## Required schema

Every object in the `projects.json` array must have exactly this shape.
Fields marked optional can be omitted entirely (don't include them as
empty strings or `null`).

```json
{
  "id": "kebab-case-unique-slug",
  "category": "data | web | odoo | software | blockchain",
  "priority": 0,
  "title": "Project Name",
  "subtitle": "One-line description of what it is",
  "tech": "Tech · Stack · Separated · By · Middle Dots (·)",
  "description": "1-3 sentences in English, in complete sentences, no trailing whitespace.",
  "github": "https://github.com/... (optional)",
  "demo": "https://... (optional, live demo/deployment URL)",
  "appstore": "https://... (optional, for Odoo App Store listings)"
}
```

Rules for each field:

- `id`: lowercase, kebab-case, unique across the whole file. Once set,
  don't change it unless explicitly asked — it may be referenced elsewhere.
- `category`: must be one of the five existing values. If a new project
  doesn't fit any of them, flag it in chat before inventing a new category
  — adding one also requires updating `CATEGORIES` in the portfolio's
  `Projects.jsx` (a separate repo), so it's a two-repo change, not just this
  file.
- `priority`: integer, higher = shown first. New entries should get a
  priority that reflects where they logically rank against existing ones —
  don't default to 0 or 100 without thinking about ordering.
- `tech`: use the middle-dot separator (`·`) to match existing entries,
  not commas or pipes.
- `description`: written in English, professional tone, factually accurate
  to what the project actually does — don't embellish capabilities it
  doesn't have.
- `github` / `demo` / `appstore`: only include if the link is real and
  currently reachable. Don't include a placeholder or a link you haven't
  verified.

## Validation before committing

Always validate the JSON is well-formed before committing:

```bash
python3 -m json.tool projects.json > /dev/null && echo "Valid JSON"
```

## Commit conventions

- Commit messages in English, present tense, descriptive
  (e.g. `"Add QuantLab v2 backtesting engine entry"`, not `"update"`).
- Never commit directly without validating the JSON first.
- Push to `origin main` (or `master`, check `git branch` — this repo may
  still be on the legacy default) after committing; `portfolio-api` picks
  up changes automatically via its cache refresh, no server restart needed.
