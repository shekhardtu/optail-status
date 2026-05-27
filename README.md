# Optail Status

Uptime monitoring + incident history for [Optail](https://github.com/shekhardtu/optail) — the open-source provider-failover-first transactional email platform.

Probed every 5 minutes by GitHub Actions. Status page auto-generated at https://shekhardtu.github.io/optail-status (or `status.optail.io` once the CNAME is set up).

## What's monitored

| Endpoint | What it covers |
|---|---|
| `https://api.optail.io/health` | The REST API customers hit |
| `https://app.optail.io/` | The dashboard SPA |
| `https://optail.io/` | The landing + docs site |
| `https://webhooks.optail.io/health` | The provider webhook ingester (SendGrid/Postmark/Mailgun/SES) |

Edit `.upptimerc.yml` and open a PR to add or change monitors.

## How it works

- `.github/workflows/uptime.yml` runs every 5 minutes, probes each `sites[].url` from `.upptimerc.yml`.
- Failed probes auto-open a GitHub Issue in this repo. Title pattern: `🟥 <site name> is down`.
- When the next probe succeeds, the issue auto-closes. The open/close pair becomes the incident record.
- Response-time history is stored as commits under `history/`, response-time graphs under `graphs/`. Both regenerate daily.

## Setup checklist (one-time)

The setup happens partly here and partly in `Settings →` panels GitHub Actions can't reach via API:

- [ ] **Personal Access Token** at `Settings → Developer settings → Personal access tokens → Tokens (classic)`. Scopes: `repo` + `workflow`. Add it to this repo's secrets as `GH_PAT` (Settings → Secrets and variables → Actions → New repository secret).
- [ ] **GitHub Pages** at `Settings → Pages`. Source: "Deploy from a branch" → Branch: `gh-pages` → `/` (root). Wait for the first Pages build to finish (~2 min) before checking the URL.
- [ ] **(Optional) Custom domain** — point `status.optail.io` CNAME at `shekhardtu.github.io`. Then flip `baseUrl` → `cname` in `.upptimerc.yml`.
- [ ] **Trigger the setup workflow** at `Actions → Setup CI → Run workflow`. This bootstraps the cron + initial probe history.

## Related

- [Optail main repo](https://github.com/shekhardtu/optail)
- [Operations runbook](https://github.com/shekhardtu/optail/blob/main/docs/operations/uptime.md)
- [Upptime](https://upptime.js.org) — the open-source uptime monitor this is built on
