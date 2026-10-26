## Why

`projects.json` (lines 294-302) lists "CV Download API" (`id: web-cv-download`) with a demo link to `https://cv-api.razs.dev/cv`. That service is being retired (`retire-cv-download-api`), so the demo link would 404.

## What Changes

**Owner decision: keep the project entry, remove only its obsolete demo link.**

- Delete the `"demo": "https://cv-api.razs.dev/cv"` key from the `web-cv-download` object (and the trailing comma on the line before it). Everything else in the entry, including `github`, stays.
- `portfolio-api` re-reads `projects.json` from GitHub raw (`master`) with a 5-minute cache, so the change shows up within about 5 minutes of the merge; no restart is needed.

## Owner decisions

- The API key is permanent; `job.profile` 14 in Odoo is the single source of truth for the CV.
- No observation period: `cv_download` is retired right after end-to-end verification.
- Hosting of the frontend is Vercel (auto-deploys on push to the default branch).

## Capabilities

### New Capabilities
- `project-catalog`: the catalog must not advertise dead demo links.

### Modified Capabilities
None.

## Impact

- `projects.json` only. Merged to `master` (the API's source) after the frontend is verified, and before `cv-api` is stopped.

## Out of scope

- Other entries, ordering, wording of the kept entry, or a new entry for the Odoo CV endpoint.
