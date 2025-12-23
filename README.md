# FocusMe

**Intelligent Productivity Orchestration Platform**

> Give people back their best hours by removing coordination friction.

[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](LICENSE)
[![Phase 0](https://img.shields.io/badge/Phase-0%20Planning%20Complete-green.svg)](#project-status)

---

## What is FocusMe?

FocusMe is an open-source productivity orchestration platform designed for busy professionals who struggle with:
- **Constant context switching** and fragmented focus time
- **Manual coordination overhead** (finding meeting times, checking room availability)
- **Reminder fatigue** and procrastination loops
- **Loss of context** between meetings and projects
- **Difficulty prioritizing** in fast-paced environments

**Target Users:** ADHD office workers, project managers, and anyone involved in 3+ projects who need intelligent help managing their calendar and maximizing focus time.

---

## Project Status

**Current Phase:** ✅ **Phase 0 Planning COMPLETE** (2025-12-22)

**Next Steps:** Beginning implementation with PR #1 (Repository Foundation)

### What We've Completed

- ✅ Comprehensive competitive analysis of 10+ productivity tools
- ✅ Technical architecture designed (Next.js 15 + PostgreSQL + tRPC)
- ✅ User requirements refined through interactive Q&A
- ✅ MVP scope prioritized (flexible meetings + meeting relationships)
- ✅ Phase 0 broken into 9 logical PRs (~40-50 hours estimated)
- ✅ Deployment strategy finalized (Vercel + Neon / Podman Compose)

### Planning Documents

- **Full Planning Document:** See `/Users/bmucklow/.claude/plans/twinkly-tumbling-pascal.md`
- **Initial Planning:** See `docs/initial-planning/` worktree
  - Mission & Vision: `docs/mission.md`
  - MVP Requirements: `docs/mvp.md`
  - Competitive Analysis: `docs/competitive_analysis_summary.md`
  - Planning Status: `docs/phase0_planning_status.md`

---

## Key Features (Planned)

### Phase 0 (Infrastructure - Current)
- Dual calendar provider support (Microsoft Outlook + Google Calendar)
- OAuth authentication with NextAuth.js v5
- Calendar event viewing and flexible meeting toggle
- PostgreSQL database with Prisma ORM

### MVP (Phase 1)
- **Flexible Meeting Modeling** - Mark meetings as flexible/fixed, get optimization suggestions
- **Meeting Relationships** - Connect prep time, follow-ups, meetings that move together
- **Priority Learning** - AI learns which meetings/people are important
- **Visual Priority Indicators** - See at-a-glance which meetings matter most

### Future Phases
- Auto-find optimal meeting times + room booking
- Full AI note integration (Zoom AI Companion)
- Advanced analytics and reports
- Mobile applications

---

## Technology Stack

**Frontend:**
- Next.js 15 (App Router) + React 19 + TypeScript
- Shadcn/ui + Tailwind CSS (ADHD-friendly visual design)
- Zustand (state) + React Query (server state)

**Backend:**
- Next.js API Routes + tRPC (type-safe API)
- Microsoft Graph SDK + Google Calendar API
- Calendar provider abstraction for extensibility

**Database:**
- PostgreSQL 16 + Prisma ORM + pgvector (AI embeddings)

**AI/ML:**
- Dual support: OpenAI/Claude API + self-hosted Ollama
- LangChain for orchestration

**Testing:**
- Vitest (unit tests) + Playwright (E2E) + MSW (API mocking)

**Deployment:**
- Hosted: Vercel + Neon PostgreSQL
- Self-hosted: Podman Compose (rootless containers)

---

## Competitive Advantages

**What makes FocusMe unique:**
- ✅ Only tool with flexible meeting modeling + participant priority learning
- ✅ Only tool tracking meeting relationships (prep, followups)
- ✅ Only tool with dual AI support (cloud API + self-hosted Ollama)
- ✅ Only full open-source solution with self-hosted option
- ✅ Designed specifically for ADHD professionals with sophisticated calendar needs

**White-space opportunity:** No existing product combines meeting intent modeling, elastic priority-aware scheduling, unified reasoning across calendar/email/tasks, and continuous focus guidance.

See `docs/competitive_analysis_summary.md` for detailed competitive research.

---

## Getting Started

**Status:** Not yet ready for development setup (Phase 0 in progress)

Once PR #1 is complete, you'll be able to:
```bash
# Clone the repository
git clone https://github.com/blainemucklow/focusme.git
cd focusme

# Install dependencies
pnpm install

# Start PostgreSQL
podman-compose up -d

# Run database migrations
pnpm db:migrate

# Start development server
pnpm dev
```

**Stay tuned for setup instructions in PR #1!**

---

## Contributing

**Status:** Contribution guidelines will be available after PR #8 (Documentation)

FocusMe is open source (GPL-3.0) and welcomes contributors! We're building this in the open with:
- Industry-standard security practices
- Robust architecture for extensibility
- Comprehensive documentation
- Clean PR workflow for easy contributions

---

## Roadmap

### Phase 0: Infrastructure Setup (Current - ~40-50 hours)
- [ ] PR #1: Repository Foundation & Build Infrastructure
- [ ] PR #2: Database Schema & Migrations
- [ ] PR #3: Authentication Infrastructure
- [ ] PR #4: Calendar Provider Abstraction
- [ ] PR #5: tRPC API Layer
- [ ] PR #6: Frontend Calendar UI
- [ ] PR #7: Testing Infrastructure
- [ ] PR #8: Documentation
- [ ] PR #9: UX Wireframes (Excalidraw)

### Phase 1: MVP Features
- Flexible meeting modeling + optimization engine
- Meeting relationships (prep, followups, connected meetings)
- Priority tagging + VIP detection

### Phase 2: Enhancement
- Auto-find optimal meeting times
- Room booking automation
- Advanced analytics

### Phase 3: Scale
- Mobile applications
- Reports and dashboards
- Deep AI integration

---

## License

GPL-3.0 - See [LICENSE](LICENSE) for details

---

## Contact

**Repository:** https://github.com/blainemucklow/focusme

---

*Less coordination. More focus.* 🎯
