![PanchangaAPI](https://api.moon-bot.cc/static/logo.png)

# PanchangaAPI

**Vedic Astrology API & MCP Server — 19 tools, Swiss Ephemeris precision**

The most accurate and complete Vedic astrology (Jyotish) API available. Purpose-built for AI agents, developers, and astro-applications. Swiss Ephemeris engine with Lahiri ayanamsha, sidereal zodiac, and true planetary positions.

**v4.0** — KP System, 300+ Yogas, Panchanga Search, Vrata Calendar, Remedies, and Ashtakavarga.

---

## Quick Start

### 1. Register

```bash
curl -X POST https://api.moon-bot.cc/register \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com"}'
```

You will receive a verification email. Click the link or use the PIN code to verify.

### 2. Get Your API Key

```bash
curl https://api.moon-bot.cc/register/status/acc_YOUR_ACCOUNT_ID
```

Returns your `api_key` once verified.

### 3. Make a Request

```bash
curl -X POST https://api.moon-bot.cc/panchanga \
  -H "X-API-Key: pnc_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"datetime": "2026-03-15T06:00:00+05:30", "latitude": 28.6139, "longitude": 77.2090}'
```

---

## Endpoints

| Method | Path | Credits | Description |
|--------|------|---------|-------------|
| POST | `/panchanga` | 1 | Complete Panchanga -- tithi, nakshatra, yoga, karana, vara + inauspicious periods (Rahu Kalam, Yamaganda, Gulika) |
| GET | `/panchanga` | 1 | Same via query parameters |
| POST | `/panchanga/range` | 1/day | Multi-day Panchanga |
| POST | `/panchanga/search` | 5 | **NEW** Search for specific Panchanga combinations (tithi+nakshatra+yoga) within a date range |
| POST | `/kundali` | 3 | Full birth chart -- Lagna, 9 planets, 12 houses, Navamsha, Dasha, Ashtakavarga, 300+ Yogas, Doshas |
| POST | `/kp` | 3 | **NEW** KP (Krishnamurthy Paddhati) System -- sub-lords, significators, cuspal analysis |
| POST | `/dasha` | 2 | Vimshottari Dasha -- Maha + Antar + Pratyantardasha with exact date ranges |
| POST | `/compatibility` | 5 | Ashtakoot 8-fold matching (36-point scale) |
| POST | `/muhurta` | 1 | Ranked auspicious timing windows with quality scores |
| POST | `/transits` | 2 | Planetary transits relative to natal Moon, Sade Sati detection |
| POST | `/vargas` | 3 | All 16 divisional charts (D1 through D60) |
| POST | `/shadbala` | 3 | Six-fold planetary strength with component breakdown |
| POST | `/bhava-chalit` | 3 | Bhava Chalit chart with house cusps and planet shifts |
| POST | `/prashna` | 2 | Horary (Prashna) astrology -- significators and indication scoring |
| POST | `/varshaphal` | 2 | Solar Return -- Muntha, Year Lord, Tajaka Yogas |
| POST | `/remedies` | 3 | **NEW** Personalized remedies -- gemstones, mantras, rituals based on chart weaknesses |
| GET | `/festivals/{year}` | 10 | 50+ Hindu festivals with astronomical basis |
| GET | `/festivals/{year}/{month}` | 1 | Monthly festival calendar |
| GET | `/vrata/{year}` | 5 | **NEW** Vrata (fasting) calendar -- Ekadashi, Pradosham, Chaturthi, Amavasya, Purnima |
| GET | `/ephemeris` | 1 | Raw planetary positions |

All calculation endpoints accept:

```json
{
  "datetime": "ISO-8601 with timezone, e.g. 2026-03-15T10:30:00+05:30",
  "latitude": 28.6139,
  "longitude": 77.2090
}
```

---

## What's New in v4.0

- **KP System (`/kp`)** -- Krishnamurthy Paddhati with sub-lord theory, significators, and ruling planets
- **300+ Yogas** -- Pancha Mahapurusha, Dhana, Raja, Daridra, Nabhas, and more detected in `/kundali`
- **Panchanga Search (`/panchanga/search`)** -- Find dates matching specific tithi, nakshatra, yoga combinations
- **Vrata Calendar (`/vrata/{year}`)** -- Complete fasting calendar with Ekadashi, Pradosham, Chaturthi dates
- **Remedies (`/remedies`)** -- Chart-based gemstone, mantra, and ritual recommendations
- **Ashtakavarga** -- Full Sarvashtakavarga and Prastarashtakavarga in Kundali output
- **Dosha Detection** -- Manglik, Kaal Sarp, Pitra, Grahan doshas in Kundali
- **Inauspicious Periods** -- Rahu Kalam, Yamaganda, Gulika Kalam in Panchanga
- **19 MCP tools** -- All endpoints available via MCP Streamable HTTP
- **425 tests** -- Comprehensive test coverage

---

## MCP Integration

PanchangaAPI is available as an MCP server for Claude Desktop, Cursor, and other MCP-compatible clients. **19 tools** covering all Vedic astrology calculations.

**Smithery:** [smithery.ai/servers/panchanga/api](https://smithery.ai/servers/panchanga/api)

### Claude Desktop

Add to your `claude_desktop_config.json`:

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

Add to your MCP settings:

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

For full MCP documentation, see [MCP.md](MCP.md).

---

## Payment Methods

### Free Tier

2 requests per day, all endpoints. Register and start using immediately -- no payment required.

### x402 USDC (Automatic)

Send a request without auth. Receive a `402 Payment Required` response with USDC payment instructions. Sign the payment (Base or Solana), retry with `PAYMENT-SIGNATURE` header. Fully automated, zero-friction, no registration needed.

Cost: **$0.03 per credit**.

### Telegram Stars

Purchase credits via [@vastr_bot](https://t.me/vastr_bot) using Telegram Stars. Deep link format:

```
https://t.me/vastr_bot?start=pay_{api_key}_{stars}
```

1 Telegram Star = 0.5 API credits.

### Crypto (NOWPayments)

Pay with 350+ cryptocurrencies (BTC, ETH, USDT, SOL, and more):

```
GET https://api.moon-bot.cc/checkout/{api_key}/{credits}
```

Credits are applied automatically after payment confirmation.

---

## Pricing

| Credits | Price | Per Credit |
|---------|-------|------------|
| Free tier | $0 | 2 requests/day |
| 100 | $3 | $0.03 |
| 500 | $15 | $0.03 |
| 1,000 | $30 | $0.03 |
| 5,000 | $150 | $0.03 |

---

## Use Cases

- **Daily horoscopes** -- Panchanga for tithi, nakshatra, yoga, karana
- **Birth chart readings** -- Full Kundali with 300+ Yogas, Dasha, Ashtakavarga
- **Compatibility matching** -- Ashtakoot 8-fold scoring for relationships
- **Event timing** -- Muhurta for weddings, business launches, travel
- **Annual predictions** -- Varshaphal with Tajaka Yogas
- **KP astrology** -- Sub-lord based predictions and ruling planet analysis
- **Financial astrology** -- Transit-based market signals, Dasha cycle analysis
- **Sports prediction** -- Prashna horary for event outcomes
- **Festival & Vrata calendars** -- Hindu festivals and fasting dates with precise astronomical timing
- **Remedial astrology** -- Personalized gemstone, mantra, and ritual recommendations

---

## Links

| Resource | URL |
|----------|-----|
| API Base URL | [api.moon-bot.cc](https://api.moon-bot.cc) |
| OpenAPI Spec | [api.moon-bot.cc/openapi.json](https://api.moon-bot.cc/openapi.json) |
| MCP Endpoint | [api.moon-bot.cc/mcp](https://api.moon-bot.cc/mcp) |
| Smithery | [smithery.ai/servers/panchanga/api](https://smithery.ai/servers/panchanga/api) |
| ClawHub Skill | [SKILL.md](SKILL.md) |
| Terms | [api.moon-bot.cc/terms](https://api.moon-bot.cc/terms) |

---

## License

[MIT](LICENSE)
