# PayIt2 — Internal Org Guide

> This README is for org members only. It covers repo structure, development workflow, and project context.

---

## What We're Building

PayIt2 is an online payment collection platform for groups, events, and fundraisers. Founded 2007 in Grand Rapids, MI.

**Platform positioning:**
- Open platform — welcomes virtually any lawful purpose
- Key niches: legal defense fundraising, reunions, events & tickets, fundraisers
- Differentiator vs GoFundMe/GiveSendGo: legal defense is our primary niche

**Current focus:** Rebuilding the platform from the ground up (v2) with AI-powered campaign creation, automated promotion, and intelligent supporter engagement.

---

## Repositories

### Active

| Repo | Purpose | Stack |
|------|---------|-------|
| [payit2-app-v2](https://github.com/PayIt2/payit2-app-v2) | **New platform rebuild** — the primary engineering effort | Next.js, TypeScript |
| [payit2-website](https://github.com/PayIt2/payit2-website) | Marketing website at payit2.com | HTML/CSS, Cloudflare Pages |
| [payit2-campaign-coach](https://github.com/PayIt2/payit2-campaign-coach) | Claude Code plugin — AI campaign creation and coaching | Claude plugin |
| [payit2-plugins-marketplace](https://github.com/PayIt2/payit2-plugins-marketplace) | Plugin index — install Campaign Coach and other tools from here | Markdown |
| [payit2-business](https://github.com/PayIt2/payit2-business) | Brand, research, specs, planning docs | Markdown, docs |

### Legacy (maintenance only)

| Repo | Purpose | Stack |
|------|---------|-------|
| [payit2-app-v1](https://github.com/PayIt2/payit2-app-v1) | Live production application (until v2 is ready) | .NET / C# |

---

## Repo Details

### `payit2-app-v2` — Platform Rebuild
The Next.js rebuild of the platform. Still in active development.

```
architecture/   System design and ADRs
backend/        API and server-side code
database/       Schema and migrations
frontend/       UI components and pages
infrastructure/ Deployment and infra config
docs/           Developer documentation
prototypes/     Experiments and spikes
```

### `payit2-website` — Marketing Site
Static marketing site deployed via Cloudflare Pages. Contains 99+ use-case landing pages.

- Landing page pattern: hero with card background + navy overlay, 3-step How It Works, 3-card Why PayIt2, final CTA
- Use case pages live in `use-cases/`
- Shared partials in `shared/`

### `payit2-campaign-coach` — Claude Plugin
A Claude Code plugin that gives users AI-powered campaign management tools.

- Source of truth lives here
- Mirrored to `payit2-plugins-marketplace/payit2-campaign-coach/` on release
- Do **not** sync to `payit2-business/` (that copy was removed)
- Build and release via `build-plugin.sh` / `release.sh`

### `payit2-business` — Brand & Planning
Non-code assets: brand guidelines, research, platform specs, blog drafts, agent configs.

```
brand/      Logo, colors, voice guidelines
research/   User research and competitive analysis
docs/       Platform specs and planning docs
platform/   Product roadmap and strategy
blog/       Draft posts
agents/     AI agent configs and prompts
```

---

## Development Workflow

### Local Setup
Each repo is independent — clone and set up individually. There is no monorepo root.

### Committing
- Work in the individual repo directory
- Commit and push together (no separate confirm step needed)
- If push is rejected, `git pull --rebase` then push again

### Plugin Releases
1. Edit source in `payit2-campaign-coach/plugin/`
2. Run `./build-plugin.sh`
3. Run `./release.sh` to publish
4. Sync updated files to `payit2-plugins-marketplace/payit2-campaign-coach/`

---

## Key Links

| Resource | URL |
|----------|-----|
| Production app | https://payit2.com |
| Marketing site (same) | https://payit2.com |
| Blog | https://blog.payit2.com |
| Support | https://payit2.uservoice.com |
| Contact | help@payit2.com |

---

## Tech Stack Summary

| Layer | Technology |
|-------|-----------|
| Live app (v1) | .NET / C#, Azure |
| New platform (v2) | Next.js 16, TypeScript, Vercel |
| Marketing site | Static HTML/CSS, Cloudflare Pages |
| Payments | Stripe |
| AI tooling | Claude Code, Vercel AI Gateway |
