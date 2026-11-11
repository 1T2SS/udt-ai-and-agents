# Recipe: Multimodal LLM & Autonomous Agent App (`google-genai` / PydanticAI / TS)

## When to Use
Use this recipe when building an AI agent, multimodal app, or structured-output pipeline in Python (`uv` + `google-genai` / `pydantic-ai`) or TypeScript (`Bun` + `@google/genai`).

## 1. Official Scaffold Commands

### Option A: Python (`uv` + `google-genai` + Pydantic v2)
```powershell
uv init --package .
uv add google-genai pydantic pydantic-settings python-dotenv rich
uv add --dev pytest ruff mypy
```

### Option B: TypeScript (`Bun` + `@google/genai` + Zod)
```powershell
bun init -y
bun add @google/genai zod
bun add -D @types/bun vitest
```

## 2. Recommended Directory Layout
```text
├── .env.example          # GEMINI_API_KEY=your_key_here
├── src/
│   ├── config.py         # Validated settings & model IDs
│   ├── prompts/          # Versioned system instructions
│   ├── schemas/          # Pydantic / Zod structured output contracts
│   ├── tools/            # Deterministic functions exposed to the agent
│   └── agent.py          # Core agent loop & error/retry handling
└── tests/
    └── test_evals.py     # Smoke & evaluation test suite
```

## 3. Verification Commands
- **Lint & Typecheck**: `uv run ruff check . && uv run mypy src` (or `bun x tsc --noEmit`)
- **Run Unit & Eval Tests**: `uv run pytest` (or `bun test`)
