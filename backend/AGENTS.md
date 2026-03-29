# AI Agent Usage Guide

This file defines which AI coding tool to use for which tasks in this project.
All tools use MCP servers: `langchain-docs` and `deepwiki` — always let them query these.

---

## Claude Code (this tool — VS Code extension)

**Best for:**
- File creation, editing, reading
- Running terminal commands (`uv add`, `git`, `langgraph dev`)
- Planning and architecture decisions
- Debugging Python errors
- Setting up project structure

**When to use:** Primary tool for backend Python work and project setup.

**Important:** Claude Code does NOT have access to internet by default — use `WebSearch` tool when needed.

---

## Antigravity (Gemini Pro)

**Best for:**
- Long multi-file refactors
- Generating boilerplate code from descriptions
- Explaining complex LangChain/LangGraph concepts (via deepwiki MCP)
- When you need Gemini-specific knowledge

**Prompt tips:**
- Always tell it: "Use the DeepWiki MCP and LangChain Docs MCP to check the latest documentation"
- Specify: "Use `uv` not `pip`"
- Specify: "Python only, no TypeScript"

---

## GitHub Copilot (VS Code inline)

**Best for:**
- Inline code completion while typing
- Quick docstrings and type hints
- Small, localized edits within a file

**Status:** Pending account approval (as of 2026-03-27)

**Prompt tips (Copilot Chat):**
- Use `#file:agent.py` to give it context
- Say: "Use the LangChain Docs MCP for up-to-date syntax"

---

## Token Optimization Strategy

| Situation | Action |
|-----------|--------|
| Simple edit (1-5 lines) | Use Copilot inline |
| Medium task (1 file) | Use Claude Code |
| Large refactor (multiple files) | Use Antigravity |
| Need latest docs | Always invoke MCP in prompt |
| Expensive model getting rate-limited | Switch to `gemini-2.0-flash-lite` in `.env` |

---

## Standard Prompt Prefix (for Antigravity / Copilot Chat)

Always prepend this when working on this project:

```
Context: Python backend for a LangChain Deep Agent that answers questions about code repositories.
Stack: Python 3.13, uv package manager, deepagents library, langgraph, langchain-google-genai.
Rules: Use uv (not pip). Check LangChain Docs MCP and DeepWiki MCP for latest syntax.
File: [paste relevant file or describe what you need]
Task: [your actual request]
```
