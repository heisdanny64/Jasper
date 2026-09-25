# Credits & Acknowledgements

Jasper stands on the shoulders of remarkable open-source projects, research initiatives, and developer tools. This document acknowledges and honors the upstream innovations, architectural patterns, and engineering philosophies that directly inspired Jasper's systems.

---

## 🏛️ Direct Inspirations & Ported Architectures

### 1. [Strix](https://github.com/usestrix/strix)
* **Website / Repo**: [https://github.com/usestrix/strix](https://github.com/usestrix/strix)
* **What It Is**: An open-source autonomous AI penetration testing tool and multi-agent cybersecurity framework designed to identify, validate, and remediate vulnerabilities in codebases.
* **What It Inspired in Jasper**:
  * **Jasper's 10-Agent Red Team Swarm**: The architecture of deploying an adversarial swarm of specialized sub-agents (Lead Orchestrator, Route Enumerator, Secret Auditor, Config Auditor, Injection Specialist, IDOR Specialist, Auth Hardener, Client/SSRF Specialist, Supply Chain Auditor, and Dynamic Patch Synthesizer).
  * **Dynamic Sandbox Behavioral Validation**: Testing endpoints against local runtime daemons inside PRoot to eliminate false positives.
  * **Automated Self-Hardening**: Rather than merely reporting warnings, the auditor automatically writes defensive AST patches, applies unified diffs, and verifies compilation.

### 2. [Ponytail](https://github.com/DietrichGebert/ponytail)
* **Website / Repo**: [https://github.com/DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)
* **What It Is**: An AI coding ruleset and skill designed to make AI agents "think like the laziest senior developer in the room" by avoiding unnecessary complexity, bloat, and boilerplate.
* **What It Inspired in Jasper**:
  * **Code Philosophy System**: Jasper's configurable discipline profiles (`Lite`, `Full`, `Ultra`).
  * **The 5-Rung Decision Ladder**: Forcing the Architect and Coder agents to verify whether code needs to be built at all, if it already exists in the project graph, if native runtime APIs can solve it, and strictly minimizing new dependencies before writing code.
  * **Anti-Overengineering & Mobile Efficiency**: Eliminating npm dependency bloat to drastically speed up PRoot build times and preserve mobile RAM and battery.

### 3. [Graphify](https://github.com/Graphify-AI/graphify)
* **Website / Repo**: [https://github.com/Graphify-AI/graphify](https://github.com/Graphify-AI/graphify)
* **What It Is**: An AST-based code graph and dependency visualizer that indexes complex codebases into structured semantic graphs.
* **What It Inspired in Jasper**:
  * **Project Knowledge Graph (AST Index)**: Powers Jasper's cross-file context retrieval, symbol references, and component dependency maps.
  * **Duplication Guard**: Enables Ponytail's decision ladder to query existing utility functions, hooks, and schemas across the codebase before generating duplicate code.
  * **Surface Mapping for Red Team**: Enables the security orchestrator to parse the full route tree and input boundaries instantly.

### 4. [Agency Agents](https://github.com/agencyenterprise/agency-agents)
* **Website / Repo**: [https://github.com/agencyenterprise/agency-agents](https://github.com/agencyenterprise/agency-agents)
* **What It Is**: A curated repository of specialized AI agent roles, prompt architectures, and division-of-labor specifications.
* **What It Inspired in Jasper**:
  * **The ~300 Specialized Sub-Agent Roster**: The taxonomic design and role boundaries for Jasper's sub-agents across Frontend, Backend, Database, Testing, DevOps, and Architecture.
  * **Role Encapsulation**: Ensuring agents maintain strict, single-responsibility contracts during execution phases.

### 5. [Claude's Agent SDK (Anthropic)](https://github.com/anthropics/anthropic-sdk-typescript)
* **Website / Repo**: [https://github.com/anthropics/anthropic-sdk-typescript](https://github.com/anthropics/anthropic-sdk-typescript) • [Anthropic Documentation](https://docs.anthropic.com/)
* **What It Is**: The official SDK and agentic design patterns for building tool-using, recursive problem-solving workflows with Claude.
* **What It Inspired in Jasper**:
  * **Mission Card Step Checklist & Tool-Calling Protocol**: The structured loop of tool call proposal, argument validation, execution, and observation feedback.
  * **Context Compaction & Memory Strategy**: Patterns for managing long-horizon reasoning within strict token budgets.

### 6. [Manus](https://github.com/manus-ai)
* **Website / Repo**: [https://manus.im](https://manus.im)
* **What It Is**: An autonomous general-purpose AI agent capable of multi-step execution, dynamic environment setup, and end-to-end task completion.
* **What It Inspired in Jasper**:
  * **Autonomous Task Completion Loop**: The principle of running multi-turn loops from prompt to verified end state without forcing the human to babysit every file write or command execution.
  * **Ambient Execution Timeline**: Clean, non-intrusive UI representations of agent thinking, tool usage, and milestones.

### 7. [9router](https://github.com/9router)
* **Website / Repo**: [https://github.com/9router](https://github.com/9router)
* **What It Is**: An intelligent multi-provider LLM reverse proxy and routing engine.
* **What It Inspired in Jasper**:
  * **Multi-Provider AI Gateway & Fallbacks**: Seamless routing between local on-device inference (`llama.cpp`), OpenRouter, Anthropic, OpenAI, and custom endpoints.
  * **Automatic Failover**: Transparently retrying or rerouting requests on rate limits or service degradation.

### 8. [Mobile Harness / PocketPal AI](https://github.com/a-ghorbani/pocketpal-ai)
* **Website / Repo**: [https://github.com/a-ghorbani/pocketpal-ai](https://github.com/a-ghorbani/pocketpal-ai)
* **What It Is**: An open-source mobile application for running local LLMs on Android and iOS using `llama.cpp`.
* **What It Inspired in Jasper**:
  * **Hardware Safety Analyzer & Memory Tiering**: RAM safety thresholds, LMK (Low Memory Killer) protection algorithms, and GGUF quantization selection based on mobile device specs.
  * **ARM64 Native Inference Optimization**: Dynamic thread allocation based on device thermal status.

---

## 🛠️ Core Infrastructure & Open-Source Foundations

Jasper also relies on and extends foundational open-source engineering achievements:

* **[PRoot](https://proot-me.github.io/)**: Rootless Linux userspace and syscall translation on Android.
* **[llama.cpp](https://github.com/ggerganov/llama.cpp)**: High-performance, quantized local LLM inference on ARM64 NEON.
* **[CodeMirror 6](https://codemirror.net/)**: Extensible, touch-friendly mobile code editor framework.
* **[xterm.js](https://xtermjs.org/)**: Web-based terminal emulator component.
* **[Capacitor](https://capacitorjs.com/)**: Cross-platform native runtime connecting web interfaces to Android APIs.
* **[Model Context Protocol (MCP)](https://modelcontextprotocol.io/)**: Open standard for connecting AI models to data sources and tools.
* **[Composio](https://composio.dev/)**: Tooling and external service integration fabric.

---

*Note: For the exact technical adaptations, state machine logic, and implementation code ported into Jasper, please consult [`docs/logic.md`](./docs/logic.md).*
