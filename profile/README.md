<div align="center">

# ArcRouter

**Intelligent LLM routing. One API, 345+ models, always the best one.**

Route any prompt to the optimal AI model based on topic, complexity, and budget — with benchmark-verified selection across OpenAI, Anthropic, Google, DeepSeek, and xAI.

[![Website](https://img.shields.io/badge/arcrouter.com-visit-blue?style=flat-square)](https://arcrouter.com)
[![Docs](https://img.shields.io/badge/docs-arcrouter.com%2Fdocs-green?style=flat-square)](https://arcrouter.com/docs)
[![npm @arcrouter/sdk](https://img.shields.io/npm/v/@arcrouter/sdk?label=%40arcrouter%2Fsdk&style=flat-square&color=cb3837)](https://www.npmjs.com/package/@arcrouter/sdk)
[![npm arcrouter-classifier](https://img.shields.io/npm/v/arcrouter-classifier?label=arcrouter-classifier&style=flat-square&color=cb3837)](https://www.npmjs.com/package/arcrouter-classifier)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow?style=flat-square)](https://opensource.org/licenses/MIT)

</div>

---

## Why ArcRouter?

LLMs vary wildly in quality by task. GPT-4o dominates coding, Gemini excels at long context, DeepSeek leads math reasoning. ArcRouter picks the right model for every prompt — automatically.

### Smart Routing
- **Hybrid semantic routing** — lexical prefilter + benchmark shortlist + embedding reranking
- **24 topic categories** with subcategory detection (code/frontend, math/calculus, science/physics, ...)
- **4 complexity tiers** — SIMPLE, MEDIUM, COMPLEX, REASONING
- **Agentic detection** — auto-detects tool-use prompts, routes to tool-capable models
- **345+ models scored** with real benchmarks (LiveBench, LiveCodeBench, HumanEval, GPQA)

### Multi-Model Verification
- **Council mode** — query 3-7 models in parallel, return the consensus answer
- **Semantic grouping** — embedding similarity (paid) or Jaccard overlap (free) to find agreement
- **Chairman escalation** — when models disagree, a synthesis model resolves conflicts

### Agent Workflow Support
- **X-Agent-Step header** — hint complexity per step (`simple-action`, `code-generation`, `reasoning`, `verification`)
- **Workflow budgets** — set a total USD budget per workflow, auto-downgrade at 60/80/95% spend
- **Session model pinning** — lock a model for a conversation via `session_id`
- **Workflow telemetry** — `GET /v1/workflow/{session_id}/usage` for spend, latency, tier distribution

### Cost Optimization
- **Prompt compression** — lossless L1 (dedup) + L2 (whitespace) + L5 (JSON compaction), 10-15% token savings
- **5 direct providers** — OpenAI, Anthropic, Google, DeepSeek, xAI (no middleman markup)
- **OpenRouter fallback** — 300+ long-tail models when direct access isn't available
- **Max cost filtering** — `max_cost` per request, graceful downgrade to cheapest viable model
- **Routing metadata** — every response includes `estimated_cost_usd`, `savings_vs_gpt4_pct`, `models_considered`

### Reliability
- **Circuit breaker + fallback chains** — auto-retry with up to 3 fallback models on failure
- **Context-length filtering** — excludes models with insufficient context window
- **Model exclusion** — `exclude_models` to block specific models per request

### Payments
- **MPP (Machine Payments Protocol)** — pay per request via USDC.e on Tempo. Sub-cent fees, 500ms finality. Standards-based RFC 7235 auth headers. Built by Tempo + Stripe. See [mpp.dev](https://mpp.dev).
- **x402 micropayments** — pay per request with USDC on Base, no API key needed
- **Stripe metered billing** — traditional API key billing for teams
- **Free tier** — no auth required, free models, rate-limited
- **Discovery endpoint** — `GET /openapi.json` advertises payment methods + pricing for agent auto-discovery

### Developer Experience
- **Model aliases** — `"claude"`, `"gpt"`, `"gemini"`, `"deepseek"` instead of full model IDs
- **OpenAI-compatible API** — drop-in replacement, same `/v1/chat/completions` format
- **Streaming** — SSE streaming with routing metadata in the first chunk
- **Usage tracking** — `GET /v1/usage` for per-key daily stats

## Quick Start

```bash
# TypeScript SDK
pnpm add @arcrouter/sdk

# MCP server for Claude Code / Cursor / Cline
claude mcp add arcrouter --transport http https://api.arcrouter.com/mcp

# Direct API (no auth required for free tier)
curl https://api.arcrouter.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Hello"}],"budget":"auto"}'
```

```typescript
import { ArcRouter } from '@arcrouter/sdk';

const arc = new ArcRouter();
const res = await arc.chat('Explain quantum entanglement');

console.log(res.content);           // The answer
console.log(res.routing.model);     // e.g. "gemini-2.0-flash"
console.log(res.routing.topic);     // "science/physics"
console.log(res.routing.complexity);// "MEDIUM"
```

## Ecosystem

| Package | Description | Install |
|---------|-------------|---------|
| [`@arcrouter/sdk`](https://github.com/ArcRouterAI/arcrouter-sdk) | TypeScript SDK — routing, council, streaming, workflows, x402 | `pnpm add @arcrouter/sdk` |
| [`arcrouter-classifier`](https://github.com/ArcRouterAI/arcrouter) | Open-source prompt classifier — topic, complexity, compression | `pnpm add arcrouter-classifier` |
| [`arcrouter-mcp`](https://github.com/ArcRouterAI/arcrouter-mcp) | MCP server for AI coding tools (3 tools: chat, models, health) | `claude mcp add arcrouter ...` |
| [awesome-arcrouter](https://github.com/ArcRouterAI/awesome-arcrouter) | Community integrations and resources | — |

## How It Works

```
Prompt → Classify (topic + complexity + agentic) → Score 345+ models → Semantic rerank → Route → Fallback chain
```

1. **Classify** — detect topic (24 categories), complexity (4 tiers), agentic intent, and confidence
2. **Score** — rank models using real benchmarks, weighted by semantic relevance + value + reliability
3. **Route** — hybrid semantic routing narrows to optimal model, filtered by budget + context length + cost
4. **Respond** — direct provider call with circuit breaker, up to 3 fallback models on failure
5. **Compress** — lossless prompt compression on long conversations (>5000 chars) to reduce token cost

## Links

- **Website:** [arcrouter.com](https://arcrouter.com)
- **API:** [api.arcrouter.com](https://api.arcrouter.com)
- **Docs:** [arcrouter.com/docs](https://arcrouter.com/docs)
- **npm:** [@arcrouter/sdk](https://www.npmjs.com/package/@arcrouter/sdk) · [arcrouter-classifier](https://www.npmjs.com/package/arcrouter-classifier)
