## 1. Decide (owner)

- [x] 1.1 Owner chose: keep the entry, remove only the demo link

## 2. Edit

- [x] 2.1 Remove the `demo` key from the `web-cv-download` object (lines 294-302) and the trailing comma before it
- [x] 2.2 `node -e "JSON.parse(require('fs').readFileSync('projects.json'))"` passes

## 3. Publish and verify

- [ ] 3.1 Merge to `master` after the frontend is verified in production, before `pm2 stop cv-download-api`
- [ ] 3.2 Within about 5 minutes `curl -s https://projects.razs.dev/` reflects the change
