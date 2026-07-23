# jtbf-scrape-runner

Scheduled trigger repo for [JTBF](https://jtbf.pages.dev)'s scraper pipeline.

This repo is intentionally empty of application code. It exists so the recurring
scheduled jobs (scrape, feed-corpus rebuild, description backlog drain) run on
**unmetered GitHub Actions minutes** — standard runners are free and unlimited on
public repos, whereas the private repo those jobs pull from has a capped free
tier that a chronic 24/7 cron schedule was exceeding.

Every workflow here checks out the private pipeline repo at run time via a
repo-scoped deploy key (write access only, cannot touch any other repo), runs
the same scrape/build/backfill logic that repo already has, and pushes state
back the same way. No scraper source, ATS endpoint, or company-specific
technique lives in this repo — only generic workflow orchestration.
