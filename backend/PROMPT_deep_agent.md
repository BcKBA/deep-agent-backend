# Prompt Templates — Deep Agent Development

Use these templates when asking Antigravity or Copilot Chat to help with the Deep Agent backend.

---

## Base Context Block (always prepend)

```
Project: AI Agent chatbot that answers questions about software repositories.
Stack: Python 3.13, uv package manager, deepagents==0.4.12, langgraph, langchain-google-genai.
LLM: Google Gemini 2.5 Flash via langchain-google-genai (Paid tier 1). Fallback: gemini-2.0-flash-lite.
Deployment: langgraph dev → LangGraph Studio UI.
Rules:
  - Use uv (not pip)
  - Check LangChain Docs MCP and DeepWiki MCP for current API syntax
  - Do not hardcode API keys — use .env + python-dotenv
  - Keep code minimal, no unnecessary abstractions
```

---

## Add a Custom Tool to the Agent

```
[Base Context Block]
Current agent.py: [paste file content]

Task: Add a custom tool to the Deep Agent that [describe what the tool does].
The tool should be a plain Python function with a docstring (LangChain uses the docstring as the tool description).
Add it to the tools=[] list in create_deep_agent().
Check the deepagents documentation via DeepWiki MCP for the correct tool signature format.
```

---

## Debug an Error

```
[Base Context Block]
I got this error when running `uv run langgraph dev`:
[paste full error traceback]

The relevant file is agent.py:
[paste agent.py content]

Task: Identify the root cause and fix it. Check LangChain Docs MCP if it's a library API issue.
```

---

## Add a New LLM Provider

```
[Base Context Block]
Current model in agent.py: init_chat_model("google_genai:gemini-2.0-flash")

Task: Add support for [OpenRouter / Anthropic / Groq] as an alternative LLM provider.
Use an environment variable to switch between providers (e.g., LLM_PROVIDER=google or openrouter).
Do not break the existing Google Gemini setup.
Check LangChain Docs MCP for init_chat_model() provider syntax.
```

---

## Test the Agent

```
[Base Context Block]

Task: Write a simple test script (test_agent.py) that:
1. Loads the agent from agent.py
2. Sends the message: "List the files in the current directory"
3. Prints the agent's response
4. Does NOT require langgraph dev to be running (run it directly with: uv run python test_agent.py)
Check deepagents documentation via DeepWiki MCP for how to invoke the agent directly.
```
