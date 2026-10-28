# EtlabPro: verification and operations

Reviewed against [default-branch commit f382f01ec5b3](https://github.com/noel-ult/EtlabPro/commit/f382f01ec5b365f1b6be3aa3a8c238581ad3ad2b) on 2026-10-28. Start with the [developer guide](PROJECT_GUIDE.md) for installation and architecture, and the [source reference](REFERENCE.md) for exact scripts, configuration readers, routes, and source locations.

## Student synchronization

With an authorized test account, verify login, token refresh, sync, cached/offline rendering, and expired-token behavior. Compare scraper results when ETLAB markup changes.

These are acceptance scenarios for a maintainer to run in the documented environment. Their inclusion is not a claim that live integrations or production credentials were tested during this documentation update.

## Deployment and failure diagnosis

Keep JWT_SECRET stable across workers/restarts and service-role credentials on the backend. Public /health checks process health; verify student sync separately.

## Maintaining the contract

When behavior changes, update the guide and examples in the same PR. Check the entry point and working directory before copying commands. Use the linked source readers to distinguish build-time configuration from process environment. For failures, capture the first application error, runtime version, selected mode, and redacted configuration names before later proxy or port errors.

Keep changes tied to evidence: a declared command is not proof it passes, a process health response is not a successful end-to-end workflow, and a historical report describes its own revision. Record actual check results and any unavailable external services in the PR.
