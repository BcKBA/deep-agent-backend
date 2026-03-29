# Security Guidelines

## API Key Management

### Rules
1. **Never commit `.env`** — it is in `.gitignore`. Verify before every push: `git status` must not show `.env`.
2. **Never hardcode API keys** in Python files. Always use `os.getenv()` or `python-dotenv`.
3. **Never share keys in chat** (not with Claude, Copilot, or Antigravity).

### Current Keys Required

| Key | Where to Get | Where to Set |
|-----|-------------|--------------|
| `GOOGLE_API_KEY` | https://aistudio.google.com/app/apikey | `.env` |
| `OPENAI_API_KEY` (optional, OpenRouter) | https://openrouter.ai/keys | `.env` |
| `LANGSMITH_API_KEY` (optional, tracing) | https://smith.langchain.com | `.env` |

### `.env` Template

```env
GOOGLE_API_KEY=your_key_here

# Optional
# OPENAI_API_KEY=your_openrouter_key
# OPENAI_BASE_URL=https://openrouter.ai/api/v1
# LANGSMITH_API_KEY=your_langsmith_key
# LANGSMITH_TRACING=true
```

## If a Key is Accidentally Committed

1. Immediately revoke the key in the provider dashboard
2. Generate a new key
3. Run: `git filter-branch` or use BFG Repo Cleaner to purge the key from history
4. Force push (coordinate with collaborators)

## Shell Tool Safety

The Deep Agent has a `Shell` tool that can run arbitrary commands. In production:
- Restrict the shell to a sandboxed environment
- Never run as admin/root
- For development (`langgraph dev`), the shell runs with your user permissions — be careful what you ask the agent to do
