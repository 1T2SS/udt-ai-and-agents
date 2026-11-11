# QUALITY_CONTROL.md — Master Quality Control Sub-Agent Protocol (`ai-and-agents`)

> **Preset**: `ai-and-agents`
> **QC Persona**: **Principal AI Systems Director & LLM Evaluation Architect** (`master-qc-director`)
> **Mandatory Rule**: Use **ONE** Master Quality Control Sub-Agent at the end of each development round. Never spawn multiple separate review sub-agents.
> **Pass Threshold**: Overall Average **`>= 8.5 / 10.0`** AND **every individual category `>= 8.5 / 10.0`**.

---

## 1. How to Invoke the Single Master QC Check

When an AI agent, LLM pipeline, or MCP server round is complete:
- **Antigravity**: Define/invoke the single `master-qc-director` sub-agent (`EnableWriteTools: true`, `EnableMCPTools: true`) to audit prompts, SDK usage, structured output schemas, MCP compliance, and evaluation tests, writing `.ai/QC_REPORT.md`.
- **Claude Code**: Invoke `.claude/agents/master-qc-director.md`.
- **Cursor / Windsurf / Copilot / Cline**: Execute a dedicated **Master QC Director Audit Pass** using the rubric below and write `.ai/QC_REPORT.md`.

---

## 2. The 5-Pillar Zero-Trust Deduction Rubric (Starts at `10.0` Per Category)

### Category 1: Prompt Engineering, Persona & Output Quality (`>= 8.5 / 10`)
- **`-2.0 pts`**: Vague, unstructured inline prompts buried inside route/handler code instead of clean, modular prompt templates with explicit role, constraints, and examples.
- **`-1.5 pts`**: Hallucination-prone instructions lacking grounding or citation/verification rules.

### Category 2: Agent Mechanics, Tool Calling & Structured Schemas (`>= 8.5 / 10`)
- **`-2.5 pts`**: Parsing LLM outputs with fragile regex/string splitting when native Structured Outputs (`response_schema` / Pydantic v2 / Zod) should be used.
- **`-2.0 pts`**: MCP tools or agent functions missing clear docstrings and parameter `Field(description=...)` metadata.
- **`-1.5 pts`**: Unbounded agent retry loops without a maximum turn/step budget.

### Category 3: SDK Currency, Code Architecture & Secret Hygiene (`>= 8.5 / 10`)
- **`-4.0 pts` (Automatic Fail)**: Using deprecated legacy SDKs (`google-generativeai` instead of `google-genai`, `@google/generative-ai` instead of `@google/genai`) or hardcoding API keys in source files!
- **`-3.0 pts` (For stdio MCP Servers)**: Writing debug logs to `stdout` (`print()` / `console.log()`) instead of `stderr`, which corrupts JSON-RPC stdio transport!

### Category 4: Feature Completeness & End-to-End Reliability (`>= 8.5 / 10`)
- **`-2.0 pts`**: Missing graceful handling for rate limits (`429`), context window limits, or malformed tool arguments.
- **`-1.5 pts`**: Incomplete RAG/memory persistence or missing `.env.example`.

### Category 5: Latency, Token Efficiency & Evaluation Suite (`>= 8.5 / 10`)
- **`-3.0 pts` (Automatic)**: Linter, typechecker, or evaluation/unit test suite fails.
- **`-2.0 pts`**: No automated smoke/evaluation test cases (`tests/` or `evals/`) verifying that the agent/MCP tools execute as expected.

---

## 3. Auto-Refinement Protocol (Up to 3 Rounds)
If any category scores `< 8.5 / 10`, `master-qc-director` sets `qc_status: REFINEMENT_REQUIRED` in [`.ai/QC_REPORT.md`](./QC_REPORT.md). The main agent must fix all listed deductions and re-run `master-qc-director` (up to 3 rounds max) before completing the round.
