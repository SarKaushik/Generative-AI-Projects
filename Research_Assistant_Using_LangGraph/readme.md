
# 🧠 Research Agent using LangGraph

This project demonstrates how to build a **tool-augmented conversational agent** using [LangGraph](https://github.com/langchain-ai/langgraph), [LangChain](https://www.langchain.com/), and the **Tavily search tool**. The agent can reason over user queries and call external tools like search engines to enhance its responses.

---

## 🔧 Features

- ✅ Multi-turn reasoning with external tools
- 🔍 Real-time internet search using **Tavily**
- 🧩 Custom agent graph using **LangGraph**
- ⚡ OpenAI GPT integration (`gpt-4`, `gpt-3.5`, etc.)
- 🧪 Ideal for research-style Q&A

---

## 📦 Requirements

- Python 3.8+
- `langgraph`
- `langchain`
- `langchain-openai`
- `langchain-community`
- `openai`
- `tavily-python`
- `IPython` (for notebook usage)

Install them with:

```bash
pip install langgraph langchain langchain-openai langchain-community openai tavily-python ipython
