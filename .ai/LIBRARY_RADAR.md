# LIBRARY_RADAR.md — AI, Agents & MCP Server Tech Stack Guide

> **Preset**: `ai-and-agents`
> **Rule for AI Agents**: Always use current official SDKs and Structured Outputs (JSON Schema / Pydantic / Zod) from the **Approved Radar** below. Never use deprecated legacy SDKs listed in the **Banned** section.

---

## 1. Architecture Decision Tree

| AI Project Goal | Recommended Primary Stack | Matching Recipe |
| :--- | :--- | :--- |
| **Multimodal LLM App, Autonomous Agent, or Tool-Calling Workflow** | **Google GenAI SDK** (`google-genai` in Python / `@google/genai` in TS), **Anthropic SDK**, or **PydanticAI** | [`.ai/recipes/multimodal-llm-and-agents.md`](./recipes/multimodal-llm-and-agents.md) |
| **Custom MCP (Model Context Protocol) Server for AI IDEs & Agents** | **FastMCP** (`mcp[cli]` / `fastmcp` in Python via `uv`) or **`@modelcontextprotocol/sdk`** (TypeScript) | [`.ai/recipes/custom-mcp-server-fastmcp-ts.md`](./recipes/custom-mcp-server-fastmcp-ts.md) |
| **Local AI / Offline LLM / RAG & Vector Search Pipeline** | **Ollama / vLLM / llama.cpp** + **DuckDB / pgvector / LanceDB** + **FastAPI / uv** | [`.ai/recipes/local-ai-and-rag-pipeline.md`](./recipes/local-ai-and-rag-pipeline.md) |

---

## 2. Approved Library Radar

- **Official Provider SDKs**:
  - **Gemini**: **`google-genai`** (Python) and **`@google/genai`** (TypeScript/JS).
  - **Anthropic**: `anthropic` (Python) and `@anthropic-ai/sdk` (TS).
  - **OpenAI**: `openai` v1+ (Python) and `openai` v4+ (TS).
  - **Google Antigravity SDK**: For orchestrating Antigravity agents (`google-antigravity-sdk` skill).
- **Agent Frameworks & Structured Outputs**:
  - **Python**: **PydanticAI** (type-safe agent tool calling with Pydantic v2), **LangGraph** (stateful graph workflows), **Instructor**.
  - **TypeScript**: **Vercel AI SDK** (`ai`, `@ai-sdk/google`, `@ai-sdk/anthropic`, `@ai-sdk/openai`) + **Zod**.
- **MCP Server Development**:
  - **Python**: `mcp[cli]` / `fastmcp`.
  - **TypeScript**: `@modelcontextprotocol/sdk` + `zod`.
- **Vector / Embedded RAG Databases**:
  - **LanceDB** (serverless, embedded, blazing fast), **pgvector** (PostgreSQL), **ChromaDB**, or **Qdrant**.

---

## 3. Banned / Deprecated by Default (DO NOT USE)

| Banned Package / Pattern | Why It Is Banned | Use This Instead |
| :--- | :--- | :--- |
| **`google-generativeai` (Python) / `@google/generative-ai` (JS)** | Deprecated legacy Gemini SDK | Use **`google-genai`** (Python) or **`@google/genai`** (JS/TS) |
| **Fragile regex parsing of free-form LLM JSON responses** | Breaks whenever the LLM adds markdown fences or commentary | Use native **Structured Outputs (`response_schema` / Pydantic / Zod)** |
| **Hardcoding API keys (`GEMINI_API_KEY = "AIza..."`) in source code** | Severe security leak | Load from `.env` (gitignored) and document required keys in `.env.example` |
| **Heavy LangChain wrapper chains for simple single-prompt + tool calls** | Obscures prompts, bloats dependencies, hard to debug | Call the official SDK (`google-genai`, `anthropic`, `openai`) or **PydanticAI** directly |
