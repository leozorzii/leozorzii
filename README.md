<div align="center">

<img src="assets/header.svg" width="100%" alt="Leonardo Zorzi - AI Engineer, Full Stack, Security-minded backend" />

</div>

I build production systems where the hard parts are trust boundaries: who is allowed to do what, what happens to the data at rest, what an LLM is allowed to see and spend, and how a change reaches production without breaking it.

Currently at **Agrocash** (agribusiness finance platform) and working on internal and real estate platforms. Information Systems at UFN, Brazil.

---

## What I solve in real projects

| Area | What I actually build |
| --- | --- |
| **AI engineering** | LLM features behind a provider abstraction (real and fake provider for tests), tool calling with per-assistant tool allowlists, structured extraction, audio and image transcription, natural-language search, versioned prompts |
| **LLM guardrails** | Moderation before chat, prompt-injection detection with an audit table, PII masking (CPF, email, phone) before data reaches the model, per-hour rate limits and a daily spend ceiling reserved atomically in SQL |
| **Authentication** | Supabase Auth and JWT flows, invite-only onboarding, forced password change, session revocation on password change or deactivation, httpOnly cookie sessions with `token_version` invalidation, server-side Turnstile validation |
| **Authorization** | Role and module-based access, tenant and subscriber scoping, row-level ownership checks, tests that assert every route declares its guard, read-only "view as user" impersonation with a short-lived token |
| **Data security** | Postgres RLS on every table (hundreds of policies), `SECURITY DEFINER` helpers, append-only audit timelines, revoked `TRUNCATE`, AES-256-GCM encrypted vault, Fernet-encrypted integration credentials |
| **HTTP hardening** | Strict CSP, HSTS, tiered rate limiting, CORS allowlists, body size limits, no internal errors in responses, secrets only in backend env |
| **Deploy and CI/CD** | GitHub Actions with QA and production environments, manual production dispatch with approval, OIDC to AWS (no static keys), Docker images, migrations applied by pipeline, smoke tests after deploy |
| **Quality gates** | Trivy, CodeQL, Gitleaks, Bandit, `npm audit`, Dependabot, schema drift checks, generated-types checks, mypy, ruff, Vitest, Pytest, Playwright, actions pinned by commit SHA |
| **AI in the workflow** | LLM PR-review agents with secret redaction before the diff leaves CI, AI-generated release notes and changelog PRs, spec-driven changes with OpenSpec |

---

## Selected work

<details open>
<summary><b>Habita - real estate platform with AI features</b> (Python, FastAPI, React, Supabase)</summary>

<br />

- **AI layer:** provider protocol with OpenAI adapter and a fake provider, so tests and E2E never call the LLM. 15 versioned prompts, assistants (listing copy, sales arguments, contracts), lead scoring and summaries, smart property search with filter extraction and ranking.
- **Cost and safety:** hourly rate limit and a daily spend ceiling reserved atomically in the database, audio and image caps, injection detection with audit logging, PII masking.
- **Isolation:** tenant isolation through RLS with SQL tests against real Postgres (anonymous visibility, public showcase leaks, lead flows). Admin "view as user" uses a 30-minute JWT with an impersonation claim; the database and an ASGI middleware both refuse writes.
- **Integrations:** job-based importer with a standalone worker and Fernet-encrypted credentials; resilient CEP lookup with fallback providers and cache.
- **Delivery:** QA on push, production by manual dispatch, `supabase db push` in the pipeline, drift and generated-type contract checks, Trivy on the image, AI code review, AI release notes, Playwright E2E.

`FastAPI` `Pydantic v2` `Supabase` `RLS` `pg_cron` `OpenAI` `Docker` `Playwright` `Storybook`

</details>

<details>
<summary><b>Accione Admin - internal portal</b> (React, Express, Supabase)</summary>

<br />

- **Auth:** invite-only accounts with no initial password known to admins, server-side token verification, member state reloaded on every request so deactivation and module removal apply immediately, `503` on provider failures so slow upstreams do not log users out.
- **Authorization:** admin and member roles, per-module guards (tasks, CRM, vault) with a test that fails if a route has no guard, 404 instead of 403 on resources a user cannot see, RLS as a second layer with a test that signs in as a real member and asserts denials.
- **Encryption:** password vault with AES-256-GCM, random 12-byte IV per record, pinned auth tag length, key only in backend env, plaintext only on an explicit rate-limited reveal endpoint.
- **Hardening:** Helmet with strict CSP and HSTS preload, four rate-limit tiers (auth failures counted only), CORS allowlist, 37 versioned migrations with name and sequence validation.
- **Delivery:** CI with lint, tests, `npm audit`, Gitleaks on full history, migrations rebuilt from scratch on a clean Postgres, auto-apply to QA, manual and gated production migration with dry run.
- **Process:** read-only security-review agent required before auth, crypto or RLS changes, OpenSpec for spec-driven changes, recurring task engine (daily, weekly, monthly, quarterly, semiannual).

`React` `Vite` `Node` `Express` `Supabase Auth` `AES-256-GCM` `RLS` `Vercel` `Railway`

</details>

<details>
<summary><b>Agrocash platform - front end and delivery pipeline</b> (React 19, TypeScript, AWS)</summary>

<br />

Second-largest human contributor on the front-end repository.

- **Session security:** JWT in httpOnly cookies (the front never sees the token), session truth from the server, forced logout after password change, optimistic-concurrency conflict handling.
- **Access control:** permission-gated components, three-level scope (platform, company, subscriber), permission matrix editor, scope-aware denials, super-admin impersonation context.
- **Input safety:** Zod 4 validation of uploads (type and size) before presigned upload, CNPJ autofill, strict TypeScript with no `any`.
- **Contract discipline:** API-contract markers with expiry enforced by tests, so an unverified claim about a backend route fails the build. Screens without a backend show an explicit unavailable state instead of mock data.
- **Pipeline:** Trivy severity gate (CRITICAL and HIGH block the PR), CodeQL, actionlint, Playwright, staging contract probes, LLM PR review with secret redaction, static deploy to S3 and CloudFront through GitHub OIDC with environment approval for production.

`React 19` `TypeScript` `TanStack` `Zod` `Tailwind v4` `Playwright` `GitHub Actions` `AWS OIDC` `S3` `CloudFront`

</details>

<details>
<summary><b>PulseStream - sentiment and trend analysis</b> (Django REST, Celery, React)</summary>

<br />

Collects public posts, cleans and analyzes text, and reports trends, sentiment and how both change over time. Built with Django REST Framework, PostgreSQL, Celery and Redis, with pytest and Docker, plus an MCP server.

<!-- Record a short screen capture to assets/pulsestream-demo.gif, then uncomment: -->
<!-- <img src="assets/pulsestream-demo.gif" alt="PulseStream demo" width="720" /> -->

[Repository](https://github.com/leozorzii/PulseStream)

</details>

---

## Toolbox

<div align="center">

![Python](https://img.shields.io/badge/Python-0b0b0c?style=flat-square&logo=python&logoColor=3776AB)
![FastAPI](https://img.shields.io/badge/FastAPI-0b0b0c?style=flat-square&logo=fastapi&logoColor=009688)
![Django](https://img.shields.io/badge/Django_REST-0b0b0c?style=flat-square&logo=django&logoColor=44B78B)
![Node.js](https://img.shields.io/badge/Node.js-0b0b0c?style=flat-square&logo=nodedotjs&logoColor=339933)
![TypeScript](https://img.shields.io/badge/TypeScript-0b0b0c?style=flat-square&logo=typescript&logoColor=3178C6)
![React](https://img.shields.io/badge/React-0b0b0c?style=flat-square&logo=react&logoColor=61DAFB)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-0b0b0c?style=flat-square&logo=postgresql&logoColor=4169E1)
![Supabase](https://img.shields.io/badge/Supabase-0b0b0c?style=flat-square&logo=supabase&logoColor=3FCF8E)
![OpenAI](https://img.shields.io/badge/OpenAI_API-0b0b0c?style=flat-square&logo=openai&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-0b0b0c?style=flat-square&logo=docker&logoColor=2496ED)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-0b0b0c?style=flat-square&logo=githubactions&logoColor=2088FF)
![AWS](https://img.shields.io/badge/AWS_S3_CloudFront-0b0b0c?style=flat-square&logo=amazonaws&logoColor=FF9900)
![Playwright](https://img.shields.io/badge/Playwright-0b0b0c?style=flat-square&logo=playwright&logoColor=2EAD33)

</div>

---

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/leozorzii/leozorzii/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/leozorzii/leozorzii/output/github-snake.svg" />
  <img alt="Contribution snake animation" src="https://raw.githubusercontent.com/leozorzii/leozorzii/output/github-snake.svg" />
</picture>

<br /><br />

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0b0b0c?style=for-the-badge&logo=linkedin&logoColor=0077B5)](https://linkedin.com/in/leozorzii)
[![Email](https://img.shields.io/badge/Email-0b0b0c?style=for-the-badge&logo=gmail&logoColor=D14836)](mailto:leomzorzi@gmail.com)

</div>
