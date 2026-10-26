## ADDED Requirements

### Requirement: Superseded by Odoo
The project catalog SHALL be managed in Odoo (`razs_jobs`) and served by `portfolio-api` at `GET https://projects.razs.dev/portfolio` (projects also at `GET /`). `projects.json` in this repository SHALL be treated as retired, read-only history and SHALL NOT be edited or consumed at runtime.

#### Scenario: Repository retired
- **WHEN** the retirement is complete
- **THEN** the repository README states it is retired and points to Odoo, and the repository is archived with its history intact

#### Scenario: No runtime consumer
- **WHEN** `portfolio-api` and `my-portfolio` are searched for `portfolio-data` or its raw GitHub URL
- **THEN** there are no matches
