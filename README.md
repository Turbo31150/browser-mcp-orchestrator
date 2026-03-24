<div align="center">

# Browser MCP Orchestrator

**Dual-browser DevTools MCP orchestration with color-routed tab workers**

[![Chrome](https://img.shields.io/badge/Chrome-CDP_9222-4285F4?style=flat-square&logo=googlechrome)](#)
[![Comet](https://img.shields.io/badge/Comet-CDP_9223-FF6B35?style=flat-square)](#)
[![MCP](https://img.shields.io/badge/MCP-enabled-FF8C00?style=flat-square)](#)
[![Zero Reload](https://img.shields.io/badge/Mode-Zero_Reload-00FF88?style=flat-square)](#)

</div>

---

## What is this?

A browser orchestration layer that controls Chrome and Comet via **Chrome DevTools Protocol** (CDP). Instead of traditional web navigation, it injects directly into the DOM for instant execution — **zero page reloads**.

Part of the [JARVIS OS](https://github.com/Turbo31150/jarvis-linux) ecosystem.

## Architecture

```
Intent → Route (Color) → Browser (Chrome/Comet) → Tab (CDP) → Action → Result
```

### Color Routing
| Color | Purpose | Port |
|-------|---------|------|
| Rouge | Social (LinkedIn, Twitter) | Chrome :9222 |
| Bleu | Trading (MEXC, GitHub) | Chrome :9222 |
| Jaune | Content generation | Chrome :9222 |
| Vert | Automation (Email, Perplexity) | Comet :9223 |

## Features

- **Zero-reload DOM injection** — no page navigation, instant execution
- **Multi-tab workers** — each tab is a specialized worker
- **Tab registry** — auto-synced from CDP every 30s
- **18 pre-built actions** — LinkedIn post, MEXC price check, screenshot, meta extraction
- **DevTools MCP specs** — perf audit, SEO check, network scan, meta extraction
- **Domino integration** — browser steps in automation pipelines

## Actions Registry

```json
linkedin_post, linkedin_paste_content, linkedin_publish,
github_navigate_repo, github_check_actions, github_extract_readme,
mexc_check_price, mexc_extract_orderbook, tradingview_screenshot,
perplexity_search, gmail_check_inbox, gmail_extract_unread,
generic_screenshot, generic_extract_meta, generic_extract_links,
generic_extract_headings, generic_dom_inject, codeur_check_profile
```

## Quick Start

```bash
# Start Chrome with CDP
google-chrome --remote-debugging-port=9222 --no-first-run

# Dispatch an action
from browser_orchestrator import BrowserOrchestrator
o = BrowserOrchestrator()
result = await o.dispatch("bleu", "navigate", {"url": "https://github.com"})
```

## Related

- [JARVIS OS](https://github.com/Turbo31150/jarvis-linux) — The parent system
- [TradeOracle](https://github.com/Turbo31150/TradeOracle) — Trading engine using browser automation
- [Whisper Flow](https://github.com/Turbo31150/jarvis-whisper-flow) — Voice pipeline triggering browser actions

---

**Built by [Franck Delmas](https://github.com/Turbo31150)**
