# MCP_AND_TOOLS.md — Proactive AI Environment & MCP Setup (`ai-and-agents`)

> **AI Agent Instruction**: On Day-0 Bootstrap, check which AI documentation MCP servers, local inference engines (Ollama), and Python/TS toolchains (`uv`, `bun`) are available. **If anything needed for the project is missing, proactively ask the user if you can install or configure it for them!** Record all verified tools in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md).

---

## 1. Recommended MCP Servers & Skills to Check

| MCP Server / Skill | Purpose in `ai-and-agents` | How to Check & Offer Setup |
| :--- | :--- | :--- |
| **Gemini API Docs MCP & Skills** (`gemini-api-docs` MCP, `gemini-api-dev`, `gemini-live-api-dev`, `google-antigravity-sdk`) | Provides up-to-date official documentation for Gemini text, multimodal, Live WebSocket audio/video, and structured outputs. | Check if `gemini_get_doc` or the `gemini-api-dev` skill is available and load it before writing Gemini code. |
| **MCP Inspector** (`npx @modelcontextprotocol/inspector`) | Interactive debugger and CLI verifier for testing custom MCP servers (`tools/list`, `tools/call`, `resources/list`). | When building an MCP server, check if `npx` / `bunx` is available to run `@modelcontextprotocol/inspector`. |
| **`credentials` Skill Protocol** | Safe verification and prompting for missing API keys (`GEMINI_API_KEY`, `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`) without exposing secrets in chat. | Always check `.env` key names safely (`Get-Content .env` keys only, never print secret values) and create `.env.example`. |

---

## 2. AI Development Environment Doctor Checklist

Run these non-destructive checks and log the results in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md):

```powershell
# 1. Check Python & uv (for Python AI agents / FastMCP)
uv --version 2>$null
python --version 2>$null

# 2. Check Bun / Node (for TypeScript AI agents / MCP Inspector)
bun --version 2>$null
node --version 2>$null

# 3. Check Local AI Runtime (if building local/offline AI)
ollama --version 2>$null
```

### Auto-Setup Commands (Offer to Run with User Permission if Missing)
- **Install `uv`**: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
- **Install Bun**: `winget install Oven-sh.Bun`
- **Install Ollama (for local LLMs/embeddings)**: `winget install Ollama.Ollama`

---

## 3. Save Verified Setup Info for Future Creations
Update [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) (`Environment Check Status: VERIFIED`) and log any working model configurations, local inference endpoints, or MCP server patterns in Section 5 of [`.ai/MEMORY.md`](./MEMORY.md).
