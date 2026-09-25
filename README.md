# Jasper

> Your development workstation. Anywhere.

Jasper is a privacy-first mobile development workstation built for developers who don't have a PC, need to work on the go, or simply want a complete development environment in their pocket.

Built by [Spün](https://byspun.xyz).

**The goal is simple: Give developers a serious development workstation without requiring a traditional PC.**

```text
                         JASPER
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
      Brain              Hands               Eyes
        │                  │                  │
    AI Models          Agent SDK        Vision Models
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                     Jasper Runtime
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
     Memory              Tools               Linux
       │                   │                   │
  Memory Graph       MCP / Skills /          PRoot
                    Browser / Files
```

These systems allow Jasper to reason, remember, see, interact with tools, and actually perform work on device.


## What Jasper Combines

| Core Pillar | What It Powers |
| :--- | :--- |
| **Linux Subsystem** | Real ARM64 Linux userspace via PRoot (Node.js, Python, Git, Rust, standard package managers) |
| **Mobile IDE & Terminal** | CodeMirror touch editor with accessory symbol bar, xterm.js persistent PTY terminals |
| **Workspaces & Previews** | Isolated project storage, automated port detection, live in-app web previews |
| **Dual AI Agents** | Autonomous Coding Agent (Claude Agent SDK-powered) + General-Purpose Agent (browser & research) |
| **Model Federation** | Multi-provider routing, protocol translation, combo fallback pipelines, and local GGUF models |
| **Persistent Memory** | Connected knowledge graph mapping preferences, architectures, skills, tools, and project history |
| **Self-Hardening Security** | Multi-agent adversarial auditing, sandbox validation, automated patching, and regression verification |


## Jasper Isn't Just an AI Chatbot

Jasper can talk to you, but conversation isn't the point. Jasper can actually work.

### Autonomous Coding Agent
Built around Anthropic's Claude Agent SDK—remaining fully compatible with Claude Code skills, plugins, and workflows:
* Understands existing codebases and project structures
* Creates and edits files, refactors code, and manages dependencies
* Executes commands, runs test suites, and debugs failures
* Starts development daemons, inspects web previews, and self-heals errors

### General-Purpose Agent
Coding is one of Jasper's abilities, not its entire identity. The general-purpose agent leverages browser automation and external tools to:
* Research documentation, libraries, and real-time information
* Navigate dynamic web applications and complete multi-step online workflows
* Perform research and operational tasks outside the terminal and code editor


## A Real Development Environment in Your Pocket

Jasper runs a true Linux userspace directly on Android without requiring a remote development server or root access:
* **Toolchains**: Node.js, Python, Rust, Git, and package managers running natively in PRoot
* **Persistent Terminals**: Multi-session PTY shells with xterm.js and background WakeLock support
* **On-Device Storage**: Projects live directly on your phone's storage and can be worked on completely offline


## Your AI, Your Models

Jasper isn't tied to a single AI provider. Its native model federation layer provides:
* **Provider Adapters & Protocol Translation**: Seamless switching between cloud endpoints and local engines
* **Intelligent Routing & Fallbacks**: Model combinations, rate-limit failovers, load balancing, and vision handoffs
* **Local On-Device Models**: High-performance local inference via quantized GGUF models on mobile ARM64 hardware


## Built for Privacy & User Ownership

* **No Mandatory Account**: Use Jasper without forced logins or platform lock-in
* **Zero Telemetry by Default**: Your source code, terminal sessions, and queries stay on your hardware
* **Local Backups**: Encrypted `.jasp` portable archives for full backup and restore
* **Offline-Capable**: Full development loop works without an active internet connection


## Security & Self-Hardening

Jasper doesn't just build software—it actively secures what it builds:
1. **Analyze**: Examines routes, entry points, dependencies, and AST boundaries
2. **Find**: Detects injection, broken access control (IDOR), secret leaks, and misconfigurations
3. **Validate**: Verifies vulnerabilities inside the local PRoot sandbox with zero false positives
4. **Patch & Re-Test**: Synthesizes defensive code patches, applies unified diffs, and re-compiles


## Connected Memory Graph

Instead of treating every conversation as an isolated session, Jasper builds a connected knowledge graph that maintains long-term context:
* User preferences & coding style
* Project architecture & design decisions
* Recurring development patterns & conventions
* Tools, skills, active dependencies, and verified historical checkpoints


## Built for Mobile Ergonomics

Jasper isn't a desktop IDE awkwardly shrunk down to a smartphone screen:
* Touch-first controls and gesture-driven drawer navigation
* Dedicated virtual accessory keyboard bar for code symbols
* Non-blocking background builds with Android persistent foreground notifications
* Hardware-aware resource protection against Low Memory Killer (LMK) events


## Documentation

Jasper's architecture and specifications are documented across focused reference guides:

* 📋 **[`docs/features.md`](./docs/features.md)** — Detailed capabilities, agent tools, WakeLock architecture, and project lifecycle
* ⚙️ **[`docs/logic.md`](./docs/logic.md)** — Core engineering logic, PRoot internals, AST route discovery, and agent state machines
* 🎨 **[`docs/ui_specs.md`](./docs/ui_specs.md)** — Mobile UI design system, touch ergonomics, screen wireframes, and keyboard specs
* 🤝 **[`CREDITS.md`](./CREDITS.md)** — Open-source projects, research, and upstream tools that helped shape Jasper


## Project Status

**🚧 Early Development**

Jasper is currently in the research, architecture, and UI/UX specification phase before implementation begins.


Jasper is a project by [Spün](https://byspun.xyz).

> Less complexity. More seamless technology.
