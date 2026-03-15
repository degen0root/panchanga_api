# MCP Integration Guide

PanchangaAPI implements the Model Context Protocol (MCP) via Streamable HTTP transport, making all 16 Vedic astrology tools available to MCP-compatible clients.

## Endpoint

```
POST https://api.moon-bot.cc/mcp
```

**Protocol:** JSON-RPC 2.0 over Streamable HTTP

**Authentication:** `X-API-Key` header with your API key

**Session:** Server returns `Mcp-Session-Id` header on `initialize` -- include it in subsequent requests.

---

## Client Configuration

### Claude Desktop

Add to `~/.config/claude/claude_desktop_config.json` (Linux) or `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS):

```json
{
  "mcpServers": {
    "panchanga": {
      "url": "https://api.moon-bot.cc/mcp",
      "headers": {
        "X-API-Key": "pnc_YOUR_KEY"
      }
    }
  }
}
```

### Cursor

Add to your Cursor MCP settings (Settings > MCP Servers):

```json
{
  "panchanga": {
    "url": "https://api.moon-bot.cc/mcp",
    "headers": {
      "X-API-Key": "pnc_YOUR_KEY"
    }
  }
}
```

### Smithery

Install directly from Smithery:

[smithery.ai/servers/panchanga/api](https://smithery.ai/servers/panchanga/api)

---

## Available Tools

All tools accept `datetime` (ISO-8601 with timezone), `latitude`, and `longitude` parameters unless noted otherwise.

| Tool Name | Description | Credits |
|-----------|-------------|---------|
| `panchanga.daily` | Complete Panchanga -- tithi, nakshatra, yoga, karana, vara, sunrise/sunset | 1 |
| `panchanga.range` | Multi-day Panchanga for a date range | 1/day |
| `kundali.birthchart` | Full birth chart -- Lagna, planets, houses, Navamsha, Dasha, Ashtakavarga, Yogas | 3 |
| `dasha.vimshottari` | Vimshottari Dasha timeline -- Maha + Antar + Pratyantardasha | 2 |
| `compatibility.ashtakoot` | Ashtakoot 8-fold matching for two birth charts (36-point scale) | 5 |
| `muhurta.find` | Find ranked auspicious timing windows with quality scores | 1 |
| `transits.current` | Planetary transits relative to natal Moon, Sade Sati detection | 2 |
| `vargas.divisional` | All 16 divisional charts (D1 through D60) | 3 |
| `shadbala.strength` | Six-fold planetary strength with component breakdown | 3 |
| `bhavachalit.houses` | Bhava Chalit chart with house cusps and planet shifts | 3 |
| `prashna.horary` | Horary astrology -- significators, indication scoring, guidance | 2 |
| `varshaphal.annual` | Solar Return -- Muntha, Year Lord, Tajaka Yogas | 2 |
| `festivals.year` | 50+ Hindu festivals for a given year | 10 |
| `festivals.month` | Monthly festival calendar | 1 |
| `ephemeris.positions` | Raw planetary positions at a given time and place | 1 |
| `account.info` | Check balance, usage, and tier | free |

---

## Protocol Flow

### 1. Initialize

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2025-03-26",
    "capabilities": {},
    "clientInfo": {
      "name": "my-client",
      "version": "1.0.0"
    }
  }
}
```

### 2. List Tools

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "tools/list"
}
```

### 3. Call a Tool

```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "method": "tools/call",
  "params": {
    "name": "panchanga.daily",
    "arguments": {
      "datetime": "2026-03-15T06:00:00+05:30",
      "latitude": 28.6139,
      "longitude": 77.2090
    }
  }
}
```

---

## Prompts

The server exposes an `x402-setup` prompt via `prompts/list` and `prompts/get` that explains the x402 USDC auto-payment flow for agents with crypto wallets.

---

## Getting an API Key

Register for free (2 requests/day):

```bash
curl -X POST https://api.moon-bot.cc/register \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com"}'
```

Purchase credits via [NOWPayments crypto](https://api.moon-bot.cc/checkout/{api_key}/{credits}), [Telegram Stars](https://t.me/vastr_bot), or x402 USDC auto-payment.
