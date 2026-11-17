# BeatVig MCP: Sports Betting MCP Server for Sportsbook and Prediction-Market Prices in Claude and ChatGPT

BeatVig runs a paid, hosted MCP connector. Add it to Claude, ChatGPT or another MCP app and your assistant can read BeatVig's live NFL, NBA and MLB prices from sportsbooks such as DraftKings and FanDuel and from prediction markets such as Kalshi and Polymarket. It is built for people comparing venue prices, and it needs BeatVig Premium with MCP Access.

Updated 2026-11-17

## Server URL and how to connect

Server URL:

```
https://mcp.beatvig.com/mcp
```

Paste it exactly, with no trailing slash and no spaces. Sign-in uses OAuth: the app opens beatvig.com, you sign in and click Authorize once, and the app then reads the board as you. Menu names change between app releases, so the server URL and the Authorize button are what to look for. Only apps that support remote MCP servers over HTTP with OAuth sign-in can connect.

### Claude (claude.ai on Pro, Max, Team or Enterprise)

1. Open Settings, then under Customize open Connectors, then click Add.
2. Name it BeatVig and paste the server URL into Remote MCP server URL.
3. Click Continue. Leave the authentication options Claude has marked Detected as they are, then click Add.
4. Click Connect, sign in to beatvig.com if asked, and click Authorize.
5. Start a chat. The first time Claude uses a BeatVig tool, choose Always allow.

### ChatGPT (paid plan: Plus, Pro, Business or Enterprise)

1. Turn on Developer mode first: Settings, then Security and login, then scroll to the bottom and switch Developer mode on.
2. In Settings open Plugins. Close Settings, open Plugins in the main menu, and click the + button beside the search box.
3. Name it BeatVig, leave Connection on Server URL, paste the server URL, and leave Authentication on OAuth.
4. Tick the acknowledgement box, click Create, then Sign in with BeatVig and Authorize.
5. In a new chat, click the + at the left of the message box and switch BeatVig on.

### Claude Code

```
claude mcp add --transport http beatvig https://mcp.beatvig.com/mcp
```

Add `--scope user` to keep it in every project. Start Claude Code, run `/mcp`, select beatvig, choose Authenticate, sign in in the browser and click Authorize.

### Cursor

Open Cursor Settings, choose MCP, then Add new MCP server with the URL type, or paste this into `mcp.json`:

```json
{
  "mcpServers": {
    "beatvig": {
      "url": "https://mcp.beatvig.com/mcp"
    }
  }
}
```

Cursor opens your browser: sign in to BeatVig and click Authorize. Use the chat pane in Agent mode.

### Gemini CLI

```
gemini mcp add --transport http beatvig https://mcp.beatvig.com/mcp
```

The Gemini app itself does not take custom servers; the Gemini CLI does (it needs Node.js 20 or newer). Start `gemini`, run `/mcp` to confirm beatvig is listed, and ask a question. The first time, sign in to BeatVig in the browser and click Authorize.

### Other MCP apps

Add a remote server (HTTP, Streamable HTTP or URL, not a command or stdio server), name it `beatvig`, paste the server URL, then sign in to BeatVig in the browser window and click Authorize.

## Tools (14)

There are 14 tools, and all of them are read-only. The connector places no bets, and BeatVig accepts no wagers and holds no funds. A few tools return estimates, such as simulated fair prices and projection-based comparisons, and label them as estimates.

### Prices across venues

- `get_odds_comparison`: compares one bet across every sportsbook and every exchange. Returns each venue's quote on the same outcome, the best price and how far it sits from the median.
- `get_player_prop_prices`: lists every live prop market for one player, with every venue's quote and the player's recent hit rates against the line.
- `get_arbitrage`: finds positions where both sides can be backed at two venues for less than a certainty after fees. An empty list is the normal answer.
- `get_vig_by_venue`: ranks sportsbooks and prediction markets by what they charge on player props, with the two types listed separately.

### Prop edges and estimates

- `get_prop_edges`: lists player props where an exchange is priced below the fair price, with the fee-adjusted gap.
- `get_projection_picks`: ranks props by the gap between BeatVig's projection and the price on offer. The projection is an estimate.
- `get_prop_sims`: reads the prop simulator for NFL and NBA player props. The simulated prices are estimates.
- `get_prop_sim_accuracy`: reports how accurate the prop simulator has been on settled props.

### Movement, trends and screens

- `get_line_movement`: shows which player props have moved the most in the last hour, three hours or twelve hours.
- `get_hit_rate_screener`: screens today's props by how often the player has cleared the line over the last 5, 10 and 20 games.
- `get_team_trends`: shows how often a team has beaten the team-level markets this season, plus the next game and tonight's roster props.
- `get_defense_vs_position_props`: shows what each NFL or NBA defense allows to each position, with today's main prop line for players facing it.

### Reports and alerts

- `get_weekly_price_report`: returns the weekly report on how often prediction markets had the better price than sportsbooks, by sport and market.
- `get_alert_history`: returns your own recent BeatVig alerts, newest first. It only returns the signed-in member's own history.

## Example questions

- "Where is Kalshi cheaper than DraftKings on NFL passing yards right now?" (`get_odds_comparison`)
- "Is there an arbitrage between Kalshi and DraftKings right now?" (`get_arbitrage`)
- "Which NFL props moved the most in the last three hours?" (`get_line_movement`)
- "Which venue charges the least on NBA player props?" (`get_vig_by_venue`)
- "How often did Kalshi beat the sportsbooks last week?" (`get_weekly_price_report`)

## Price

MCP Access is $60 a year, on top of BeatVig Premium. You need both to connect. Current plans are on the premium page: https://beatvig.com/premium

## Learn more

- Sports betting MCP server: https://beatvig.com/sports-betting-mcp
- Every tool, with what it returns and a question to ask: https://beatvig.com/sports-betting-mcp/tools
- Kalshi and Polymarket in Claude and ChatGPT: https://beatvig.com/kalshi-mcp
- Site: https://beatvig.com

BeatVig is not affiliated with, endorsed by, or an official product of Kalshi or Polymarket. Claude and ChatGPT are products of Anthropic and OpenAI, and BeatVig is not affiliated with either.

## This repository

This repository is documentation only. BeatVig hosts the MCP server behind a paid BeatVig login, so there is no code here to install or run. Contact: admin@beatvig.com
