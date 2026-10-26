## 1. Gate

- [x] 1.1 razs_jobs import parity check passed (owner reviewed)
- [x] 1.2 portfolio-api `/portfolio` deployed and verified in production
- [x] 1.3 my-portfolio production parity verified
- [x] 1.4 Re-grep for consumers of portfolio-data; none besides the removed `SOURCE_URL`

## 2. Retire

- [x] 2.1 Mark the project-catalog spec superseded by Odoo (apply this change's delta)
- [x] 2.2 Add the README retirement notice
- [x] 2.3 Final commit merged to `master` with owner approval
- [x] 2.4 `gh repo archive RAZermenoSaracho/portfolio-data`; history kept
- [x] 2.5 Confirm `isArchived` is true and `https://projects.razs.dev/` and `/portfolio` still respond

## 3. Rollback (only if needed)

- [x] 3.1 (Not triggered: parity passed, no rollback needed.) Reverse order: revert my-portfolio first; then `gh repo unarchive` (if archived) and revert portfolio-api to restore `SOURCE_URL`; razs_jobs fields can stay (`is_public=False` if needed)
