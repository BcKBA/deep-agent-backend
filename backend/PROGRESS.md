# Progress Log

## Week 2 — Scaffolding (2026-03-27)

### Completed
- [x] `uv` package manager installed (v0.11.2)
- [x] Project initialized with `uv init` at `c:\bitirme`
- [x] Dependencies installed: `deepagents`, `langgraph-cli[inmem]`, `langchain-google-genai`, `python-dotenv`, `gitpython`
- [x] `agent.py` created — Deep Agent with all default tools (planning, vfs, shell, sub-agents) + custom `clone_and_read_repo` tool
- [x] `langgraph.json` created — graph config for `langgraph dev`
- [x] `.env` configured with GOOGLE_API_KEY (Paid tier 1 account)
- [x] `.gitignore` created
- [x] MD documentation files created
- [x] `gh` CLI v2.68.1 installed → `C:\Users\Alperen Kayım\.local\bin\gh.exe`
- [x] `uv` + `gh` added to Windows user PATH permanently
- [x] `gh auth login` completed (GitHub account: alperenkayim)
- [x] MD documentation system created (CONTEXT, PROGRESS, DECISIONS, AGENTS, SECURITY, PROMPT_deep_agent)
- [x] GitHub repo `bitirme-backend` created → https://github.com/alperenkayim/bitirme-backend
- [x] GitHub repo `bitirme-frontend` created → https://github.com/alperenkayim/bitirme-frontend
- [x] `langgraph dev` tested — server running on port 2024, LangGraph Studio connected
- [x] Agent tested — successfully cloned and analyzed GitHub repositories via `clone_and_read_repo` tool
- [x] Instructor `amirkiarafiei` collaborator invite sent to both repos

### In Progress
- [ ] Instructor collaborator invite acceptance (pending on their end)
- [ ] GitHub Copilot account approval (pending)

---

## Week 1 — Setup (completed before Week 2)

### Completed
- [x] Git & GitHub account ready
- [x] VS Code installed with Copilot extension
- [x] Gemini Code Assist (Antigravity) set up
- [x] MCP servers configured in VS Code: `langchain-docs`, `deepwiki`
- [x] LaTeX environment configured (for research paper)

---

## Upcoming Weeks

| Week | Goal |
|------|------|
| Week 3 | ReAct Agent implementation |
| Week 4+ | Custom frontend UI |
| Later | SWE-QA dataset evaluation |
| Final | Research paper |
