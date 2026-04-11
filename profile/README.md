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

- **Hybrid semantic routing** — lexical prefilter + benchmark shortlist + embedding reranking
- **24 topic categories** with subcategory detection (code/frontend, math/calculus, science/physics, ...)
- **4 complexity tiers** — SIMPLE, MEDIUM, COMPLEX, REASONING
- **5 direct providers** — OpenAI, Anthropic, Google, DeepSeek, xAI (with OpenRouter fallback)
- **Council mode** — query 3-7 models in parallel, return the consensus answer
- **x402 micropayments** — pay per request with USDC on Base, no API key needed

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
| [`arcrouter-mcp`](https://github.com/ArcRouterAI/arcrouter-mcp) | MCP server for AI coding tools | `claude mcp add arcrouter ...` |
| [awesome-arcrouter](https://github.com/ArcRouterAI/awesome-arcrouter) | Community integrations and resources | — |

## How It Works

```
Prompt → Classify (topic + complexity) → Score 345+ models → Semantic rerank → Route to best model
```

1. **Classify** — detect topic (code/math/science/writing/reasoning) and complexity (SIMPLE → REASONING)
2. **Score** — rank models using real benchmarks (LiveBench, LiveCodeBench, HumanEval, GPQA)
3. **Route** — hybrid semantic routing narrows to the optimal model for the task
4. **Respond** — direct provider call with automatic failover and circuit breaking

## Links

- **Website:** [arcrouter.com](https://arcrouter.com)
- **API:** [api.arcrouter.com](https://api.arcrouter.com)
- **Docs:** [arcrouter.com/docs](https://arcrouter.com/docs)
- **npm:** [@arcrouter/sdk](https://www.npmjs.com/package/@arcrouter/sdk) · [arcrouter-classifier](https://www.npmjs.com/package/arcrouter-classifier)
