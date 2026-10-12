# Agentic AI Portfolio — 12 Production-Grade Patterns

**"If you can build these 12 Agentic AI projects, you're hired."**

This is the complete set: twelve standalone repositories, each one a
production pattern built from scratch — with tests that pass, demos
that run, and design decisions documented. No tutorial-ware, no
copy-paste chains. Every repo ships offline-deterministic tests (no
network needed) plus an optional live-LLM mode wired to any
OpenAI-compatible API.

## The projects

| # | Repo | Pattern | Proves |
|---|------|---------|--------|
| 1 | [p01-structured-output-agent](https://github.com/Murasimu/p01-structured-output-agent) | Pydantic-enforced LLM/tool responses, targeted self-correction retries, JSONL validation audit | You can make LLMs reliable, not random |
| 2 | [p02-rag-citation-agent](https://github.com/Murasimu/p02-rag-citation-agent) | RAG with post-hoc citation enforcement, confidence gating, search fallback | You can prevent hallucinations at scale |
| 3 | [p03-react-planning-agent](https://github.com/Murasimu/p03-react-planning-agent) | ReAct loop with iteration limits, bounded self-critique, graceful degradation | You can build agents that don't infinite loop |
| 4 | [p04-multi-tool-orchestrator](https://github.com/Murasimu/p04-multi-tool-orchestrator) | Dynamic tool registry, RBAC permission scoping, parallel DAG execution, write-conflict resolution | You can coordinate complex workflows |
| 5 | [p05-memory-agent](https://github.com/Murasimu/p05-memory-agent) | Compressed short-term buffer, long-term vector recall, cross-session sync | You can build agents that remember users |
| 6 | [p06-hitl-approval-agent](https://github.com/Murasimu/p06-hitl-approval-agent) | Uncertainty detection with rule hard-floors, approval gates, tamper-evident audit chain | You can build safe, compliant systems |
| 7 | [p07-cost-router](https://github.com/Murasimu/p07-cost-router) | Complexity-based model routing, budget cascades, early exit, cost-per-decision ledger | You can cut infra costs 40–60% |
| 8 | [p08-event-automation](https://github.com/Murasimu/p08-event-automation) | Idempotent webhook/queue workflows, backoff retries, terminal dead-lettering with replay | You can build production automation, not demos |
| 9 | [p09-debate-system](https://github.com/Murasimu/p09-debate-system) | Stance-diverse proposers, critic scoring, weighted consensus, confidence-scored synthesis | You can orchestrate swarms, not single agents |
| 10 | [p10-self-eval-agent](https://github.com/Murasimu/p10-self-eval-agent) | LLM-as-judge auto-eval, constraint-driven regeneration, improvement metrics | You can build systems that improve over time |
| 11 | [p11-production-observability](https://github.com/Murasimu/p11-production-observability) | Span tracing, latency/cost dashboards, loop/failure alerting, canary auto-rollback | You can ship to production, not just localhost |
| 12 | [p12-langgraph-circuit-breaker](https://github.com/Murasimu/p12-langgraph-circuit-breaker) | Circuit-breaker pattern for graph nodes: fail-fast, half-open probing + benchmark + PR writeup | You're a community builder, not just a consumer |

## Numbers

- **12 repos**, each independently installable (`uv pip install -e .`)
- **233 tests passing** across the suite (21 + 16 + 13 + 25 + 20 + 23 +
  21 + 22 + 18 + 16 + 25 + 13), all runnable offline with `pytest -q`
- **Live-LLM modes verified** against real OpenAI-compatible endpoints
  (P1–P11)
- **Benchmarks**: P7 measured ~95% savings vs always-flagship on a mixed
  workload; P12 measured ~27,000x fail-fast vs hung-dependency calls

## How the projects connect

The set is sequenced deliberately:

- **P1–P4 (reliability core)**: structured output and RAG grounding
  make model *output* trustworthy; ReAct and the orchestrator make
  *execution* trustworthy.
- **P5–P8 (production semantics)**: memory, HITL, cost routing, and
  event automation are the four systems an agent needs before real
  users touch it.
- **P9–P12 (scale & craft)**: debate improves answer quality through
  disagreement; self-eval closes the quality loop; observability
  closes the operations loop; the circuit breaker is the P11 findings
  turned into a publishable OSS pattern.

Several bugs *found by this suite's own tests* are documented in the
READMEs (P4's global-lock parallelism killer, P6's optimistic-judge
calibration hole, P8's poison-message retrigger storm) — the design
decisions sections explain both the bug and the fix.

## Stack

- **P1–P10**: Python stdlib + Pydantic where schemas matter — cores are
  framework-free, LLMs are plain `messages -> text` callables
- **P11**: LangGraph runtime + LangSmith-optional tracing (the
  observability layer itself is framework-free)
- **P12**: zero-dependency extension targeting LangGraph

All live modes work with OpenAI, Groq, DeepSeek, or any
OpenAI-compatible gateway via `LLM_API_KEY` / `LLM_BASE_URL` /
`LLM_MODEL` env vars (`.env.example` in each repo).

## License

MIT across all repos.
