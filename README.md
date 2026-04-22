<div align="center">
  <img src="static/img/hero.png" alt="Deep Agent Drive-Thru" width="80%">
  <h1>Workshop: How To Build A Deep Agent Harness</h1>
  <p><strong>Presented by ArtiPortal.com</strong></p>
  <h3>Build, Customize, and Deploy "Batteries-Included" Agents.</h3>

  <br/>

  ![Python](https://img.shields.io/badge/python-3.11%2B-blue?logo=python&logoColor=white)
  ![License](https://img.shields.io/badge/license-MIT-green)
  ![LangGraph](https://img.shields.io/badge/LangGraph-powered-orange)
  ![deepagents](https://img.shields.io/badge/deepagents-%E2%89%A50.0.34-purple)
  ![uv](https://img.shields.io/badge/uv-package%20manager-red)
  ![Workshop](https://img.shields.io/badge/workshop-ArtiPortal.com-blue)

</div>

---

## 🗺️ Workshop Roadmap

| # | Module | Topic | What You'll Build |
| :---: | :--- | :--- | :--- |
| 0 | 🛠️ [Prerequisites & Setup](#️-module-0-prerequisites--setup) | Environment & Keys | Working dev environment |
| 1 | 🚀 [Your First Agent](#-module-1-your-first-agent) | The "Health Check" Harness | `simple_agent.py` |
| 2 | 🔧 [Brain & Hands](#-module-2-customizing-brain--hands) | Model Swaps & Custom Tools | `custom_agent.py` |
| 3 | 🤝 [Delegated Authority](#-module-3-sub-agents--task-planning) | The Sub-Agent Pattern | Multi-step research agent |
| 4 | 🧪 [Benchmarking](#-module-4-the-deep-agents-cli) | The Deep Agents CLI | TUI coding assistant |
| ★ | 🏗️ [Advanced Patterns](#-exploration-advanced-patterns) | Production Architectures | See examples directory |

---

Welcome to the **Deep Agents Workshop**! This hands-on guide will transform you from an agent enthusiast into a developer capable of deploying production-ready AI agents using the Deep Agents framework and LangGraph.

At its core, Deep Agents is an **Agent Harness**. While most LLM implementations focus on the model, a harness focuses on the **plumbing**: the state management, tool-calling loops, planning logic, and context compression required for a reliable system. By building on [LangGraph](https://github.com/langchain-ai/langgraph), Deep Agents provides a robust, stateful architecture that handles complex cycles and human-in-the-loop interactions with ease.

This workshop, curated by **ArtiPortal.com**, is designed to bridge the gap between "cool demos" and "functional software."

## 📖 How to Use This Workshop

| Icon | Purpose | What to Do |
| :---: | :--- | :--- |
| 🚀 | **Module** | Core technical narrative and follow-along code. |
| 🧪 | **Lab Challenge** | Active learning — a task for you to solve using new skills. |
| 🔍 | **Deep Dive** | Under-the-hood explanation of the "Why" behind the code. |
| 🛑 | **Common Gotcha** | Preventive troubleshooting for common friction points. |
| ✅ | **Self-Check** | Quick reflection questions to verify your understanding. |

---

## 🎯 Learning Objectives

By the end of this workshop, you will be able to:

| # | Skill |
| :---: | :--- |
| 1 | **Architect** a production-ready agent harness using the `create_deep_agent` factory |
| 2 | **Configure** multi-provider LLM orchestration (e.g., Anthropic for reasoning, OpenAI for tools) |
| 3 | **Implement** autonomous planning and sub-agent delegation for multi-faceted tasks |
| 4 | **Execute** a terminal-based TUI coding assistant using the Deep Agents CLI |
| 5 | **Optimize** token efficiency through automated context management and summarization |

---

## 🏗️ The Workshop Tech Stack

| Technology | Category | Purpose | Setup |
| :--- | :---: | :--- | :--- |
| **Python 3.11+** | 💻 Local | Core runtime | [Download](https://www.python.org/downloads/) |
| **[uv](https://astral.sh/uv/)** | 💻 Local | Dependency manager | `curl -LsSf https://astral.sh/uv/install.sh \| sh` |
| **Deep Agents SDK** | 📦 Package | The agent harness | `uv add deepagents` |
| **Anthropic / OpenAI** | ☁️ SaaS | Reasoning & tools | API keys + credits |
| **[LangSmith](https://smith.langchain.com/)** | ☁️ SaaS | Observability & tracing | Account + API key |
| **[Tavily](https://tavily.com/)** | ☁️ SaaS | Web search | API key (free tier available) |
| **[Modal](https://modal.com/)** | ☁️ SaaS | Remote GPU sandbox | Account + `uv run modal setup` |

### 🔍 Deep Dive: The Hybrid Architecture

This workshop uses a **Hybrid Infrastructure** model. The "Brain" (LLM) and "Eyes" (Search) live in the cloud to minimize local hardware requirements, while the "Hands" (state management, file I/O) run locally for maximum security and control.

---

## 🛠️ Module 0: Prerequisites & Setup

Before we start, ensure your environment is ready.

> [!IMPORTANT]
> This workshop requires Python 3.11+ and a valid API key for an LLM provider (OpenAI is the default).

### 1. Installation

```bash
# Recommended: Using uv
uv add deepagents

# Traditional: Using pip
pip install deepagents
```

### 2. Environment Configuration

```bash
export OPENAI_API_KEY="your-key-here"
# Optional: For Anthropic models
export ANTHROPIC_API_KEY="your-key-here"
```

---

## 🚀 Module 1: Your First Agent

In this module, we'll run a "Health Check" agent. Deep Agents provides a `create_deep_agent()` factory that sets up planning, filesystem tools, and context management out of the box.

### The Code

Create a file named `simple_agent.py`:

```python
from deepagents import create_deep_agent

# Initialize the agent with smart defaults
# This includes planning, file access, and sub-agent capabilities
agent = create_deep_agent()

# Execute a research task
result = agent.invoke({
    "messages": [
        {"role": "user", "content": "Explain the difference between an Agent and a Chain."}
    ]
})

print(result["messages"][-1].content)
```

> [!NOTE]
> **Wait, why?** In high-stakes environments, you don't want an agent starting from scratch. By using a harness, the agent inherits a pre-defined "memory" of how to plan and use files, drastically reducing the number of turns needed to solve a problem.

### 🛑 Common Gotcha: API Key Scope

If you see an "Authentication Error," ensure your `OPENAI_API_KEY` is exported in the **same** terminal session where you run the script. API keys do not persist across different terminal windows unless added to your `.zshrc` or `.bashrc`.

### ✅ Module 1 Self-Check

- What is the difference between `create_deep_agent()` and a standard LangChain `ChatOpenAI` call?
- In the `result`, why is the final message usually an `AIMessage`?

---

## 🔧 Module 2: Customizing Brain & Hands

Now, let's make the agent our own. We'll swap the model to Claude 3.5 Sonnet and add a custom tool.

### Learning Lab: The Weather Agent

Create `custom_agent.py`:

```python
from langchain_core.tools import tool
from langchain.chat_models import init_chat_model
from deepagents import create_deep_agent

@tool
def get_weather(city: str):
    """Get the current weather for a specific city."""
    # In a real app, you'd call an API here
    return f"The weather in {city} is sunny, 72°F."

# 1. Swap the model (requires anthropic SDK: uv add anthropic)
model = init_chat_model("anthropic:claude-3-5-sonnet-latest")

# 2. Re-create the agent with custom components
agent = create_deep_agent(
    model=model,
    tools=[get_weather],
    system_prompt="You are a friendly travel assistant."
)

# Test it out!
agent.invoke({"messages": [{"role": "user", "content": "What's the weather in Tokyo?"}]})
```

---

## 🧠 Module 3: Sub-Agents & Task Planning

Deep Agents excels at **Planning**. It uses a `write_todos` tool to break down complex goals into smaller pieces.

### 🔍 Deep Dive: The Planning Cycle

Deep Agents uses a "Write-Then-Execute" pattern. When a complex prompt is received, the agent doesn't start calling tools immediately. Instead, it calls `write_todos`, which updates a stateful list in the LangGraph memory. This list serves as a **dynamic anchor**, preventing the agent from "getting lost" in long-running tasks.

### ✅ Module 3 Self-Check

- How does the `task` tool maintain a separate context window from the main agent?
- What would happen if the `researcher` sub-agent failed? Does it stop the whole process? (Hint: See "Error Handling" in the full docs).

### Challenge: Multi-Step Research

Try asking the agent:

> *"Research the top 3 AI papers of 2024, write a summary for each to a new file 'research.txt', and then create a sub-task to check for any critical critiques of those papers."*

---

## 🖥️ Module 4: The Deep Agents CLI

The SDK also powers a **TUI (Terminal User Interface)** — a "batteries-included" coding assistant that runs in your terminal.

### Installation & Run

```bash
# One-line installer
curl -LsSf https://raw.githubusercontent.com/langchain-ai/deepagents/main/libs/cli/scripts/install.sh | bash

# Fire it up
deepagents
```

**Key Features to Try:**

| Feature | Description |
| :--- | :--- |
| `/slash` commands | Quick actions for common tasks |
| Web search | Search the web directly from the prompt |
| Background shell | Execute shell commands in the background |

---

## 🌍 Exploration: Advanced Patterns

The core modules covered the foundation. To see how these principles scale to production, explore the **Advanced Patterns** in our examples directory:

| Pattern | Example | Learning Outcome |
| :---: | :--- | :--- |
| 🚀 **Recursive** | [deep_research](examples/deep_research/) | Master the "Thinking Tool" for multi-step web research and strategic reflection |
| 🏎️ **Heterogeneous** | [nvidia_deep_agent](examples/nvidia_deep_agent/) | Orchestrate frontier models with specialized GPU-accelerated research nodes |
| 🎨 **Asset Pipeline** | [content-builder](examples/content-builder-agent/) | Bundle persona memory, task skills, and image generation into a content engine |
| 📊 **Disclosure** | [text-to-sql](examples/text-to-sql-agent/) | Implement progressive schema exploration for lean, efficient SQL agents |
| 🔁 **Persistent** | [ralph_mode](examples/ralph_mode/) | Build long-running project loops with fresh context and Git-based memory |
| 📦 **Portable** | [downloading](examples/downloading_agents/) | Distribute and version "Brain Folders" as portable agent artifacts |
| 🌐 **Distributed** | [async-subagent](examples/async-subagent-server/) | Scale agents across infrastructure using the async Agent Protocol |

> [!TIP]
> **Recommended Path**: Start with `deep_research` to understand planning, then move to `async-subagent` to see how to host your agents as services.

---

## 🏁 Completion & Next Steps

Congratulations! You've successfully navigated the core features of Deep Agents.

### 📚 Resources for Further Learning

| Resource | Description |
| :--- | :--- |
| [Full Documentation](https://docs.langchain.com/oss/python/deepagents/overview) | Deep dives into ACP, custom skills, and sandboxing |
| [Examples Directory](examples/) | Pre-built patterns for different domains |
| [ArtiPortal Workshops](https://artiportal.com/workshops) | More interactive AI training |
| [Intro to Agents (LangChain)](https://python.langchain.com/docs/concepts/agents/) | Core primitives explained |
| [LangChain Academy](https://academy.langchain.com/) | Fast-paced courses on building with LangGraph |
| [LangSmith Dashboard](https://smith.langchain.com/) | Visualize and debug every agent turn in real time |

### 🆘 Support & Community

- **Lab Support**: Contact **labs@artiportal.com** for workshop help.
- **GitHub Issues**: Report bugs or request features.
- **LangChain Forum**: Connect with other agent builders.

---

## 📝 Workshop Summary & Key Takeaways

| Pillar | Insight |
| :--- | :--- |
| **Framework over Feature** | Deep Agents provides a pre-configured LangGraph architecture that tracks state and history automatically — solving the "blank page" problem. |
| **Autonomous Planning** | The `write_todos` tool creates a structured roadmap and follows it, significantly reducing mid-task drift. |
| **Modular Power** | Swap frontier models (GPT-4o, Claude 3.5) while keeping your custom tools and system prompts intact — provider-agnostic by design. |
| **Operational Efficiency** | Auto-summarization and file-based tool outputs manage token costs and context window limits — essential, not optional. |

**Final Challenge**: Take the `custom_agent.py` you built in Module 2 and integrate it with the Sub-Agent logic from Module 3. Can you build an agent that researches a city *and* provides a weather-based travel itinerary in a single run?

---

## 🛑 Workshop Cleanup & Security

> [!WARNING]
> Prevent unexpected charges: revoke keys and shut down infrastructure before you log off.

### Steps

| Step | Action |
| :---: | :--- |
| 1 | **Revoke API Keys** — OpenAI, Anthropic, Tavily, and LangSmith dashboard |
| 2 | **Stop Modal sandboxes** — `modal sandbox list` and terminate any active ones |
| 3 | **Kill local servers** — `Ctrl+C` any running `uvicorn` or `langgraph dev` processes |
| 4 | **Clear env vars** — remove keys from `.zshrc`/`.bashrc` and delete `.env` files |

```bash
rm -f .env
unset OPENAI_API_KEY ANTHROPIC_API_KEY TAVILY_API_KEY LANGSMITH_API_KEY
```

---

## 📖 Glossary of Terms

| Term | Definition |
| :--- | :--- |
| **Agent Harness** | The structural "plumbing" (state, tools, memory) that wraps around an LLM to make it functional. |
| **Skill** | A specific, file-based instruction (`SKILL.md`) that teaches the agent a new capability on the fly. |
| **Memory** | Persistent instructions stored in `AGENTS.md` that define the agent's persona and rules. |
| **Sub-Agent** | A specialized agent spawned by a "Supervisor" to handle a specific sub-task in isolation. |
| **LangGraph** | The underlying orchestration engine that manages the agent's stateful, cyclic workflow. |
| **TUI** | Terminal User Interface — the rich, interactive visual system used by the Deep Agents CLI. |

---

## 📚 Resources & Further Reading

> [!NOTE]
> **Origin & Acknowledgements**
> This repository is a specialized workshop fork of the original [Deep Agents](https://github.com/langchain-ai/deepagents) project by LangChain, Inc. It has been restructured and enhanced with pedagogical scaffolding, lab exercises, and detailed architectural guides by **ArtiPortal.com**.

### 🔰 Foundational

- **[Intro to Agents (LangChain Docs)](https://python.langchain.com/docs/concepts/agents/)**: Understanding the core primitives.
- **[LangChain Academy](https://academy.langchain.com/)**: Fast-paced courses on building with LangGraph.

### 🧪 Advanced Deep Dives

- **[Deep Research Pattern](examples/deep_research/README.md)**: Recursive search and task-based reflection loops.
- **[Multi-Agent Orchestration](examples/async-subagent-server/README.md)**: Supervisor-subagent communication.
- **[The Agentic RAG Pipeline](examples/text-to-sql-agent/README.md)**: Structured data retrieval.

### 🛠️ Developer Tools

- **[Deep Agents SDK Reference](libs/deepagents/README.md)**: Technical documentation for the core harness.
- **[LangSmith Dashboard](https://smith.langchain.com/)**: Visualize and debug every agent turn in real time.

---

<div align="center">

**Thank you for participating! We look forward to seeing what you build next.**

<br/>

![Python](https://img.shields.io/badge/python-3.11%2B-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)
![deepagents](https://img.shields.io/badge/deepagents-%E2%89%A50.0.34-purple)

<br/>

*© 2026 [ArtiPortal.com](https://artiportal.com) | Based on the MIT-licensed [LangChain Deep Agents](https://github.com/langchain-ai/deepagents) project*

</div>
