# Hospital IT Asset Management

**Internship portfolio · 8 June–12 October 2026 · Full-stack development**

A web application for hospital IT teams to manage printer assets, contracts, monthly meter readings, imports and fiscal-year expense reporting.

**My role:** Primary developer responsible for the end-to-end internship project, from application development and testing to technical documentation and delivery, under mentor supervision. This repository preserves the original contributors' authorship and credits the [source project](https://github.com/saritrungj/suth-helpdesk-assets).

**ผู้พัฒนา:** [WayuOHm99](https://github.com/WayuOHm99) · **ช่วงฝึกงาน:** 8 มิถุนายน–12 ตุลาคม 2026

รับผิดชอบการพัฒนาระบบครบวงจรภายใต้การดูแลของพี่เลี้ยง รายละเอียดผลงานและหลักฐานอยู่ใน [กรณีศึกษาจากงานจริง](docs/portfolio/README.md)

## Engineering highlights

| Work | Engineering focus | Evidence |
|---|---|---|
| Unified analytics dashboard | Consistent filters across KPIs, charts, tables and exports; URL state | [PR #127](https://github.com/saritrungj/suth-helpdesk-assets/pull/127) |
| Import preview and confirmation | Review planned changes before committing business data | [PR #210](https://github.com/saritrungj/suth-helpdesk-assets/pull/210) |
| Thai CSV compatibility | UTF-8, UTF-16 and Windows-874 decoding; invalid-input handling | [PR #234](https://github.com/saritrungj/suth-helpdesk-assets/pull/234) |
| Accessibility verification | Route/state coverage across themes and viewport sizes | [PR #293](https://github.com/saritrungj/suth-helpdesk-assets/pull/293) |
| Expense and re-import regression tests | Verify price changes and prevent duplicate readings | [PR #328](https://github.com/saritrungj/suth-helpdesk-assets/pull/328) |

The case studies distinguish historical PR evidence from checks performed on this portfolio copy. They do not claim that the full application was re-tested during the repository transfer.

## Technology

- **Frontend:** Vue 3, Vite, Tailwind CSS v4, TanStack Query, Reka UI and Lightweight Charts.
- **Backend:** Node.js, Express, MySQL, zod validation and JWT sessions in httpOnly cookies.
- **Shared domain:** Fiscal-year, date, currency and localization logic in packages/domain.
- **Verification:** Node.js tests, Vitest, Playwright, axe and isolated MySQL QA checks.

The browser calls the Express HTTP API, which applies authorization and business rules before accessing MySQL. The web client and API reuse packages/domain. Details are maintained in the [architecture guide](docs/explanation/architecture.md) and [domain guide](docs/explanation/domain.md).

## Run locally

Requirements: Node.js 20+, npm and MySQL 8.4 or Docker Desktop. Follow the [development setup](docs/how-to/set-up-development.md) and [Docker development database guide](docs/how-to/run-docker-database.md) to create your own environment and sample data.

    npm install
    npm run dev:api
    # In a second terminal:
    npm run dev:web

Use synthetic data for demonstrations. This repository contains no working production environment or database backup. Screenshots and a hosted demo have not been prepared for this copy.

## Documentation and continued development

- [Portfolio case studies and interview talking points](docs/portfolio/README.md).
- [Project documentation index](docs/README.md).
- [Verification guide](docs/how-to/verify-changes.md).
- [Personal repository issue tracker](https://github.com/WayuOHm99/suth-helpdesk-assets-portfolio/issues).
- [Repository contribution workflow](CONTRIBUTING.md).

Deployment records inherited from the source describe that source system, rather than a deployment of this personal repository.

## Provenance and license

This is an independent personal portfolio copy of [saritrungj/suth-helpdesk-assets](https://github.com/saritrungj/suth-helpdesk-assets), prepared on 12 October 2026. Original contributor names, documentation and the [Apache License 2.0 text](LICENSE) are retained.

Historical backend/.env and the raw docs/meter-import-source.xlsx were removed from this copy's Git history before upload. Original commit IDs can therefore differ; the linked source PRs remain the references for historical work. The original local archive is kept separately and is not uploaded here.
