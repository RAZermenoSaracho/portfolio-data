## Why

Projects (and the rest of the portfolio) now live in Odoo `razs_jobs` and are served by `portfolio-api` `/portfolio`. `projects.json` here becomes a stale second source of truth that could be edited by mistake. Retire the repo once nothing depends on it.

## What Changes

- Mark the `project-catalog` spec as superseded by Odoo.
- Add a README notice pointing to Odoo as the source and to `https://projects.razs.dev/portfolio`.
- Final commit, then `gh repo archive RAZermenoSaracho/portfolio-data`. History is kept (archive, not delete).

## Gate (all must be verified first)

1. razs_jobs import parity check (29 projects) passed and owner reviewed.
2. `portfolio-api` `/portfolio` (and `/` derived from it) deployed and verified.
3. `my-portfolio` production parity verified (`render-from-portfolio-api`).

Cross-repo order: razs_jobs deploy, import dry-run/review/apply with backup, portfolio-api, my-portfolio, parity verified, then this change.

## Consumers

Exploration grep found no runtime consumer other than `portfolio-api`'s `SOURCE_URL`, which `serve-portfolio-from-odoo` removes. Re-grep (`portfolio-data`, `raw.githubusercontent.com/RAZermenoSaracho/portfolio-data`) across `/Users/razs/production` and `my-portfolio` immediately before archiving.

## Rollback

Rollback runs in reverse order: (1) revert my-portfolio first; (2) then revert portfolio-api, which restores `SOURCE_URL` and requires portfolio-data to be unarchived (if already archived, run `gh repo unarchive RAZermenoSaracho/portfolio-data` first); (3) the razs_jobs fields can stay, set `is_public=False` if needed.

Here this means: `gh repo unarchive` first if needed. `projects.json` is unchanged, so the old behavior returns.

## Capabilities

### Modified Capabilities
- `project-catalog`: adds a requirement declaring it superseded by Odoo (delta uses ADDED; existing requirements are untouched).

## Impact

Docs only plus one archive action. No data is deleted.
