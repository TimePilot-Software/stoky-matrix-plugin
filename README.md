# Stoky Matrix

Stoky Matrix is a market knowledge graph built by Stoky. It holds companies, industries, themes and regions, the relationships between them, their history, and the sources behind each entry. This plugin gives Claude read-only access to Stoky Matrix, so you can research a company or theme and check where each claim came from.

## Requirements

- A Stoky Pro account.
- Stoky Basics accounts cannot connect. The connection page that appears after sign-in says so, and nothing is connected.

## Install and connect

1. Install the `stoky-matrix` plugin from Claude's plugin directory. In Claude Code you can also add this repository as a marketplace and install from it:

   ```bash
   claude plugin marketplace add TimePilot-Software/stoky-matrix-plugin
   claude plugin install stoky-matrix@stoky
   ```

2. Installing the plugin adds the `stoky-matrix` MCP server and the `matrix-research` skill. The plugin sets the server address, `https://mcp.stoky.ai/mcp`, for you. You do not need to enter it.
3. The first time Claude uses Stoky Matrix, a browser window opens. Sign in to Stoky with your email, Google or Apple account, then choose Allow.

No API key or token needs to be copied. Allowing the connection gives Claude read-only access to Stoky Matrix research.

## What you can ask

- "Research NVIDIA in Matrix. Resolve the ticker, read its risk factors and competitive position sections, and cite the source for each claim."
- "What did Matrix say about Apple on a date three months ago, and what changed by today? Compare the two snapshots and list the differences with their citations."
- "What has happened recently for AMD? Show its changelog and recent event stream, and say which sources support each item."

## Tools

All tools are read-only.

| Tool | What it does |
|---|---|
| `matrix_status` | Shows how fresh the Matrix data is, with entity and link counts and whether semantic search is available. |
| `resolve_ticker` | Matches a ticker or company name to one Matrix entity, with the match method and a confidence. |
| `find_entities` | Finds entities from names, tickers or themes, using exact and semantic matches. |
| `get_entity_tree` | Lists what an entity contains (sections and topics, sizes, last updates) without the text. Use it before reading. |
| `read_entity` | Reads an entity's profile, or selected sections and topics, with citation IDs on the claims that have them. |
| `get_neighbors` | Lists related entities. Typed relationships come with a plain-language explanation; some neighbors are weaker co-mention or similarity links with no typed relationship. |
| `find_path` | Looks for a strong chain of relationships between two entities, up to four steps. The search is bounded, so no result does not prove there is no link. |
| `get_sentiment` | Shows retail social discussion for entities: stance, score, confidence and top threads. |
| `get_citations` | Pages through the citation records for entities: entity, relationship, sentiment and fact sources. |
| `get_market_pulse` | Lists recent changes across Matrix: recently updated entities and sentiment spikes. |
| `get_entity_changelog` | Shows recent changes to an entity from Matrix's git history, including which sections changed. |
| `get_facts` | Lists timestamped facts with their sources for entities, when a fact store is connected. |
| `get_matrix_snapshot` | Shows what Matrix recorded for entities on a given date or commit. |
| `diff_matrix` | Compares Matrix between two dates or commits and lists what changed. |
| `get_event_stream` | Pages through the raw, time-ordered event log before the writer consolidates it. |

## Limits and accuracy

- The plugin is read-only. It cannot change Matrix or your Stoky account.
- Answers are written by the AI from sourced Matrix entries. They can be wrong. Open the cited source before you rely on anything that matters.
- Fact citations from `get_citations` cover the newest 200 facts in the requested window. When `facts_capped` is true, older facts in that window were left out; null means facts were not requested or could not be loaded.
- Some data layers depend on how the service is set up. Facts and the event stream may be unavailable. The tools say so when that happens.
- Matrix has no live prices.
- Access is granted for one hour at a time and your AI app renews it in the background. You need to connect again if it is not renewed for 30 days, or if the account is not on a paid plan when it is renewed. If the plan lapsed, restore Stoky Pro before reconnecting.
- This is information and research only. It is not investment advice.

## Troubleshooting

- **The sign-in window does not open.** Check that a browser can open on this computer and that pop-up windows are not blocked. Then ask Claude to try again.
- **The connection page says Stoky Matrix is part of Stoky Pro.** Your account is on Stoky Basics. Upgrade to Stoky Pro at https://www.stoky.ai, then connect again.
- **Claude reports "Unauthorized", or the connection stops working.** The connection has expired or was revoked. Sign in to `stoky-matrix` again from Claude's MCP or connector settings.
- **"You have hit the maximum rate limit for Matrix MCP requests."** Wait a minute, then try again.

## Privacy and support

- Privacy policy: https://www.stoky.ai/privacy
- Terms: https://www.stoky.ai/terms
- Website: https://www.stoky.ai
- Support: contact@stoky.ai

The connector sees the tool requests your AI app sends to Stoky Matrix, and your Stoky account identity for sign-in. It does not read your Claude conversations, memory or files.
