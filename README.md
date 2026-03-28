<div align="center">

# Browser MCP Orchestrator

**Dual-browser DevTools MCP orchestration with color-routed tab workers**

<br/>

[![Chrome](https://img.shields.io/badge/Chrome-CDP_9222-4285F4?style=flat-square&logo=googlechrome&logoColor=white)](#)
[![Comet](https://img.shields.io/badge/Comet-CDP_9223-FF6B35?style=flat-square)](#)
[![MCP](https://img.shields.io/badge/MCP-Protocol-FF8C00?style=flat-square)](#)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)](#)
[![DevTools](https://img.shields.io/badge/DevTools-Protocol-47A248?style=flat-square)](#)
[![Zero Reload](https://img.shields.io/badge/Mode-Zero_Reload-00FF88?style=flat-square)](#)
[![DOM Injection](https://img.shields.io/badge/DOM-Direct_Injection-FF4444?style=flat-square)](#)
[![Actions](https://img.shields.io/badge/Actions-18_built--in-58A6FF?style=flat-square)](#actions-registry)
[![JARVIS](https://img.shields.io/badge/JARVIS-Ecosystem-8B5CF6?style=flat-square)](https://github.com/Turbo31150/jarvis-linux)

<br/>

<p><em>A browser orchestration layer that controls Chrome and Comet via Chrome DevTools Protocol (CDP). Instead of traditional web navigation, it injects directly into the DOM for instant execution -- zero page reloads.</em></p>

[**Architecture**](#architecture) · [**Color Routing**](#color-routing) · [**Features**](#features) · [**Actions**](#actions-registry) · [**Quick Start**](#quick-start) · [**Ecosystem**](#jarvis-ecosystem)

</div>

---



## Architecture

```mermaid
graph LR
    Orchestrator[MCP Orchestrator] --> B1[Browser 1 CDP]
    Orchestrator --> B2[Browser 2 CDP]
    B1 --> Sites[Web Sites]
    B2 --> Sites
    Orchestrator --> Router[Color Router]
    Router --> AI[AI Analysis]
```

## Overview

Part of the [JARVIS OS](https://github.com/Turbo31150/jarvis-linux) ecosystem, the **Browser MCP Orchestrator** provides a unified interface to control multiple browser instances through the Chrome DevTools Protocol. Each browser tab becomes a specialized worker, routed by color-coded intent categories.

Key differentiator: **zero-reload DOM injection** -- actions execute directly in the page context without triggering navigation or page refreshes.

---

## Architecture

```
Intent -> Route (Color) -> Browser (Chrome/Comet) -> Tab (CDP) -> Action -> Result
```

### Detailed Flow

```
+------------+     +---------------+     +------------------+
| JARVIS     | --> | MCP           | --> | Route Dispatcher |
| Orchestrator|     | Protocol Layer|     | (Color Router)   |
+------------+     +---------------+     +--------+---------+
                                                  |
                                    +-------------+-------------+
                                    |                           |
                            +-------v-------+           +-------v-------+
                            | Chrome        |           | Comet         |
                            | CDP :9222     |           | CDP :9223     |
                            +-------+-------+           +-------+-------+
                                    |                           |
                            +-------v-------+           +-------v-------+
                            | Tab Registry  |           | Tab Registry  |
                            | Rouge | Bleu  |           | Vert tabs     |
                            | Jaune tabs    |           |               |
                            +---------------+           +---------------+
```

---

## Color Routing

| Color | Purpose | Browser | Port | Use Cases |
|-------|---------|---------|:----:|-----------|
| **Rouge** | Social | Chrome | 9222 | LinkedIn posts, Twitter engagement |
| **Bleu** | Trading | Chrome | 9222 | MEXC prices, GitHub Actions, TradingView |
| **Jaune** | Content | Chrome | 9222 | Content generation, SEO audits |
| **Vert** | Automation | Comet | 9223 | Email, Perplexity search, scraping |

---

## Features

| Feature | Description |
|---------|-------------|
| **Zero-reload DOM injection** | No page navigation, instant execution in page context |
| **Dual-browser control** | Chrome + Comet managed simultaneously |
| **Multi-tab workers** | Each tab is a specialized worker with dedicated purpose |
| **Tab registry** | Auto-synced from CDP every 30s, always up-to-date |
| **18 pre-built actions** | LinkedIn, MEXC, GitHub, Gmail, Perplexity, screenshots |
| **DevTools MCP specs** | Performance audit, SEO check, network scan, meta extraction |
| **Color routing** | Intent-based routing to the right browser and tab |
| **Domino integration** | Browser steps in JARVIS automation pipelines |
| **Screenshot capture** | Full-page and element-level screenshots |
| **Network monitoring** | Request/response interception and analysis |

---

## Actions Registry

### Social (Rouge)

| Action | Description |
|--------|-------------|
| `linkedin_post` | Navigate to LinkedIn post creation |
| `linkedin_paste_content` | Inject content into post editor |
| `linkedin_publish` | Publish the post |

### Trading (Bleu)

| Action | Description |
|--------|-------------|
| `mexc_check_price` | Extract current price from MEXC |
| `mexc_extract_orderbook` | Pull orderbook data |
| `tradingview_screenshot` | Capture chart screenshot |
| `github_navigate_repo` | Navigate to a repository |
| `github_check_actions` | Check CI/CD status |
| `github_extract_readme` | Extract README content |

### Automation (Vert)

| Action | Description |
|--------|-------------|
| `perplexity_search` | Execute search query |
| `gmail_check_inbox` | Check inbox status |
| `gmail_extract_unread` | Extract unread emails |
| `codeur_check_profile` | Check freelance profile |

### Generic

| Action | Description |
|--------|-------------|
| `generic_screenshot` | Full-page screenshot |
| `generic_extract_meta` | Extract page metadata |
| `generic_extract_links` | Extract all page links |
| `generic_extract_headings` | Extract heading structure |
| `generic_dom_inject` | Inject arbitrary JavaScript |

---

## Quick Start

```bash
# Start Chrome with CDP
google-chrome --remote-debugging-port=9222 --no-first-run

# (Optional) Start Comet with CDP
comet-browser --remote-debugging-port=9223

# Dispatch an action
from browser_orchestrator import BrowserOrchestrator

o = BrowserOrchestrator()
result = await o.dispatch("bleu", "navigate", {"url": "https://github.com"})
```

### Example: Multi-step automation

```python
o = BrowserOrchestrator()

# Check crypto price
price = await o.dispatch("bleu", "mexc_check_price", {"pair": "BTC/USDT"})

# Take TradingView screenshot
screenshot = await o.dispatch("bleu", "tradingview_screenshot", {"symbol": "BTCUSDT"})

# Post update to LinkedIn
await o.dispatch("rouge", "linkedin_post", {"content": f"BTC at {price}"})

# Search for analysis
analysis = await o.dispatch("vert", "perplexity_search", {"query": "BTC market analysis"})
```

---

## Configuration

| Parameter | Default | Description |
|-----------|---------|-------------|
| `CHROME_CDP_PORT` | 9222 | Chrome DevTools Protocol port |
| `COMET_CDP_PORT` | 9223 | Comet DevTools Protocol port |
| `TAB_SYNC_INTERVAL` | 30s | Tab registry refresh interval |
| `ACTION_TIMEOUT` | 10s | Default action timeout |
| `SCREENSHOT_FORMAT` | png | Screenshot output format |

---

## JARVIS Ecosystem

| Project | Description |
|---------|-------------|
| [jarvis-linux](https://github.com/Turbo31150/jarvis-linux) | Distributed Autonomous AI Cluster |
| **browser-mcp-orchestrator** | Dual-Browser DevTools Orchestration *(this repo)* |
| [github-social-automation](https://github.com/Turbo31150/github-social-automation) | GitHub Social Automation via Comet Bridge |
| [TradeOracle](https://github.com/Turbo31150/TradeOracle) | Autonomous Crypto Trading Agent |
| [lumen](https://github.com/Turbo31150/lumen) | Multilingual Live AI Web App |



## What is Browser MCP Orchestrator?

Automate any web workflow using two browsers simultaneously. While Browser 1 scrapes data, Browser 2 can fill forms — both controlled by MCP (Model Context Protocol) and Chrome DevTools.

Built for JARVIS OS to handle tasks like: scanning Codeur.com for projects, posting on LinkedIn, and managing multiple web sessions in parallel.

## Usage Examples

```python
# Example 1: Scrape + act in parallel
browser1.navigate("https://codeur.com/projects")  # Scrape
browser2.navigate("https://linkedin.com/feed")     # Post

projects = browser1.extract_data()
browser2.post_comment(generate_comment(projects))

# Example 2: Form automation
browser1.navigate("https://codeur.com/offers/new")
browser1.fill("#amount", "750")
browser1.fill("#message", proposal_text)
browser1.click("#submit")

# Example 3: Screenshot verification
browser1.screenshot("/tmp/result.png")
# → Verify the action was successful
```

## Use Cases

| Workflow | Description |
|----------|-------------|
| **Freelance prospection** | Scan Codeur → filter → auto-apply |
| **LinkedIn engagement** | Read notifications → draft replies → post |
| **Price monitoring** | Track prices across multiple sites |
| **Form filling** | Auto-fill applications, registrations |
| **Data extraction** | Scrape tables, lists, structured data |

---

<div align="center">

**Built by [Franck Delmas](https://github.com/Turbo31150)** · Toulouse, France

*Browser MCP Orchestrator -- MIT License*

> Freelance profile: [codeur.com/-6666zlkh](https://www.codeur.com/-6666zlkh)

</div>


---

## Selector Caching

### How It Works

The orchestrator caches CSS selectors to avoid redundant DOM queries. When an action first resolves a selector (e.g., `#post-editor`, `.price-display`), the result is cached with the page URL as the cache key. Subsequent actions on the same page reuse the cached selector, reducing CDP round-trips by up to 60%.

### Cache Structure

```python
# Internal cache format
selector_cache = {
    "https://linkedin.com/feed": {
        "#post-editor": {
            "node_id": 142,
            "backend_node_id": 58,
            "resolved_at": 1711500000,
            "ttl": 300,            # 5 minutes
            "hit_count": 12
        },
        ".share-box__open": {
            "node_id": 89,
            "backend_node_id": 34,
            "resolved_at": 1711500010,
            "ttl": 300,
            "hit_count": 7
        }
    }
}
```

### Cache Invalidation

The cache is invalidated automatically when:
- The page navigates to a new URL (full cache clear for that tab)
- The TTL expires (default: 300 seconds per entry)
- A DOM mutation is detected via `MutationObserver` injection
- An action explicitly calls `cache.invalidate(url, selector)`

### Configuration

```yaml
selector_cache:
  enabled: true
  default_ttl: 300           # seconds
  max_entries_per_page: 200  # prevent memory bloat
  mutation_observer: true    # auto-invalidate on DOM changes
  persist_to_disk: false     # ephemeral by default
```

---

## CDP Protocol Reference

### Common Operations

The orchestrator uses the Chrome DevTools Protocol (CDP) for all browser interactions. Here are the most frequently used CDP domains and methods:

#### Page Navigation

```python
# Navigate to a URL
await cdp_send("Page.navigate", {"url": "https://example.com"})

# Wait for page load
await cdp_send("Page.setLifecycleEventsEnabled", {"enabled": True})
# Listen for "networkIdle" event

# Reload the page
await cdp_send("Page.reload", {"ignoreCache": True})
```

#### DOM Interaction

```python
# Get the document root
doc = await cdp_send("DOM.getDocument", {"depth": 0})
root_id = doc["root"]["nodeId"]

# Query a selector
result = await cdp_send("DOM.querySelector", {
    "nodeId": root_id,
    "selector": "#my-element"
})
node_id = result["nodeId"]

# Get element attributes
attrs = await cdp_send("DOM.getAttributes", {"nodeId": node_id})

# Set an attribute value
await cdp_send("DOM.setAttributeValue", {
    "nodeId": node_id,
    "name": "value",
    "value": "new content"
})

# Get outer HTML
html = await cdp_send("DOM.getOuterHTML", {"nodeId": node_id})
```

#### JavaScript Execution

```python
# Execute JavaScript in page context
result = await cdp_send("Runtime.evaluate", {
    "expression": "document.title",
    "returnByValue": True
})
title = result["result"]["value"]

# Execute with await (for async operations)
result = await cdp_send("Runtime.evaluate", {
    "expression": "await fetch('/api/data').then(r => r.json())",
    "awaitPromise": True,
    "returnByValue": True
})
```

#### Screenshots

```python
# Full page screenshot
screenshot = await cdp_send("Page.captureScreenshot", {
    "format": "png",
    "quality": 90,
    "captureBeyondViewport": True
})
# screenshot["data"] is base64 encoded

# Element screenshot (clip to bounding box)
box = await cdp_send("DOM.getBoxModel", {"nodeId": node_id})
quad = box["model"]["content"]
screenshot = await cdp_send("Page.captureScreenshot", {
    "format": "png",
    "clip": {
        "x": quad[0], "y": quad[1],
        "width": quad[2] - quad[0],
        "height": quad[5] - quad[1],
        "scale": 1
    }
})
```

#### Network Monitoring

```python
# Enable network events
await cdp_send("Network.enable", {})

# Set request interception
await cdp_send("Fetch.enable", {
    "patterns": [{"urlPattern": "*api*", "requestStage": "Request"}]
})

# Get all cookies
cookies = await cdp_send("Network.getAllCookies", {})
```

---

## Error Handling Guide

### Error Categories

| Category | HTTP-like Code | Description | Auto-Retry |
|----------|:--------------:|-------------|:----------:|
| `CDP_CONNECTION_LOST` | 503 | Browser process crashed or CDP socket closed | Yes (3x) |
| `CDP_TIMEOUT` | 504 | CDP command did not respond within timeout | Yes (2x) |
| `SELECTOR_NOT_FOUND` | 404 | CSS selector matched no elements in the DOM | No |
| `PAGE_NAVIGATION_FAILED` | 502 | Page returned an error status or failed to load | Yes (2x) |
| `JAVASCRIPT_ERROR` | 500 | Runtime.evaluate threw an exception | No |
| `TAB_CLOSED` | 410 | Target tab was closed before action completed | No |
| `RATE_LIMITED` | 429 | Too many requests to external service | Yes (backoff) |
| `PERMISSION_DENIED` | 403 | Action blocked by security policy | No |

### Retry Strategy

```python
# Default retry configuration
retry_config = {
    "max_retries": 3,
    "base_delay": 1.0,          # seconds
    "max_delay": 30.0,          # seconds
    "exponential_backoff": True,
    "jitter": True,             # add random 0-500ms to prevent thundering herd
    "retryable_errors": [
        "CDP_CONNECTION_LOST",
        "CDP_TIMEOUT",
        "PAGE_NAVIGATION_FAILED",
        "RATE_LIMITED",
    ]
}
```

### Error Recovery Patterns

```python
# Pattern 1: Reconnect on connection loss
try:
    result = await orchestrator.dispatch("bleu", "navigate", {"url": url})
except CDPConnectionLost:
    await orchestrator.reconnect_browser("chrome")
    result = await orchestrator.dispatch("bleu", "navigate", {"url": url})

# Pattern 2: Fallback selector
try:
    await orchestrator.click("#submit-button")
except SelectorNotFound:
    await orchestrator.click("button[type='submit']")
    # or: await orchestrator.click_by_text("Submit")

# Pattern 3: Wait and retry for dynamic content
for attempt in range(3):
    try:
        data = await orchestrator.scrape(".dynamic-content")
        break
    except SelectorNotFound:
        await asyncio.sleep(2 ** attempt)  # 1s, 2s, 4s
```

---

## Rate Limiting for Web Scraping

### Built-in Rate Limiter

The orchestrator includes a per-domain rate limiter to prevent IP bans and respect robots.txt:

```yaml
# config/rate_limits.yaml
rate_limits:
  default:
    requests_per_second: 2
    burst: 5
    cooldown_on_429: 60        # seconds to wait after a 429 response

  per_domain:
    linkedin.com:
      requests_per_second: 0.5  # LinkedIn is aggressive with rate limits
      burst: 2
      min_delay_between: 3      # minimum 3 seconds between requests

    mexc.com:
      requests_per_second: 5
      burst: 10

    codeur.com:
      requests_per_second: 1
      burst: 3

    github.com:
      requests_per_second: 3
      burst: 8
```

### Rate Limiter API

```python
from browser_orchestrator.rate_limiter import RateLimiter

limiter = RateLimiter(config="config/rate_limits.yaml")

# Check before making a request
if await limiter.allow("linkedin.com"):
    result = await orchestrator.dispatch("rouge", "navigate", {"url": url})
else:
    wait_time = await limiter.time_until_allowed("linkedin.com")
    print(f"Rate limited. Retry in {wait_time:.1f}s")

# The orchestrator applies rate limiting automatically when enabled
orchestrator = BrowserOrchestrator(rate_limiter=limiter)
```

---

## Proxy Configuration

### Supported Proxy Types

| Type | Protocol | Use Case |
|------|----------|----------|
| **HTTP** | `http://` | General web scraping |
| **HTTPS** | `https://` | Encrypted proxy tunnel |
| **SOCKS5** | `socks5://` | Full TCP tunneling, best anonymity |

### Configuration

```yaml
# config/proxy.yaml
proxy:
  enabled: false               # set to true to route through proxy
  type: socks5                 # http, https, socks5
  host: 127.0.0.1
  port: 1080
  username: null               # optional authentication
  password: null
  rotate: false                # rotate through proxy list
  proxy_list: null             # path to proxy list file for rotation
```

### Starting Chrome with Proxy

```bash
# HTTP proxy
google-chrome --remote-debugging-port=9222 \
    --proxy-server="http://proxy.example.com:8080"

# SOCKS5 proxy
google-chrome --remote-debugging-port=9222 \
    --proxy-server="socks5://127.0.0.1:1080"

# Proxy with authentication (set via PAC or extension)
google-chrome --remote-debugging-port=9222 \
    --proxy-pac-url="file:///path/to/proxy.pac"
```

### Proxy Rotation

For large-scale scraping, rotate through a list of proxies:

```python
from browser_orchestrator.proxy import ProxyRotator

rotator = ProxyRotator("config/proxy_list.txt")
# proxy_list.txt format: one proxy per line
# socks5://user:pass@host:port
# http://host:port

# Get next proxy
proxy = rotator.next()

# Mark a proxy as failed (removed from rotation temporarily)
rotator.mark_failed(proxy, cooldown=300)

# Get proxy stats
stats = rotator.stats()
# → {"total": 10, "active": 8, "failed": 2, "requests_served": 1523}
```

