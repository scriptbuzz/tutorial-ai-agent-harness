<p align="center">
  <picture>
    <source media="(prefers-color-scheme: light)" srcset="../.github/images/logo-light.svg">
    <source media="(prefers-color-scheme: dark)" srcset="../.github/images/logo-dark.svg">
    <img alt="Deep Agents" src="../.github/images/logo-dark.svg" height="40"/>
  </picture>
</p>

<h3 align="center">Examples</h3>

<p align="center">
  Agents, patterns, and applications you can build with Deep Agents.
</p>

| Pattern | Example | Learning Outcome |
| :--- | :--- | :--- |
| 🚀 **Recursive** | [deep_research](deep_research/) | Master the "Thinking Tool" for multi-step web research and strategic reflection. |
| 🏎️ **Heterogeneous** | [nvidia_deep_agent](nvidia_deep_agent/) | Orchestrate frontier models with specialized GPU-accelerated research nodes. |
| 🎨 **Asset Pipeline** | [content-builder](content-builder-agent/) | Bundle persona memory, task skills, and image generation into a content engine. |
| 📊 **Disclosure** | [text-to-sql](text-to-sql-agent/) | Implement progressive schema exploration for lean, efficient SQL agents. |
| 🔁 **Persistent** | [ralph_mode](ralph_mode/) | Build long-running project loops with fresh context and Git-based memory. |
| 📦 **Portable** | [downloading](downloading_agents/) | Distribute and version "Brain Folders" as portable agent artifacts. |
| 🌐 **Distributed** | [async-subagent](async-subagent-server/) | Scale agents across infrastructure using the async Agent Protocol. |

Each example has its own README with setup instructions.

## Contributing an Example

See the [Contributing Guide](https://docs.langchain.com/oss/python/contributing/overview) for general contribution guidelines.

When adding a new example:

- **Use uv** for dependency management with a `pyproject.toml` and `uv.lock` (commit the lock file)
- **Pin to deepagents version** — use a version range (e.g., `>=0.3.5,<0.4.0`) in dependencies
- **Include a README** with clear setup and usage instructions
- **Add tests** for reusable utilities or non-trivial helper logic
- **Keep it focused** — each example should demonstrate one use-case or workflow
- **Follow the structure** of existing examples (see `deep_research/` or `text-to-sql-agent/` as references)
