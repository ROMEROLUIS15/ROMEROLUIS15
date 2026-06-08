# Luis Romero

Backend & AI Engineer with Full-Stack capabilities focused on building real-world software products with autonomous AI agents, backend architectures, and rigorous deterministic engineering.

I focus on designing and scaling end-to-end cloud platforms, optimizing relational domains, enforcing multi-tenant data isolation, and implementing multi-layer anti-hallucination architectures for generative AI.

Currently developing, scaling, and maintaining products actively used by real users.

---

# 🚀 Featured Production Systems

## ▶ CRONIX — Multi-Tenant SaaS Platform
🔗 (https://cronix-app.vercel.app/)

A multi-tenant SaaS platform for service businesses in Latin America, designed and scaled independently from infrastructure to edge deployment.

### Highlights
- **Custom AI Orchestration Engine:** Frameworkless integration for WhatsApp and web voice agents utilizing Groq and Deepgram with 11 core system capabilities and autonomous scheduling pipelines.
- **5-Layer Anti-Hallucination Flow:** Implemented Fast Paths, Privacy Gates, fail-hard RAG thresholds, Response Guardrails, and rigid Backend Response Policies to keep the LLM off the critical path for cached operations.
- **Strict Multi-Tenant Isolation:** Enforced data security across 4 distinct layers using PostgreSQL Row-Level Security (116 RLS policies over 44 tables), fully validated via 127 automated pgTAP assertion tests.
- **Edge Architecture & Observability:** Instrumented a tracking layer across 9 Deno Edge Functions, capturing structured logs for latency, token consumption, and automated multi-tenant error tracking.
- **Idempotent Billing Systems:** Integrated global and local payment webhooks (PayPal, NOWPayments, Pago Móvil, Binance) backed by an asynchronous queue fulfillment architecture via Upstash QStash.
- **Enterprise Core Features:** WebAuthn/Passkeys authentication (Face ID & fingerprint), 3-layer anti-spam protection with PostgreSQL atomic rate-limiting, and an installable PWA with offline support.

**Stack:** Next.js 15 · TypeScript · Node.js · PostgreSQL · Supabase · Row-Level Security (RLS) · Edge Functions (Deno) · Groq API · Deepgram · Upstash · Redis · pgTAP · Sentry · Vercel

---

## ▶ IBIME Connect — Government Institutional Platform
🔗 (https://ibime-connect.vercel.app/))

Modernization of a legacy government static HTML/CSS web ecosystem into an institutional full-stack digital platform.

### Highlights
- **Stateful AI Agent Pipelines:** Built a data processing engine using LangGraph (extractor-validator-corrector loop) to parse and structure complex catalog PDFs into validated JSON schemas.
- **Hybrid RAG Architecture:** Engineered a semantic search pipeline over PostgreSQL + pgvector utilizing Gemini embeddings, optimized via Redis session caching and a custom token rate limiter.
- **Comprehensive Quality Gate:** Established clean architecture principles, strict dependency injection, and shared Zod schema validation across front-and-backend, backed by 230+ automated tests (Vitest + Playwright).
- **Core Government Operations:** Designed an event/course registration system, an automated citizen inbox, and a secure document ingestion pipeline with contextual chunking.

**Stack:** React · TypeScript · Node.js · Express · PostgreSQL · pgvector · Gemini · LangGraph · Redis · Supabase · Zod · Vitest · Playwright · Vercel

---

## ▶ Industrial CMMS — Maintenance & Logistics Infrastructure

Designed and deployed an end-to-end industrial Computerized Maintenance Management System, digitizing and replacing paper-based inspection workflows for an industrial maintenance firm.

### Highlights
- **Relational Backend:** Architected 52 REST endpoints over 11 relational data models, featuring JWT rotative refresh tokens, request idempotency, and role+ownership authorization.
- **Multi-Graph Diagnostic Assistant:** Built an AI diagnostic subsystem using a multi-node LangGraph orchestration architecture with tool-calling agents over historical industrial inspection logs.
- **High-Performance PWA:** Delivered a React 19 Progressive Web App featuring full offline capabilities (IndexedDB + Background Sync), a 13-step inspection wizard with digital Canvas signatures, and real-time streaming via Server-Sent Events (SSE).
- **Testing Coverage:** Backed by 394 automated tests achieving 82% backend line coverage with dual-database support (PostgreSQL/Neon + SQLite).

**Stack:** React 19 · Node.js · TypeScript · LangGraph · PostgreSQL · SQLite · IndexedDB · Server-Sent Events (SSE) · Docker · PWA · Vitest

---

# 🛠 Core Stack

### Backend & Architecture
TypeScript · Node.js · Express · NestJS · PostgreSQL · Supabase · Row-Level Security (RLS) · Redis · SQL · REST APIs · System Design

### AI & Intelligent Agents
LangGraph · Retrieval-Augmented Generation (RAG) · LLM Orchestration · pgvector · Vector Databases · Groq · Google Gemini · Prompt Engineering

### Frontend & Mobile
React · Next.js · Tailwind CSS · TypeScript · JavaScript · HTML5/CSS3 · IndexedDB · Progressive Web Apps (PWA)

### DevOps, Infra & Testing
Docker · GitHub Actions · CI/CD Pipelines · Automated Testing (Vitest · Playwright · pgTAP) · Sentry · Vercel · Deno Deploy · Edge Computing

---

# 📫 Contact

- **LinkedIn:** (https://www.linkedin.com/in/luisromero15/))
- **GitHub:** (https://github.com/ROMEROLUIS15))
- **Email:** lueduar15@gmail.com

