# project-catalog Specification

## Purpose
Retired catalog of portfolio projects (projects.json); superseded by Odoo `razs_jobs` and served by portfolio-api at /portfolio.

## Requirements

### Requirement: No dead demo links
Every `demo` URL in `projects.json` SHALL resolve to a live service. The `web-cv-download` entry SHALL be kept but SHALL have no `demo` link before `cv-api.razs.dev` is stopped.

#### Scenario: Entry kept without demo
- **WHEN** the change is applied
- **THEN** `projects.json` is valid JSON, the `web-cv-download` entry exists with no `demo` key, and `https://projects.razs.dev/` returns it without `demo` after the cache refresh

### Requirement: Superseded by Odoo
The project catalog SHALL be managed in Odoo (`razs_jobs`) and served by `portfolio-api` at `GET https://projects.razs.dev/portfolio` (projects also at `GET /`). `projects.json` in this repository SHALL be treated as retired, read-only history and SHALL NOT be edited or consumed at runtime.

#### Scenario: Repository retired
- **WHEN** the retirement is complete
- **THEN** the repository README states it is retired and points to Odoo, and the repository is archived with its history intact

#### Scenario: No runtime consumer
- **WHEN** `portfolio-api` and `my-portfolio` are searched for `portfolio-data` or its raw GitHub URL
- **THEN** there are no matches
