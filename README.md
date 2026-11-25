# Frontier MCP server

Frontier gives AI assistants an open index of new research from the top journals (Nature, Science, Cell, NEJM, The Lancet, PNAS and their families), scored against its primary sources and updated daily, plus the citation impact of **any** paper or researcher, read live from [OpenAlex](https://openalex.org).

- **Server URL:** `https://frontierresearch.co/api/mcp` (remote, Streamable HTTP)
- **Authentication:** none. Public, read-only data; no account or API key.
- **Docs and setup:** [frontierresearch.co/assistants](https://frontierresearch.co/assistants)
- **Official MCP Registry:** `co.frontierresearch/frontier`

## What you can ask

| Tool | What it does | Try asking |
|------|--------------|------------|
| `latest_breakthroughs` | What Frontier added in the last days, optionally in one field | "What's new in neuroscience research this week?" |
| `search_breakthroughs` | Search the index by topic, ranked by Frontier Score or newest first | "Find recent high-impact papers on CRISPR gene editing." |
| `get_breakthrough` | One entry in full: why it matters, authors, score breakdown and sources | "Explain the Frontier entry W7221139068." |
| `check_paper` | Any paper's citations, field-weighted citation impact (FWCI), citation percentile and retraction or correction status | "What is the FWCI of 10.1038/s41586-026-11174-3, and has it been retracted?" |
| `check_researcher` | A researcher's record by ORCID iD or OpenAlex author id: papers, citations, h-index, mean FWCI, top 10% papers | "What is the h-index of the researcher with ORCID 0000-0001-9609-4600?" |
| `list_fields` | The fields the index covers | "Which fields does Frontier cover?" |
| `explain_frontier_score` | How the Frontier Score is built | "How does Frontier score a paper?" |

Every tool is read-only (`readOnlyHint: true`). Every answer links to its page on frontierresearch.co, where each figure is shown with its source, and to the paper's DOI.

## Connect it

**Claude (web and desktop):** Settings, Connectors, Add custom connector. Name it Frontier, paste `https://frontierresearch.co/api/mcp`, leave authentication empty.

**Claude Code:**

```bash
claude mcp add --transport http frontier https://frontierresearch.co/api/mcp
```

**Cursor, Windsurf, Cline and other MCP clients:**

```json
{ "mcpServers": { "frontier": { "url": "https://frontierresearch.co/api/mcp" } } }
```

**ChatGPT:** with developer mode on (Settings, Apps, Advanced settings), create an app with the server URL and no authentication.

## Data and limits

- Figures come from OpenAlex (CC0), with Crossref, Europe PMC and OpenCitations for corrections and citations. FWCI compares a paper's citations with papers of the same field, year and type, so 1.0 is the world average.
- An author profile can hold another person's paper, and scores of very recent papers are early signals that move as citations arrive.
- Paper and researcher checks are limited to 30 an hour per connection, since each reads OpenAlex live.
- The server stores no prompts or answers: [privacy policy](https://frontierresearch.co/legal/privacy).

## About

Frontier is operated by O-mega Enterprise, Inc. Questions: hello@frontierresearch.co. This repository documents the hosted server; the server itself runs at frontierresearch.co.
