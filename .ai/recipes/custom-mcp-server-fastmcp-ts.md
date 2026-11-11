# Recipe: Custom MCP (Model Context Protocol) Server (`FastMCP` or TypeScript SDK)

## When to Use
Use this recipe when building a custom **MCP Server** that exposes tools, resources, and prompts to AI agents (Antigravity, Claude Desktop/Code, Cursor, Windsurf, Cline).

## 1. Official Scaffold Commands

### Option A: Python MCP Server with `mcp` (`FastMCP`) + `uv`
```powershell
uv init --package .
uv add "mcp[cli]" pydantic httpx
uv add --dev pytest ruff
```

### Option B: TypeScript MCP Server with `@modelcontextprotocol/sdk`
```powershell
bun init -y
bun add @modelcontextprotocol/sdk zod
bun add -D @types/bun typescript
```

## 2. Crucial MCP Server Rules
- **NEVER `print()` to `stdout` in stdio MCP servers!** Standard output (`stdout`) is reserved exclusively for JSON-RPC 2.0 messages. Always log debug messages to **`stderr`** (`sys.stderr` in Python / `console.error` in TypeScript).
- **Clear Tool Descriptions & Schemas**: Every `@mcp.tool()` must have a descriptive docstring and typed parameters so client agents understand when and how to invoke it.

## 3. Verification Commands
- **Syntax & Import Check (Python)**: `uv run python -c "import src.server"`
- **Test with MCP Inspector**: `npx @modelcontextprotocol/inspector uv --directory . run mcp-server`
