# SpendBar

**Every AI account you use, what each one costs, and one click to switch.**

SpendBar is a native macOS menu bar app that shows everything you spend on AI tools — subscriptions and API bills — in one place. Split costs by project or client, get alerts before you blow a budget, and switch Claude Code or Codex between your accounts in one click.

> **Status:** 🚧 In early development. Features below describe the v1 goal; see the [Roadmap](#roadmap) for what's done.

<!-- Add a screenshot or short GIF of the menu bar popover here once the UI exists:
![SpendBar menu bar popover](docs/images/popover.png) -->

---

## Why

If you use AI tools for work, your spending is scattered: a Claude subscription here, ChatGPT there, Cursor, Copilot, plus API bills across several providers and organizations. Provider dashboards each show one piece. None of them tell you:

- How much you spend on AI **in total** this month
- Which **project or client** that spend belongs to
- When you're about to **go over budget**
- Which of your accounts still has **room left** — and how to switch to it quickly

SpendBar answers all of that from your menu bar.

## Features

### 💸 Spending
- **All subscriptions in one list** — Claude, ChatGPT, Cursor, Copilot, Gemini and more, with renewal reminders
- **Real API costs** pulled from provider billing APIs (Anthropic, OpenAI, OpenRouter)
- **Month-to-date total** in the menu bar, with a forecast for the full month

### 📁 Projects & clients
- Tag accounts and subscriptions to a project or client
- See spend broken down by project
- **Export to CSV** for invoicing and bookkeeping

### 🔔 Budgets & alerts
- Budgets for everything, per account, or per project
- Notifications at 80% and 100% (configurable)
- Spike alerts when today's spend is unusually high

### 🔀 Multiple accounts & one-click switching
- Keep several accounts per tool — e.g. *Work*, *Personal*, *Client A*
- See each account's session and weekly limits and when they reset
- **Switch the active account** for Claude Code or Codex from the menu bar
- Every switch is backed up first, with **Undo last switch**

## Privacy & security

SpendBar is built to be trusted with sensitive keys:

- **Keys and logins are stored only in the macOS Keychain.** Never in files, logs, or app data.
- **No servers, no accounts, no telemetry.** All data stays on your Mac.
- The app only talks to the providers you connect (plus the update feed).
- Billing API keys are read-only admin keys used solely to fetch usage and cost.

## Supported providers

| Provider | Cost tracking | Limits | Account switching |
|---|---|---|---|
| Claude Code (Anthropic) | ✅ Admin API + local logs | ✅ | ✅ |
| Codex (OpenAI) | ✅ Admin API + local logs | ✅ | ✅ |
| OpenRouter | ✅ | — | — |
| Cursor, Copilot, Gemini, others | Manual subscription | — | Planned |

*All planned for v1 unless marked otherwise.*

## Requirements

- macOS 14 Sonoma or later
- Apple Silicon or Intel Mac

## Building from source

Requires Xcode (latest stable) and Swift 6.

```bash
git clone https://github.com/<your-username>/spendbar.git
cd spendbar
open SpendBar.xcodeproj
```

Or from the command line:

```bash
# Build
xcodebuild -scheme SpendBar -destination 'platform=macOS' build

# Run tests
xcodebuild -scheme SpendBar -destination 'platform=macOS' test
```

The app is not sandboxed, because account switching needs to update other tools' login data. It uses the hardened runtime and is distributed with Developer ID signing and notarization.

## Project structure

```
App/         App entry, menu bar, settings
Features/    Dashboard, Accounts, Subscriptions, Budgets, Projects
Core/
  Models/      SwiftData models
  Providers/   Cost and usage sources (one module per provider)
  Switchers/   Account switching (one module per tool)
  Keychain/    Keychain wrapper
  Networking/  HTTP client
  Scheduler/   Background refresh
Tests/
docs/        Technical findings and notes
```

Development guidelines live in [`CLAUDE.md`](CLAUDE.md), and the phased build plan in [`PLAN.md`](PLAN.md).

## Roadmap

- [ ] Research: credential storage, cost and usage APIs
- [ ] Menu bar app + manual subscriptions
- [ ] Keychain + Anthropic, OpenAI and OpenRouter cost tracking
- [ ] Projects, budgets, alerts, CSV export
- [ ] Multiple accounts + limit tracking
- [ ] One-click account switching (Claude Code, Codex)
- [ ] Onboarding, widget, auto-updates, release

**Later:** Cursor switching, team features, more providers.

## Contributing

Bug reports and ideas are welcome — please open an issue. For larger changes, open an issue first to discuss the approach.

## License

<!-- Choose before publishing. Options: MIT (fully open source), a source-available license, or keep the repo private if the app is sold commercially. -->
TBD

---

*SpendBar is an independent project and is not affiliated with, endorsed by, or sponsored by Anthropic, OpenAI, OpenRouter, Cursor, GitHub, Google, or any other provider mentioned. All product names are trademarks of their respective owners.*
