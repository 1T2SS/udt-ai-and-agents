# Recipe: Local AI & Embedded RAG Pipeline (Ollama + LanceDB + FastAPI)

## When to Use
Use this recipe when building a privacy-first local AI assistant, document search/RAG engine, or hybrid local+cloud inference pipeline.

## 1. Official Scaffold Commands
```powershell
uv init --package .
uv add lancedb ollama pydantic fastapi[standard] httpx rich
uv add --dev pytest ruff
```

## 2. Verification Commands
- **Check Local Ollama Models**: `ollama list`
- **Run Tests**: `uv run pytest`
