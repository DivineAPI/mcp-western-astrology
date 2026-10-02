# Western Astrology MCP Server (Natal Chart, Synastry, Transits) by DivineAPI

![Western Astrology MCP Server by DivineAPI](https://raw.githubusercontent.com/DivineAPI/DivineAPI/main/assets/mcp-western-astrology.png)

Connect Claude, Cursor, VS Code or any MCP client to DivineAPI's Western astrology data: natal charts, synastry, transits, composite charts, progressions, planetary returns and prenatal charts, returned as JSON (and SVG for wheel charts).

[![Docs](https://img.shields.io/badge/docs-developers.divineapi.com-blue)](https://developers.divineapi.com/western-api)
[![Trial](https://img.shields.io/badge/14--day%20trial-start-green)](https://divineapi.com/start-trial)
[![MCP](https://img.shields.io/badge/MCP-streamable%20HTTP-purple)](https://divineapi.com/mcp)
[![PyPI](https://img.shields.io/badge/pypi-divineapi--western--astrology--mcp-orange)](https://pypi.org/project/divineapi-western-astrology-mcp/)
[![Status](https://img.shields.io/badge/status-status.divineapi.com-brightgreen)](https://status.divineapi.com)
[![License: MIT](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)

Hosted server URL:

```
https://mcp.divineapi.com/western/mcp
```

One-click install (adds the hosted server with placeholder credentials):

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=divineapi-western-astrology&config=eyJ1cmwiOiJodHRwczovL21jcC5kaXZpbmVhcGkuY29tL3dlc3Rlcm4vbWNwIiwiaGVhZGVycyI6eyJYLURpdmluZS1BcGktS2V5IjoiWU9VUl9BUElfS0VZIiwiWC1EaXZpbmUtQXV0aC1Ub2tlbiI6IllPVVJfQVVUSF9UT0tFTiJ9fQ%3D%3D)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=divineapi-western-astrology&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.divineapi.com%2Fwestern%2Fmcp%22%2C%22headers%22%3A%7B%22X-Divine-Api-Key%22%3A%22YOUR_API_KEY%22%2C%22X-Divine-Auth-Token%22%3A%22YOUR_AUTH_TOKEN%22%7D%7D)

After installing, replace `YOUR_API_KEY` and `YOUR_AUTH_TOKEN` in the server's headers with your own values. In VS Code you can use the `inputs` version of the config below instead, so the values are stored securely.

## Connect in 1 minute

**1. Get your credentials.** Start the [14-day free trial](https://divineapi.com/start-trial) (credit card required to activate the trial), then copy your **API key** and **auth token** from the DivineAPI dashboard.

**2. Add the server to your client.** The hosted server accepts your credentials in one of two ways:

- **Request headers:** `X-Divine-Api-Key` and `X-Divine-Auth-Token` (Cursor, VS Code, Claude Code).
- **Sign-in page (OAuth):** the client opens a DivineAPI page where you paste the API key and auth token once (Claude.ai and Claude Desktop custom connectors).

### Claude.ai and Claude Desktop (custom connector)

Custom connectors added in Claude.ai also appear in Claude Desktop.

1. Open **Customize > Connectors**, click **+ Add**, then **Add custom connector**.
2. Name: `DivineAPI Western Astrology`. URL: `https://mcp.divineapi.com/western/mcp`. Click **Continue**.
3. Keep the detected sign-in settings and click **Add**. When you connect, a DivineAPI sign-in page opens: paste your API key and auth token and click **Connect**.

If your Claude plan offers request headers for custom connectors, you can instead choose no sign-in and add the two headers `X-Divine-Api-Key` and `X-Divine-Auth-Token`.

Team and Enterprise plans: an owner adds the connector under **Organization settings > Connectors** first. Steps from [Claude's custom connector guide](https://support.claude.com/en/articles/11175166).

### Cursor

`~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "divineapi-western-astrology": {
      "url": "https://mcp.divineapi.com/western/mcp",
      "headers": {
        "X-Divine-Api-Key": "YOUR_API_KEY",
        "X-Divine-Auth-Token": "YOUR_AUTH_TOKEN"
      }
    }
  }
}
```

### VS Code (GitHub Copilot agent mode)

`.vscode/mcp.json`. VS Code asks for both values on first start and stores them securely:

```json
{
  "inputs": [
    { "type": "promptString", "id": "divine-api-key", "description": "DivineAPI API key", "password": true },
    { "type": "promptString", "id": "divine-auth-token", "description": "DivineAPI auth token", "password": true }
  ],
  "servers": {
    "divineapi-western-astrology": {
      "type": "http",
      "url": "https://mcp.divineapi.com/western/mcp",
      "headers": {
        "X-Divine-Api-Key": "${input:divine-api-key}",
        "X-Divine-Auth-Token": "${input:divine-auth-token}"
      }
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport http divineapi-western-astrology https://mcp.divineapi.com/western/mcp \
  --header "X-Divine-Api-Key: YOUR_API_KEY" \
  --header "X-Divine-Auth-Token: YOUR_AUTH_TOKEN"
```

Run `/mcp` inside Claude Code to check the connection.

### Clients that send only one credential field

If a client can send only a single bearer token and no custom headers, send `Authorization: Bearer YOUR_API_KEY:YOUR_AUTH_TOKEN` (API key, a colon, then the auth token). The server splits it into the two credentials.

## Example prompts

- "I was born on 24 May 1990 at 14:40 in New Delhi. Draw my natal wheel chart and list my planets, houses and aspects (Placidus)."
- "Compare my chart with my partner's: show the synastry aspect table and the emotional and financial compatibility readings."
- "Which transits hit my natal chart this week? Use Saturn as the transit planet."
- "Build our composite chart and list its planetary positions."
- "When is my next Saturn return, and what are its details?"
- "Show my secondary progressions and progressed lunar events for this year."

## Tool groups

Tool counts below are counted from the `@mcp.tool` definitions in [`server.py`](server.py) of this repository (version 1.5.0). The hosted server is updated more often and can list more tools; your MCP client always shows the live list.

| Group | Tools | What they cover | Host |
|---|---|---|---|
| Natal | 10 | Planetary positions, house cusps, aspect table, natal wheel chart (SVG), general sign report, general house report, Moon phases, ascendant report, Moon phase calendar, natal insights | astroapi-4 (wheel on astroapi-8) |
| Synastry | 13 | Planetary positions and house cusps for both people, bi-wheel chart, inter-chart aspect table, harmonious / conflicting / contrasting / intense aspect readings, physical, emotional, sexual, spiritual and financial compatibility | astroapi-4 (wheel and aspect table on astroapi-8) |
| Transits | 12 | Basic transit, custom transit (any moment and place), daily, weekly and monthly transits, transit house overlay, full transit, retrograde and combustion transits, transit wheel chart, transit planetary positions, planetary ingress | astroapi-4 and astroapi-8 |
| Composite | 4 | Composite planetary positions, house cusps, aspect table, wheel chart | astroapi-8 |
| Advanced natal | 11 | Arabic lots, asteroid positions, fixed stars list and details, planetary midpoints, eclipses, declinations and parallels, aspect patterns, chart shape, other minor bodies, dominants | astroapi-8 |
| Progressions and returns | 5 | Planet returns list and return details, progressed lunar events, planetary arc directions, secondary progressions | astroapi-8 |
| Prenatal | 2 | Prenatal list and prenatal details | astroapi-8 |

All tools are read-only (`readOnlyHint: true`) and each tool call makes one request to the DivineAPI REST API.

### Inputs the model needs to know

- Dates are separate `day`, `month`, `year` fields plus `hour`, `min`, `sec` (send `sec` as `0` if unknown).
- `place` is a plain lowercase city string; `lat` and `lon` are decimals; `tzone` is a decimal UTC offset (for example `-5` or `5.5`), not a zone name.
- Calculations are tropical. `house_system` defaults to `placidus` and accepts `placidus`, `koch`, `porphyry`, `regiomontanus`, `campanus`, `equal`, `whole-sign`, `morinus`, `alcabitius` or the single-letter codes `B, C, E, K, M, O, P, R, W`.
- Two-person tools (synastry, composite) take a birth block for each person.
- Two-step tools: `divine_western_planet_return_details` needs a `return_key` from `divine_western_planet_returns_list`; `divine_western_prenatal_details` needs a `prenatal_key` from `divine_western_prenatal_list`; `divine_western_fixed_stars_details` needs star names from `divine_western_fixed_stars_list`.
- `divine_western_dominants` needs `method`: `TRADITIONAL` or `MODERN`.
- Transit tools need the transit date (and, for weekly, monthly and full reports, a `transit_planet`).
- `lan` sets the response language. Western text reports support 12 languages: `en`, `hi`, `ja`, `ru`, `pt`, `es`, `fr`, `de`, `it`, `nl`, `pl`, `tr`.

## Self-hosting

You only need this if you want to run the server yourself instead of using the hosted URL. The server reads your credentials from two environment variables: `DIVINE_API_KEY` and `DIVINE_AUTH_TOKEN`.

### Local (stdio) with uv or pip

```bash
# uv (no install step)
uvx divineapi-western-astrology-mcp

# or pip
pip install divineapi-western-astrology-mcp
divineapi-western-astrology-mcp
```

Claude Desktop local config (`claude_desktop_config.json`; on macOS `~/Library/Application Support/Claude/`, on Windows `%APPDATA%\Claude\`):

```json
{
  "mcpServers": {
    "divineapi-western-astrology": {
      "command": "uvx",
      "args": ["divineapi-western-astrology-mcp"],
      "env": {
        "DIVINE_API_KEY": "YOUR_API_KEY",
        "DIVINE_AUTH_TOKEN": "YOUR_AUTH_TOKEN"
      }
    }
  }
}
```

To run exactly this repository's code:

```bash
git clone https://github.com/DivineAPI/mcp-western-astrology.git
cd mcp-western-astrology
pip install .
DIVINE_API_KEY=YOUR_API_KEY DIVINE_AUTH_TOKEN=YOUR_AUTH_TOKEN divineapi-western-astrology-mcp
```

### Remote (streamable HTTP) with Docker

```bash
docker build -t divineapi-western-mcp .
docker run -p 8000:8000 -e MCP_JWT_SECRET=a-long-random-string divineapi-western-mcp
```

The MCP endpoint is then `http://localhost:8000/mcp`. Clients send their own `X-Divine-Api-Key` and `X-Divine-Auth-Token` headers. `docker compose up` maps the same server to port 8002 and passes the variables below from your shell.

| Variable | Used for |
|---|---|
| `DIVINE_API_KEY`, `DIVINE_AUTH_TOKEN` | Your DivineAPI credentials. Required in stdio mode; in HTTP mode, per-request headers or the sign-in page override them |
| `MCP_TRANSPORT` | `stdio` (default) or `http` (set by the Dockerfile) |
| `MCP_HOST` | Public host name for the OAuth sign-in flow and allowed hosts (default `mcp.divineapi.com`) |
| `MCP_JWT_SECRET` | Secret that signs session tokens. Set a fixed value so sign-ins survive restarts |

The OAuth sign-in flow expects HTTPS on `MCP_HOST` behind a reverse proxy that serves the server under `/western/`. Header authentication works without it.

## Which plan includes this

The tools call the Western endpoints, so they use your **Western plan** (Western Nova, Western Atlas or Western Lumen); a tool works when your plan includes its endpoint. Compare plans at [divineapi.com/pricing](https://divineapi.com/pricing).

## FAQ

**Do I need a DivineAPI account to use the Western tools?**
Yes. Natal, synastry and transit tools call the Western REST endpoints with your API key and auth token, so a tool works when your Western plan includes its endpoint. Start with the [14-day free trial](https://divineapi.com/start-trial) (credit card required to activate the trial); plans and prices are at [divineapi.com/pricing](https://divineapi.com/pricing).

**Which MCP clients can draw a natal chart with it?**
Clients with remote MCP support over streamable HTTP, such as Claude.ai, Claude Desktop, Claude Code, Cursor and VS Code. For a local-only client, `uvx divineapi-western-astrology-mcp` starts the same tools over stdio and reads `DIVINE_API_KEY` and `DIVINE_AUTH_TOKEN`.

**Tropical or sidereal?**
Tropical, calculated with Swiss Ephemeris. For sidereal (Vedic) charts use the [Vedic astrology MCP server](https://github.com/DivineAPI/mcp-indian-astrology).

**Can it draw wheel charts?**
Yes. The natal, synastry (bi-wheel), transit and composite wheel tools return chart images.

**My client lists synastry or transit tools that are not in the table. Why?**
The table was counted from version 1.5.0 of this repository's `server.py`. The hosted server and the PyPI package can be newer.

**I want the REST API, not MCP.**
Use the [birth-chart-api](https://github.com/DivineAPI/birth-chart-api) repo or the [API reference](https://developers.divineapi.com/western-api). SDKs: `pip install divineapi`, `npm install divineapi`, `composer require divineapi/divineapi`.

## Related repos

| Repo | What it is |
|---|---|
| [birth-chart-api](https://github.com/DivineAPI/birth-chart-api) | Western birth chart / natal chart REST API quickstart |
| [astrology-api](https://github.com/DivineAPI/astrology-api) | Overview of all DivineAPI domains |
| [mcp-indian-astrology](https://github.com/DivineAPI/mcp-indian-astrology) | Vedic astrology MCP server |
| [mcp-horoscope-numerology](https://github.com/DivineAPI/mcp-horoscope-numerology) | Horoscope, tarot and numerology MCP server |
| [divineapi-python](https://github.com/DivineAPI/divineapi-python) | Python SDK (`pip install divineapi`) |
| [divineapi-node](https://github.com/DivineAPI/divineapi-node) | Node.js / TypeScript SDK (`npm install divineapi`) |
| [divineapi-php](https://github.com/DivineAPI/divineapi-php) | PHP SDK (`composer require divineapi/divineapi`) |

## Support

- MCP overview: [divineapi.com/mcp](https://divineapi.com/mcp)
- API reference: [developers.divineapi.com/western-api](https://developers.divineapi.com/western-api)
- Help center: [support.divineapi.com](https://support.divineapi.com)
- API status: [status.divineapi.com](https://status.divineapi.com)

## License

MIT. See [LICENSE](LICENSE).
