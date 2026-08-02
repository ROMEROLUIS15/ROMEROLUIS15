# Luis Romero

AI Engineer and Backend Developer with Full-Stack capabilities, focused on building production software powered by AI, automation, and modern cloud architectures.

I build and deploy complete systems from database design to production infrastructure — AI agents, RAG platforms, multi-tenant SaaS products, payment integrations, and real-time applications.

My focus is not just connecting an LLM. I design the systems around it: deterministic workflows, guardrails, semantic search, observability, evaluation pipelines, and architectures that keep AI reliable when it faces real users.

Currently a backend developer at a US software company, while building and operating my own products in production, used by real businesses every day.

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

Multi-tenant SaaS platform for service businesses, with AI-powered appointment management over WhatsApp and voice.

### Highlights

- Built and operate the platform end-to-end: database architecture, backend services, AI systems, infrastructure, deployment, and monitoring.
- Developed a custom AI orchestration engine (no framework) for WhatsApp and Voice AI agents using Groq, Deepgram, restricted tool calling, and autonomous scheduling workflows.
- Implemented a deterministic anti-hallucination architecture that stops the agent from inventing data or acting on the wrong customer during appointment and payment operations.
- Built an evaluation and observability layer: LLM-as-judge regression evals that block CI, plus per-business tracing with p50/p95 latency.
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

TypeScript · Node.js · Python · Express · NestJS · FastAPI · PostgreSQL · SQL · Prisma · Redis · Elasticsearch · Supabase · REST APIs · OpenAPI/Swagger · Serverless · Edge Functions · Event-Driven Architecture · Hexagonal Architecture · Multi-Tenant Systems · Spec-Driven Development (SDD)

### AI & LLM Systems

AI Agents · LangGraph · Multi-Agent Orchestration · RAG · Semantic Search · Tool Calling · Function Calling · pgvector · LLM Evaluation (DeepEval) · LLM Observability (LangSmith) · Anti-Hallucination · Groq · DeepSeek · Gemini · Deepgram · MCP · Voice AI

### Frontend

React · Next.js · TypeScript · Tailwind CSS · Progressive Web Apps (PWA)

### DevOps & Testing

Docker · GitHub Actions · CI/CD · Vercel · Render · Cloudflare · Sentry · OpenTelemetry · Load Testing (k6) · Vitest · Jest · pytest · Playwright · pgTAP · CodeQL · OWASP ZAP · Trivy · SBOM · Supply-Chain Security

---

## Contact

- **LinkedIn:** https://www.linkedin.com/in/luis-romero-dev-back15/
- **GitHub:** https://github.com/ROMEROLUIS15
- **Email:** lueduar15@gmail.com
