# CONTEXT.md — Project Master Reference

> **Yeni chat veya model başlatırken tek komut:**
> `"Read CONTEXT.md at c:\bitirme and follow all rules and links inside it before doing anything."`
>
> Bu dosyayı okuyan her model şunları bilir: proje bağlamı, kurallar, mevcut ilerleme, araç seçimleri.
> Detay için: PROGRESS.md (neredeyiz) · DECISIONS.md (neden) · AGENTS.md (hangi AI aracı ne zaman) · SECURITY.md (key yönetimi)

---

## Mandatory Rules (her model her zaman uymak zorunda)

1. **Package manager: `uv`** — `pip` ASLA kullanma. Paket eklemek için: `uv add <pkg>`. Çalıştırmak için: `uv run <cmd>`.
2. **API keys: `.env` dosyasında** — kod içine hardcode etme. `python-dotenv` ile yükle.
3. **Her değişiklikten sonra push** — `gh` CLI ile commit + push yap (bkz. Git Workflow bölümü).
4. **Her değişiklikten sonra PROGRESS.md güncelle** — tamamlanan adımı işaretle, yeni adım varsa ekle.
5. **MCP kullan** — LangChain veya deepagents kodu yazarken mutlaka `langchain-docs` ve `deepwiki` MCP'yi sorgula. Eski dokümantasyonla yanlış kod yazma.
6. **Minimal değişiklik** — istenenden fazlasını yapma, gereksiz abstraction ekleme, docstring/yorum ekleme.

---

## What This Project Is

An AI Agent chatbot that answers complex questions about software repository architecture and logic.
Two agent architectures are implemented and compared:

- **Deep Agent** (LangChain Deep Agents library) — hierarchical, uses sub-agents, planning, virtual filesystem
- **ReAct Agent** — "Reason-then-Act" loop, simpler, single-context

Final deliverable: a research paper comparing both architectures on the **SWE-QA dataset**.

## Scope

| Component | Description | Status |
|-----------|-------------|--------|
| Deep Agent backend | Python, LangChain deepagents, langgraph dev | Week 2 — Complete |
| ReAct Agent backend | Python, LangChain | Week 3 — Not started |
| Frontend UI | LangGraph Studio (built-in) → custom UI later | Week 2 — Complete |
| SWE-QA Evaluation | Benchmark both agents on dataset | Later |
| Research Paper | Academic comparison of both architectures | Final |

## Architecture

```
User → LangGraph Studio UI (https://smith.langchain.com/studio)
             ↓
       langgraph dev server (localhost:2024)
             ↓
       Deep Agent (deepagents.create_deep_agent)
             ↓
       LLM (Google Gemini via AI Studio)
             ↓
       Default Tools:
         - Planning Tool (write_todos)
         - Virtual Filesystem (read/write/edit/ls/glob/grep)
         - Shell (execute)
         - Sub-agents (task)
         - Context Summarization
       Custom Tools:
         - clone_and_read_repo(repo_url) — clones GitHub repo, returns file tree + key file contents
         - read_repo_file(file_path) — reads a specific file from a cloned repo
```

## Repository Structure

```
c:\bitirme\           ← backend repo (this repo)
  agent.py            ← Deep Agent definition
  langgraph.json      ← graph config for langgraph dev
  pyproject.toml      ← uv-managed dependencies
  uv.lock
  .env                ← API keys (NOT committed)
  CONTEXT.md          ← this file
  PROGRESS.md         ← weekly progress log
  DECISIONS.md        ← architecture decisions
  AGENTS.md           ← AI tool usage guide
  SECURITY.md         ← API key & secret management
```

## Tech Stack

| Layer | Choice | Reason |
|-------|--------|--------|
| Language | Python 3.13 | LangChain ecosystem |
| Package manager | uv | Fast, modern, project requirement |
| Agent framework | LangChain deepagents 0.4.12 | Project requirement |
| LLM provider | Google Gemini (AI Studio) | Free daily limits, no credit card |
| Deployment | langgraph dev | Built-in, connects to LangGraph Studio |
| Frontend (now) | LangGraph Studio hosted UI | Fast prototype |
| Frontend (later) | Custom UI | Future week |

## Git Workflow (her değişiklikten sonra)

```powershell
cd C:\bitirme
git add <değişen dosyalar>
git commit -m "kısa açıklama"
git push
```

**Tek seferlik not:** `gh auth login` tamamlandı. `uv` ve `gh` PATH'e kalıcı eklendi. Yeni terminal açınca direkt çalışır.

**gh CLI kurulu:** `C:\Users\Alperen Kayım\.local\bin\gh.exe` (v2.68.1)
**gh auth:** Tamamlandı — PATH kalıcı olarak eklendi (2026-03-27). Yeni terminalde direkt `gh` ve `uv` çalışır, tekrar login veya PATH ayarı gerekmez.

---

## Key Links

- LangGraph Studio: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
- Google AI Studio (API key): https://aistudio.google.com/app/apikey
- Instructor GitHub: https://github.com/amirkiarafiei
