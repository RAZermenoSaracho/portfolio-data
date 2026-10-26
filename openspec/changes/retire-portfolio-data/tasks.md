## 1. Gate

- [ ] 1.1 razs_jobs import parity check passed (owner reviewed)
- [ ] 1.2 portfolio-api `/portfolio` deployed and verified in production
- [ ] 1.3 my-portfolio production parity verified
- [ ] 1.4 Re-grep for consumers of portfolio-data; none besides the removed `SOURCE_URL`

## 2. Retire

- [ ] 2.1 Mark the project-catalog spec superseded by Odoo (apply this change's delta)
- [ ] 2.2 Add the README retirement notice
- [ ] 2.3 Final commit merged to `master` with owner approval
- [ ] 2.4 `gh repo archive RAZermenoSaracho/portfolio-data`; history kept
- [ ] 2.5 Confirm `isArchived` is true and `https://projects.razs.dev/` and `/portfolio` still respond

## 3. Rollback (only if needed)

- [ ] 3.1 `gh repo unarchive`, then restore `SOURCE_URL` in portfolio-api and redeploy
