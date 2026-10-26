## Decisions

- **Archive, don't delete or empty.** Read-only archive keeps history and makes rollback one command. `projects.json` stays untouched so the rollback is exact.
- **Spec stays, marked superseded.** The spec documents the former contract and the dead-demo-link rule; it gets a requirement stating that Odoo is now the source, rather than being removed (OpenSpec archive of this change applies the delta).
- **Order is a hard gate.** Archiving earlier would break `portfolio-api` `/` (still fetching `SOURCE_URL`) only if the archived repo stopped serving raw files; archived repos still serve raw content, but the gate keeps rollback trivial and avoids confusion about which source is live.
- **No Cloudflare, Vercel or Odoo action** is part of this change.

## Steps

1. Verify the gate and re-grep consumers.
2. Commit spec delta applied (superseded notice).
3. Commit README notice (top of file): "Retired. Portfolio content is managed in Odoo (razs_jobs) and served at https://projects.razs.dev/portfolio. This repo is archived for history."
4. Merge to `master` (owner approval), then `gh repo archive RAZermenoSaracho/portfolio-data --yes`.
5. Confirm `gh repo view --json isArchived`.
