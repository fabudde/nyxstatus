# 🦞 NyxStatus

**Full-stack uptime monitoring SaaS — built in 378 lines of NyxCode.**

[![Live](https://img.shields.io/badge/live-nyxstatus.com-brightgreen)](https://nyxstatus.com)
[![Built with NyxCode](https://img.shields.io/badge/built%20with-NyxCode%20v0.30-blueviolet)](https://github.com/fabudde/nyxcode)

The proof that one `.nyx` file = production app.

## What is this?

NyxStatus is a real, working uptime monitoring service. Not a demo. Not a prototype. A production SaaS with:

- 🔐 JWT authentication (register, login, logout)
- 📊 Dashboard with per-user monitors
- 🏥 Background health checks (every 60s)
- 📧 Email alerts on downtime
- 🗑️ Cascade deletes (monitors → checks → alerts)
- 📱 Responsive dark theme
- 🔒 Auth guards, user isolation, CSRF protection

**All from a single `site.nyx` file. 378 lines. Zero JavaScript written by hand.**

## The Point

This exists to prove that [NyxCode](https://github.com/fabudde/nyxcode) works. Not in theory — in production.

### NyxCode vs Next.js — Same App, Measured

| | NyxCode | Next.js |
|---|---------|---------|
| Lines | **378** | 1,069 |
| Files | **1** | 27 |
| Tokens | **~2,733** | ~9,476 |
| AI generation cost | **~$0.20** | **~$0.71** |

**3.5x fewer tokens. 71% cheaper.**

The Next.js version is deployed at [nextjsstatus.heynyx.dev](https://nextjsstatus.heynyx.dev) for comparison.

## Quick Start

```bash
# Install NyxCode
npm i -g @fabudde/nyxcode

# Build
nyx build site.nyx

# Configure SMTP (optional, for email alerts)
export SMTP_HOST=your-smtp-server
export SMTP_PORT=587
export SMTP_USER=you@example.com
export SMTP_PASS=your-password

# Run
node dist/server.js
```

Open `http://localhost:3000`, register, add monitors, watch them get checked every 60 seconds.

## Architecture

```
site.nyx (378 lines)
    ↓ nyx build
dist/
├── index.html          # Landing page
├── login/index.html    # Login page
├── register/index.html # Register page
├── dashboard/
│   ├── index.html      # Dashboard (auth required)
│   ├── new/index.html  # Add monitor
│   └── monitor/index.html # Monitor detail
└── server.js           # Express + SQLite + JWT + background workers
```

## What's in site.nyx?

```nyx
use nodemailer                          # SMTP integration
env { SMTP_HOST, SMTP_USER, ... }       # Environment config
table monitors { ... }                  # 4 database tables
security { login email password }       # JWT auth
every 60s 'health-check' { ... }        # Background worker
page / { ... }                          # 6 pages
page /dashboard auth { ... }            # Auth-guarded pages
api POST /api/monitors/delete auth { }  # Custom API endpoints
```

No React. No Vue. No Express boilerplate. No ORM. No webpack. No tailwind. Just NyxCode.

## NyxCode Features Used

- `use` — npm package integration
- `env` — environment variable validation
- `table` — database schema → auto CRUD
- `security` — JWT auth generation
- `every` — background workers
- `page auth` — auth-guarded pages
- `visible=auth/guest` — conditional nav
- `data` + `each` — data binding
- `form` — form handling with success/error
- `preset` — reusable style bundles
- `theme` — design tokens
- `api` — custom endpoints with multi-query

## Created By

**Fabian Budde** 🐻 — Creator
**Nyx** 🦞 — Developer — [@NyxTheLobster](https://x.com/NyxTheLobster)
**Kiro** 🐺 — QA (found 8 bugs in the compiler while dogfooding this)

## License

MIT

---

*Built with [NyxCode](https://github.com/fabudde/nyxcode) v0.30 — the AI-native programming language.*
