# project-catalog Specification

## Purpose
Defines how portfolio projects are listed in projects.json, the data served by portfolio-api.

## Requirements

### Requirement: No dead demo links
Every `demo` URL in `projects.json` SHALL resolve to a live service. The `web-cv-download` entry SHALL be kept but SHALL have no `demo` link before `cv-api.razs.dev` is stopped.

#### Scenario: Entry kept without demo
- **WHEN** the change is applied
- **THEN** `projects.json` is valid JSON, the `web-cv-download` entry exists with no `demo` key, and `https://projects.razs.dev/` returns it without `demo` after the cache refresh
