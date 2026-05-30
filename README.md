# news-feed-agent

Serverless AI agent that delivers a personalised daily industry news digest to Gmail every morning at 7am AEST.

## Architecture

- **AWS Lambda** (Python 3.12) — agentic loop with Anthropic Claude
- **EventBridge** — cron trigger, 7am AEST daily
- **AWS SES** — HTML email delivery to Gmail
- **S3** — digest archive + context profile
- **Serper API** — Google Search
- **GitHub Actions** — deploy on push to main

## Deployment

Push to `main` → GitHub Actions zips `lambda_agent.py` → deploys to AWS Lambda automatically.

Required GitHub secrets:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

## Context profile

The agent's context profile (`context.md`) lives in S3 at `s3://2026-practices-agents/News-Agent/context.md`.
It is intentionally excluded from this repo (contains personal data). Update it directly in S3.

## Local structure

```
lambda_agent.py          ← agent loop (deployed to Lambda)
.github/workflows/
  deploy.yml             ← GitHub Actions deploy on push to main
.gitignore               ← excludes context.md, secrets
README.md
```
