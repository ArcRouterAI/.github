# ArcRouter — Intelligent LLM Routing

Route any prompt to the best AI model. 345+ models, 24 topic categories, benchmark-verified scores.

## Quick Start

```bash
# TypeScript SDK
npm install arcrouter

# MCP server for Claude Code / Cursor / Cline
claude mcp add arcrouter --transport http https://api.arcrouter.com/mcp

# Direct API
curl https://api.arcrouter.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Hello"}],"budget":"auto"}'
```

## How It Works

1. **Classify** — topic detection (code/math/science/writing/reasoning) + complexity scoring (SIMPLE/MEDIUM/COMPLEX/REASONING)
2. **Score** — 345+ models ranked by quality benchmarks (LiveBench, LiveCodeBench, HuggingFace)
3. **Route** — hybrid semantic routing: keyword prefilter → benchmark shortlist → embedding reranking
4. **Respond** — direct provider calls (OpenAI/Anthropic/Google/DeepSeek/xAI) with failover

## Repos

| Repo | Description |
|------|-------------|
| [arcrouter](https://github.com/ArcRouterAI/arcrouter) | Open-source prompt classifier — topic detection, complexity scoring, lossless compression |
| [arcrouter-sdk](https://github.com/ArcRouterAI/arcrouter-sdk) | TypeScript SDK — smart routing, council mode, x402 micropayments, workflow budgets |
| [arcrouter-mcp](https://github.com/ArcRouterAI/arcrouter-mcp) | MCP server — use ArcRouter from Claude Code, Cursor, Cline |
| [awesome-arcrouter](https://github.com/ArcRouterAI/awesome-arcrouter) | Community integrations and ecosystem links |

## Links

- **API:** https://api.arcrouter.com
- **Docs:** https://arcrouter.com/docs
- **Status:** https://arcrouter.com
