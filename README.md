# Luis Romero

**Full-Stack Developer** — I build real products, ship them to production, 
and solve hard problems autonomously.

---

## 🚀 What I've Built

### CRONIX — Multi-tenant SaaS in Production
**[cronix-app.vercel.app](https://cronix-app.vercel.app)**

A business and appointment management platform for service businesses 
in Latin America. Built entirely solo.

- **WhatsApp AI Agent** — Groq + Llama 3.3 (70b) for natural language 
  appointment booking. ~1.2s response latency via LPU architecture
- **Voice transcription** — Users send voice notes in Spanish, 
  transcribed via Groq Whisper and processed by the AI agent
- **Biometric auth** — WebAuthn/Passkeys (Face ID + fingerprint) via 
  @simplewebauthn v13. Zero-password login on iOS, Android and desktop
- **Google OAuth** with automatic identity linking — same-email accounts 
  merge regardless of sign-in method
- **3-layer anti-spam** — Atomic PostgreSQL rate limiting (10 msg/60s), 
  anti-prompt-injection sanitization, booking rate limiting (2/24h)
- **Push notifications** — Triggered by Supabase Database Webhooks 
  on appointment insert. Event-driven, fully decoupled
- **RLS multi-tenancy** — 26 pgTAP integration tests against real 
  PostgreSQL. No mocks
- **PWA** — Installable on iOS, Android and desktop. Offline support
- **Full-stack Sentry** — Multi-tenant error monitoring across Next.js 
  and Supabase Edge Functions (Deno)

`Next.js 14` `TypeScript` `PostgreSQL` `Supabase` `Groq API` `Llama 3.3`
`Groq Whisper` `WebAuthn` `React Query v5` `Zod` `pgTAP` `Sentry` `Vercel`

---

### IBIME Connect — Institutional Government Platform
**[ibime-connect.vercel.app](https://ibime-connect.vercel.app)**

I identified that the organization was running on a static HTML page. 
I designed and built a modern platform on my own initiative — 
they adopted it fully and migrated their entire system.

- **RAG pipeline** — pgvector (PostgreSQL) for semantic search + 
  Google Gemini API for natural language responses. Deployed via 
  Supabase Edge Functions (Deno). All AI keys server-side
- **Event registration system** — Cultural events and courses with 
  full relational schema and RLS policies
- **Citizen contact inbox** — Automated request management
- **Real-time visitor counter**
- Accessible UI with dark/light mode, glassmorphism design, 
  shadcn/ui + Radix UI primitives

`React 18` `TypeScript` `Vite` `Supabase` `pgvector` `Google Gemini`
`Edge Functions (Deno)` `TanStack React Query` `Tailwind CSS` `shadcn/ui`

---

## 🛠 Stack
```
Languages:   TypeScript · JavaScript · SQL
Backend:     Next.js 14 (App Router) · Node.js · Express · Supabase Edge Functions (Deno)
Databases:   PostgreSQL · MySQL · MongoDB · pgvector
Auth:        WebAuthn/Passkeys · Google OAuth · JWT · Bcrypt · RLS
AI & LLMs:   RAG · Groq API · Llama 3.3 · Groq Whisper · Google Gemini · pgvector
Frontend:    React 18 · Next.js · Tailwind CSS · shadcn/ui · Radix UI · PWA
Testing:     Vitest · pgTAP
Infra:       Vercel · GitHub Actions · Docker · Sentry · n8n
```

---

## 📫 Contact

[LinkedIn](https://www.linkedin.com/in/luisromero15/) · 
[Portfolio](https://portafolio-luis-romero.vercel.app/) · 
[lueduar15@gmail.com](mailto:lueduar15@gmail.com)





