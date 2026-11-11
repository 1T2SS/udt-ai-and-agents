# RESEARCH_PLAYBOOK.md — AI, LLM & MCP Server Pre-Coding Research Protocol

> **Preset**: `ai-and-agents`
> **Rule**: Always verify current model names, SDK methods, and MCP schemas before writing code.

---

## 1. Live SDK & Model ID Verification
1. **Check Official Docs MCP / Skills First**:
   - If building with Gemini, Gemini Live API, or Google Antigravity SDK, load the matching skill (`gemini-api-dev`, `gemini-live-api-dev`, `google-antigravity-sdk`) and query the `gemini-api-docs` MCP server!
   - Never guess model strings from outdated memory. Verify the active model IDs (e.g., `gemini-2.5-flash`, `gemini-2.5-pro`, etc.) in the official docs.
2. **Structured Outputs & Tool Calling Contracts**:
   - Define every tool's input and output schema using **Pydantic v2** (Python) or **Zod** (TypeScript) with clear `Field(description=...)` docstrings — the LLM reads those descriptions to decide when and how to call the tool!

## 2. Prompt & Evaluation Engineering Rules
- Keep system prompts in dedicated, versioned files or constants (`src/prompts/`) rather than buried inside route handlers.
- Create a lightweight evaluation script (`evals/` or `tests/test_evals.py`) with 3–5 representative test inputs to verify agent accuracy, tool selection, and structured output conformance.
