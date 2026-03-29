# Architecture Decisions

## ADR-001: Use `uv` instead of `pip`

**Decision:** Use `uv` as the package manager.
**Reason:** Project requirement. `uv` is significantly faster than `pip`, handles virtual environments automatically, and produces a lockfile (`uv.lock`) for reproducibility.
**How to apply:** Always use `uv add <package>` instead of `pip install`. Never run `pip` directly.

---

## ADR-002: Google Gemini (AI Studio) as LLM provider

**Decision:** Use `google_genai:gemini-2.5-flash` via Google AI Studio (Paid tier 1 account).
**Reason:** Free tier (20 RPD) was insufficient for development. Paid tier 1 provides 10K RPD for gemini-2.5-flash and unlimited RPD for gemini-2.0-flash-lite. Easy to set up with just `GOOGLE_API_KEY`. Switching to OpenRouter or other providers requires only changing one line in `agent.py`.
**How to apply:** Get API key from https://aistudio.google.com/app/apikey and put in `.env`.
**Fallback if rate-limited:** Switch to `gemini-2.0-flash-lite` (unlimited RPD on paid tier).
**Alternative:** OpenRouter — set `OPENAI_API_KEY` + `OPENAI_BASE_URL=https://openrouter.ai/api/v1` and change model string.

---

## ADR-003: Deep Agent before ReAct Agent

**Decision:** Implement Deep Agent first (Week 2), ReAct Agent later.
**Reason:** Project assignment order. Deep Agent is more complex (hierarchical, sub-agents) so scaffolding it first establishes the infrastructure for both.

---

## ADR-004: LangGraph Studio as frontend for now

**Decision:** Use the hosted LangGraph Studio UI (`smith.langchain.com/studio`) instead of building a custom frontend.
**Reason:** Week 2 task says to use the LangChain-provided UI to move fast and prototype. Custom UI is a future-week task.

---

## ADR-005: Keep `.env` out of git

**Decision:** Never commit `.env` to the repository.
**Reason:** API keys would be exposed publicly. `.gitignore` excludes `.env`. Share keys only via secure channels.

---

## ADR-006: Single backend repo, separate frontend repo

**Decision:** `bitirme-backend` for Python agent code, `bitirme-frontend` for UI code.
**Reason:** Project requirement — instructor expects two separate repositories. Also good separation of concerns.

---

## ADR-007: Custom clone_and_read_repo tool instead of shell git

**Decision:** Add a custom `clone_and_read_repo` tool using `gitpython` library instead of relying on the agent's built-in shell tool to run `git clone`.
**Reason:** The Deep Agent's shell tool runs in a sandboxed environment with no access to the host system's `git` binary (`git --version` returned "No data"). Custom tool uses `gitpython` in-process, returns file tree + file contents directly to the agent — no VFS access needed.
**How to apply:** Tool is defined in `agent.py`. Pass any public GitHub URL and the agent will clone and analyze it.
