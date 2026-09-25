# Credits & Acknowledgements

Jasper stands on the shoulders of remarkable open-source projects, research initiatives, and developer tools. This document acknowledges and honors the upstream innovations, architectural patterns, and engineering philosophies that directly inspired Jasper's systems.

---

## 🏛️ Projects & Inspirations

### Graphify
https://github.com/Graphify-Labs/graphify

**Inspired:** Jasper's memory system.

Graphify inspired the idea of making Jasper's persistent memory one large graph, allowing relationships between users, projects, preferences, decisions, skills, tools, and other information to be represented and queried as connected data.

---

### Strix
https://github.com/usestrix/strix

**Inspired:** Jasper's security capabilities.

Strix inspired Jasper's ability to actively test applications it has built, find vulnerabilities and loopholes, create patches, apply them, and test again to verify the fixes.

---

### 9Router
https://github.com/decolua/9router

**Inspired:** Jasper's native model federation and routing architecture.

Jasper is adapting useful parts of 9Router's architecture rather than using 9Router as an AI provider. This includes provider adapters, protocol translation, model combinations, fallback handling, request routing, and support for different AI providers through a unified system.

---

### Agency Agents
https://github.com/msitarzewski/agency-agents

**Inspired:** Jasper's specialist agent system.

Agency Agents inspired Jasper's use of focused specialist agents for different areas of work, such as architecture, frontend, backend, databases, security, QA, DevOps, and UI/UX.

Jasper determines which specialists are actually needed for a task instead of deploying every available agent.

---

### Mobile Harness
https://github.com/techjarves/Mobile-Harness

**Inspired:** Jasper's mobile development environment.

Mobile Harness helped inspire the idea of bringing a serious Linux development environment, terminal, AI coding capabilities, and flexible AI provider support to Android devices.

---

### Claude Agent SDK
https://code.claude.com/docs/en/agent-sdk/overview

**Inspired:** Jasper's coding agent.

The Claude Agent SDK is the SDK behind Claude Code and provides the foundation for Jasper's coding agent.

It also enables Jasper to remain compatible with the wider Claude Code ecosystem, allowing Jasper to work with things such as Claude Code skills, plugins, tools, and related workflows.

---

### Manus
https://manus.im/docs/introduction/welcome

**Inspired:** Jasper's general-purpose agent and browser capabilities.

Manus inspired the idea of making Jasper capable of much more than coding.

Jasper's general-purpose agent can use tools such as a browser to perform research, interact with websites, complete workflows, and handle tasks outside traditional software development.

---

### Ponytail
https://github.com/DietrichGebert/ponytail

**Inspired:** Jasper's Code Philosophy and Decision Ladder.

Ponytail inspired Jasper's Code Philosophy engine, making the coding agents write cleaner, minimal, and non-overengineered code through a strict decision ladder that prioritizes native platform APIs, reuses existing code, and minimizes third-party dependency churn.

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
