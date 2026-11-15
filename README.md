# Mercato CRM template

A ready Open Mercato app made from the CRM starter preset. Use it as the starting point for a CRM: companies, people, deals, pipelines, activities and email channels.

It was created with `create-mercato-app@0.9.0 --preset crm`. It differs from the stock preset in this README, the licence, the package metadata and one module line.

The template enables the `api_keys` module. The stock 0.9.0 CRM preset cannot initialize without it: the `auth` module needs the `ApiKey` entity, and `yarn initialize` stops with `Metadata for entity ApiKey not found`.

## Open Mercato version

Open Mercato 0.9.0. Every `@open-mercato/*` package in `package.json` is pinned to `0.9.0`. Node 24 or newer and Yarn 4 are required.

## What is inside

Modules enabled in `src/modules.ts`:

| Area | Modules |
| --- | --- |
| CRM | `customers` |
| Communication | `messages`, `communication_channels`, `channel_imap`, `channel_gmail`, `notifications` |
| Platform | `auth`, `api_keys`, `directory`, `configs`, `entities`, `query_index`, `audit_logs`, `attachments`, `dictionaries`, `currencies`, `feature_toggles`, `progress`, `integrations` |
| Tools | `dashboards`, `search`, `events`, `api_docs`, `ai_assistant` |

The scaffold also ships the source of four example modules in `src/modules/` (`example`, `example_customers_sync`, `ratelimit_probe`, `agent_examples`). The CRM preset does not enable them by default. `agent_examples` and five modules of `@open-mercato/enterprise` (`record_locks`, `system_status_overlays`, `sso`, `security`, `agent_orchestrator`) turn on only with the `OM_ENABLE_ENTERPRISE_MODULES` flags in `.env`.

## Demo data

`yarn initialize` seeds demo data. The data is not in this repository. It comes from the `customers` module of `@open-mercato/core@0.9.0`:

- Three fictional companies: Brightside Solar, Harborview Analytics and Copperleaf Design Co.
- Six fictional people, two per company, with addresses on `brightsidesolar.com`, `harborviewanalytics.com` and `copperleaf.design`.
- Deals, activities, interactions and notes for these companies, a default sales pipeline and the CRM dictionaries.
- The demo accounts `superadmin@acme.com`, `admin@acme.com` and `employee@acme.com`.

The companies and people are invented by Open Mercato, but the domains are ordinary internet domains and two of them are registered. Do not send email to these addresses. Run `yarn mercato init --no-examples` instead of `yarn initialize` to start without the demo companies and people.

## Create an app from this template

```bash
npx create-mercato-app my-crm --template wojciechszyjka/mercato-crm-template
```

A `create-mercato-app` without `--template` (0.9.0 and older) takes the repository address:

```bash
npx create-mercato-app my-crm --app-url https://github.com/wojciechszyjka/mercato-crm-template
```

## Run it

The app needs PostgreSQL. `docker-compose.yml` starts PostgreSQL, Redis and the other local services.

Quick start:

```bash
yarn setup
```

`yarn setup` copies `.env.example` to `.env` if needed, installs dependencies, migrates, initializes and starts the dev server.

Manual steps:

```bash
cp .env.example .env
# Edit .env with your database credentials.
yarn install
yarn generate
yarn db:migrate
yarn initialize
yarn dev
```

With Docker, after `cp .env.example .env && yarn install`:

```bash
docker compose -f docker-compose.fullapp.dev.yml up --build
```

The app listens on http://localhost:3000. Sign in at `/login`.

## Checks

```bash
yarn typecheck
yarn lint
yarn build
```

## Licence

MIT. See [LICENSE](LICENSE). The Open Mercato packages this app depends on carry their own licences.
