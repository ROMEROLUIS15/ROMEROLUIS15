# Luis Romero

AI Engineer and Backend Developer with Full-Stack capabilities, focused on building production software powered by AI, automation, and modern cloud architectures.

I build and deploy complete systems from database design to production infrastructure — AI agents, RAG platforms, multi-tenant SaaS products, payment integrations, and real-time applications.

My focus is not just connecting an LLM. I design the systems around it: deterministic workflows, guardrails, semantic search, observability, evaluation pipelines, and architectures that keep AI reliable when it faces real users.

I build backend for a software company in Texas (United States), while also building and operating my own products in production, used by real businesses every day.

---

## Backend Developer — Complexity (Texas, United States)

Project Factory: backend of a B2B company-directory platform and of its admin panel, with a mobile app. REST API, real time over WebSockets, job queues, full-text search and AI agents (Node.js · NestJS · TypeScript · PostgreSQL · Redis/BullMQ · Elasticsearch · AWS). Private codebase.

- **Setting the backend's direction.** Audited the backend when I joined, presented the findings to the team and got my remediation plan approved, which I led to completion without pausing the roadmap: through incremental refactoring, removed improper coupling between modules, cut circular dependencies from 31 to 0 and moved business logic into 330 use cases on a hexagonal architecture.
- **Agent harness and delivery.** Designed the AI agent harness I work with: numbered rules that the code itself cites, architecture and quality gates, and a check that asks for evidence behind every claim the agent makes (Orca, Gentle AI, MCP, Spec-Driven Development). With it I planned the work in 700+ tickets and delivered 1,050+ merged pull requests and 20+ production releases in three months, reviewing and approving every change.
- **Quality and security pipeline, from scratch.** When I joined, no pull request ran any tests. Today every change goes through strict typing, unit, integration and end-to-end tests, security scanning (SAST/SCA, secrets) and architecture rules, and a full PR is validated in ~6 min. Unit tests grew from 20 to 1,000+ suites. The quality check dropped from 9.4 to 3.8 min through parallel execution and integration suites selected from the dependency graph.
- **Go-to-market backend, end to end.** Led the backend of "claim your company" end to end, the product's go-to-market (GTM) program, now in production and fed by an AI-assisted loading flow I took to production: an agent builds company profiles and product drafts that nobody publishes without human approval. I also delivered the Resend integration, orders on a state machine and search on Elasticsearch.
- **AI extraction engine.** Designed and built an AI extraction engine with current agent-engineering practices: every value carries the quote from its source, two models must agree and code, not the model, decides what gets stored; quality is measured with evals against the human reviewer's decision and traces in Langfuse. It nearly tripled category classification precision.
- **Security and operations.** Took PostgreSQL row-level security (RLS) to production: from 0 to 63 enforced tables in three reversible waves, with pgTAP tests that block the merge. Resolved an urgent personal-data exposure report in under 4 hours, added rate limiting with Redis and operated AWS deployments (EC2, CloudWatch, Secrets Manager), closing two production incidents in under an hour.

---

## What I Do

- Build AI Agents and LLM-powered applications for real-world workflows.
- Design anti-hallucination architectures and AI systems that combine deterministic logic with language models.
- Develop RAG systems using PostgreSQL, pgvector, semantic search, and conversational memory.
- Architect scalable backend platforms with Node.js, TypeScript, Python, PostgreSQL, Redis, and serverless infrastructure.
- Build multi-tenant SaaS platforms with strong data isolation and security controls.
- Integrate authentication, payment gateways, external APIs, voice AI, and real-time communication systems.
- Deliver complete products from database → backend → AI → frontend → CI/CD → production.

---

# Featured Projects

## CRONIX

Multi-tenant SaaS platform for service businesses, with AI-powered appointment management over WhatsApp messages, calls and voice.

### Highlights

- Built and operate the platform end-to-end: database architecture, backend services, AI systems, infrastructure, deployment, and monitoring.
- Developed a custom AI orchestration engine (no framework) for WhatsApp and Voice AI agents using Groq, Deepgram, restricted tool calling, and autonomous scheduling workflows.
- Implemented a deterministic anti-hallucination architecture that stops the agent from inventing data or acting on the wrong customer during appointment and payment operations.
- Built an evaluation and observability layer: golden-conversation regression evals that block CI, LLM-as-judge evals with DeepEval, plus per-business tracing with p50/p95 latency.
- Built a real-time call agent that answers over WhatsApp and books appointments in Cronix by voice (Python, Pipecat Flows, WebRTC, Deepgram): the model talks and code decides every fact and every write, including the caller's confirmation. On Cronix's side, a signed API (HMAC) with idempotency and a lock that prevents booking the same slot twice.
- Chose the call agent's model by measurement, not intuition: on the golden dataset it scored 1.00 on inventing nothing and on no unrequested writes, the first token arrives in 391 ms (p50) and every call is traced in Sentry with its latency and cost.
- Audited multi-tenant isolation until it broke: found and closed a cross-tenant leak in 13 SECURITY DEFINER functions, backed by PostgreSQL Row-Level Security and 147 automated security tests (pgTAP).
- Integrated PayPal, NOWPayments, Binance, and local payment methods with idempotent, webhook-driven fulfillment.
- Production-grade quality pipeline: 1,600+ automated tests, CI/CD, monitoring, and Spec-Driven Development.

**Stack:** TypeScript · Node.js · PostgreSQL · Supabase · Next.js · Edge Functions (Deno) · Redis · pgvector · Groq · Deepgram · WebAuthn · DeepEval · LangSmith · Playwright · pgTAP · GitHub Actions · Vercel

---

## Advanced Product Search API

Product and manufacturer discovery API: relevance ranking, faceted filtering, autocomplete and query suggestions. **Public repository with live API docs — the technical challenge that got me hired.**

**Live:** [OpenAPI docs](https://advanced-search-api-chet.onrender.com/docs) · [Repository](https://github.com/ROMEROLUIS15/advanced-search-api)

### Highlights

- Built BM25 relevance on Elasticsearch 8 with typo tolerance, tuned by popularity and recency (`function_score`), plus type-ahead autocomplete and "did you mean" suggestions.
- Implemented faceted filtering where each dimension's counts exclude its own filter, so users can widen a search instead of hitting zero results — results, facets and suggestions in a single Elasticsearch round-trip.
- Strict hexagonal architecture: the domain layer imports neither NestJS nor Elasticsearch; 7 ports behind `Symbol` tokens, a cache that never fails a request when Redis is down, and rate limiting with Redis→in-process failover.
- Zero-downtime index migrations: each index version is named after the fingerprint of its own definition and goes live by flipping an alias atomically, with liveness split from readiness so the platform's health poll costs no Redis round-trip.
- Access control designed around what each surface actually exposes: an API key on every client endpoint, `/metrics` behind its own bearer token (which the env schema refuses to boot without in production), and `/docs` deliberately *not* exempt — publishing the contract of a catalogue that is not meant for strangers would be a lock on the door with the blueprints taped to the window. The auth guard runs *after* the rate limiter on purpose, so an unauthenticated flood still spends a budget instead of being rejected for free.
- Load-tested for two different questions. Capacity: 398,000 requests, 0 failures, 1,730 req/s, with a per-scenario p95 threshold on all 7 workloads (autocomplete 3.8 ms, warm search 4.5 ms, cold facets 31 ms). Correctness under abuse: flooded well past the budget, the limiter accepted exactly its 60 and rejected the other 240 with a typed 429 — zero 5xx, no timeouts, no slow tail. Plus a smoke suite run against the live production deployment.
- Verified rather than asserted: 500+ tests (97% statement coverage, including integration against a real Elasticsearch cluster; coverage runs as a CI gate, not as a badge), and a full security chain in CI — CodeQL (SAST), Dependabot (SCA), gitleaks over the entire git history, Trivy + SBOM on the shipped image, and OWASP ZAP against the running API (128 URLs, 0 findings). Every action and scanner image pinned by immutable digest, and every ZAP rule override documented as a design decision so the scan stays signal instead of noise.
- Structured logging with a correlation id per request, Prometheus and OTLP metrics, and distributed tracing. Estimates were checked against production rather than trusted: the projected ~400 metric series measured 94, the projected <10 MB/month of logs measured ~2 MB — and the measurement surfaced a real finding, that the platform was throttling the keep-alive cron to roughly one run every 2.5 hours.

**Stack:** TypeScript · NestJS · Elasticsearch 8 · Redis · Docker · OpenAPI/Swagger · OpenTelemetry · Prometheus · k6 · CodeQL · OWASP ZAP · Trivy · GitHub Actions · Render

---

## Motosmax Cordialidad

Multi-tenant SaaS in production for a motorcycle workshop: work orders, per-branch inventory, quotes, motorcycle sales, and CRM.

### Highlights

- Designed and shipped the platform as a monorepo: a NestJS API in hexagonal architecture (37 Prisma models) and a Next.js 15 / React 19 PWA. Work orders run on a state machine, quotes are versioned with client approval, and motorcycle sales include a payment plan, a PDF contract and a sales dashboard.
- Built a multi-agent microservice in Python (FastAPI + LangGraph): one agent serves customers over WhatsApp, another assists the back office with session memory and custom tools, plus periodic reports and proactive low-stock alerts. The LLM model (Groq/DeepSeek) is configurable per environment, and the WhatsApp channel handles Meta's 24h window and surfaces send failures.
- Secured service-to-service communication with short-lived JWTs (5-min TTL), encrypted sensitive fields, BullMQ/Redis queues, Cloudflare R2 storage, and a WebSocket gateway for real time.
- Found and closed a privilege escalation in production (a read-only role could edit the workshop's billing configuration), fixed with per-role permissions pinned by a regression test, and re-keyed rate limiting by user identity instead of shared IP.
- 400+ automated tests (Jest, Vitest, pytest + Playwright E2E) with strict typing (ruff + mypy) in CI; every change starts from a versioned spec (Spec-Driven Development).

**Stack:** TypeScript · NestJS · Prisma · Python · FastAPI · LangGraph · PostgreSQL · Neon · Next.js · React · Redis · BullMQ · Cloudflare R2 · DeepSeek · Groq · Docker

---

## IBIME Connect

Institutional platform for a public library network, replacing a legacy static website with a modern full-stack system and an AI assistant. I built it, the institution adopted it as its official platform, and appointed me to lead its software development.

### Highlights

- Designed and deployed the platform from scratch: administrative tools, citizen services, and AI-powered search.
- Built an architecture that keeps the LLM outside the decision flow: a rule-based intent classifier (no LLM) routes the conversation, and when deterministic data retrieval is possible the answer comes from the database without calling the model, with a deterministic sentiment layer (<1 ms, no model call) that tunes the response.
- Implemented semantic search and Retrieval-Augmented Generation (RAG) using PostgreSQL, pgvector, 768-dim Gemini embeddings, a configurable Groq model (gpt-oss-20b), and Redis caching.
- Developed LangGraph-based document processing that transforms PDF catalogs into validated structured data.
- Hardened the handling of citizens' personal data (RLS on PII tables, idempotent registrations, retention policy), with dependency injection (tsyringe), shared validation schemas, and automated testing.

**Stack:** TypeScript · Node.js · Express · PostgreSQL · Redis · React · Supabase · LangGraph · Gemini · pgvector · Vitest · Playwright

---

## Industrial CMMS

Computerized Maintenance Management System for an industrial maintenance company, in daily use.

### Highlights

- Replaced paper-based inspection workflows with a complete digital platform.
- Developed a multi-agent diagnostic assistant using LangGraph, tool calling, and RAG over historical maintenance data on a persistent pgvector store (pluggable: in-memory in dev, pgvector in prod).
- Built secure backend services with JWT authentication, role-based authorization, idempotency controls, and Server-Sent Events.
- Delivered a React Progressive Web App with offline support, digital signatures, PDF reports, and field-operations capabilities.
- Load-tested with k6 on a real staging environment (200 concurrent users, zero server errors), supported by automated testing, CI pipelines that run the suite against real PostgreSQL (not just SQLite), and dual database environments.

**Stack:** TypeScript · Node.js · PostgreSQL · Neon · React · LangGraph · IndexedDB · PWA · k6 · Docker · Vitest

---

# Core Technologies

### Backend & Architecture

TypeScript · Node.js · Python · Express · NestJS · FastAPI · PostgreSQL · SQL · Prisma · TypeORM · Redis · BullMQ · Elasticsearch · Supabase · REST APIs · OpenAPI/Swagger · Socket.IO · Resend · React Email · Serverless · Edge Functions · Event-Driven Architecture · Hexagonal Architecture · Multi-Tenant Systems · Spec-Driven Development (SDD)

### Harness Engineering & AI-Assisted Development

Claude Code (Anthropic) · Codex (OpenAI) · Orca (ADE) · Gentle AI · Engram (persistent agent memory) · MCP (Linear, Sentry, AWS, Resend, Figma) · Multi-agent orchestration · Subagents · Agent hooks & skills · Context Engineering · Human review · CI quality checks

### AI & LLM Systems

AI Agents · LangGraph · Multi-Agent Orchestration · RAG · Semantic Search · Tool Calling · Function Calling · pgvector · LLM Evaluation (DeepEval) · LLM Observability (LangSmith) · Anti-Hallucination · OpenAI API · OpenRouter · Groq · DeepSeek · Gemini · Deepgram · MCP · Voice AI · Pipecat · Pipecat Flows · WebRTC · Speech-to-Text · Text-to-Speech · Structured Outputs · Agentic AI

### Frontend

React · Next.js · TypeScript · Tailwind CSS · Progressive Web Apps (PWA)

### DevOps & Testing

Docker · AWS (S3, EC2 Auto Scaling, ECR, CloudWatch) · Git · GitHub Actions · CI/CD · Vercel · Render · Cloudflare · Sentry · OpenTelemetry · Load Testing (k6) · Vitest · Jest · pytest · Hypothesis · mypy · Ruff · Bandit · pip-audit · Playwright · pgTAP · CodeQL · Semgrep · Gitleaks · OWASP ZAP · Trivy · SBOM · Supply-Chain Security

---

## Contact

- **LinkedIn:** https://www.linkedin.com/in/hernandezrs955
- **GitHub:** https://github.com/ROMEROLUIS15
- **Email:** lueduar15@gmail.com
