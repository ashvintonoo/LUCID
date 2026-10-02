# LUCID

**Personalized CBT-I sleep programs, delivered as a daily protocol.**
Live at [lucidoptimize.com](https://lucidoptimize.com)

LUCID delivers Cognitive Behavioral Therapy for Insomnia (CBT-I), the first-line clinical treatment for insomnia, as an adaptive daily program. It is not a sleep tracker or a meditation app: it tells users what to do, then adjusts based on their data.

> The production source is private. This repo documents the product and its architecture.

## How it works

- **Intake and protocol assignment.** An 11-question intake is scored by a deterministic engine (no LLM in the loop) that assigns one of three protocols: Off-Switch (sleep onset, racing mind), Deep Sleep (night and early waking) or Performance (athletes). Mixed profiles get a hybrid protocol. The full scoring breakdown is stored as an audit trail.
- **Daily dashboard.** One action per time block (morning, evening, bedtime), changing with time of day and program phase.
- **Check-ins.** Morning and evening check-ins capture sleep quality, onset latency, wakings, stress, caffeine, alcohol, exercise timing and per-instruction compliance.
- **Phase progression.** Build → Lock In → Steady → Established, driven by a graduation engine with logged transitions.
- **AI sleep coach.** Built on the Claude API and grounded in the user's own check-in data and protocol, with rate limiting.
- **Lab analytics.** A Borbély two-process sleep model, an intervention half-life view and a constraint optimizer, all computed server-side.
- **Lifecycle email.** Welcome, daily nudges, milestones and missed-day recovery, sent on scheduled jobs with deduplication.

## Stack

| Layer | Technology |
| --- | --- |
| Frontend | Next.js 14, React, TypeScript, Tailwind CSS, shadcn/ui |
| Backend | Next.js API routes (serverless) |
| Database and auth | Supabase (PostgreSQL, row-level security) |
| AI | Claude API |
| Payments | Stripe subscriptions |
| Email | Resend, Vercel cron |
| Hosting | Vercel |

## Design decisions

- **Deterministic where it matters.** Protocol assignment is rule-based and auditable; the LLM is used only for coaching.
- **Modular protocols.** New protocols plug into the same intake, scoring and phase framework.
- **Every interaction is captured.** Check-ins, compliance and phase transitions are stored for adaptation and outcome analysis.

## Author

Built solo by [Ashvin Tonoo](https://github.com/ashvintonoo).
