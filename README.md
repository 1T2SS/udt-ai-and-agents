# Universal AI, LLM Apps & MCP Server Template (`udt-ai-and-agents`)

> **AI-First Vibe Coding Preset** for building multi-agent systems, custom **MCP (Model Context Protocol)** servers, multimodal **Gemini / Claude / OpenAI** applications, RAG pipelines, and local AI tools (**Ollama / vLLM / llama.cpp**).

---

## Quick Start (30 Seconds)

### Option A: From GitHub
1. Click **"Use this template" → "Create a new repository"** on GitHub.
2. Clone your new repo and open it in any AI coding agent.
3. Describe the AI agent, MCP server, or LLM workflow you want to build!

### Option B: From Local UDT Hub
```powershell
.\scripts\new-project.ps1 -Preset ai-and-agents -Target "E:\Projects\MyAiAgent" -InitGit
```

---

## Why This Preset Is Essential for AI Projects
AI coding agents frequently hallucinate deprecated LLM SDK packages (like `google-generativeai` instead of `google-genai` or legacy OpenAI v0 syntax) and outdated model IDs. This preset enforces:
1. **Live SDK & Model ID Verification**: Uses official documentation MCP servers (`gemini-api-docs`, `developer-knowledge`) and [`.ai/RESEARCH_PLAYBOOK.md`](./.ai/RESEARCH_PLAYBOOK.md) before writing SDK calls.
2. **Proactive Environment & MCP Doctor**: Checks for `uv`, `bun`, MCP Inspector (`@modelcontextprotocol/inspector`), local Ollama/vLLM endpoints, and safe API key setup via [`.ai/MCP_AND_TOOLS.md`](./.ai/MCP_AND_TOOLS.md).
