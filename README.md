# Jasper

> **Autonomous, privacy-first AI development workstation and Linux runtime for Android.**

Jasper transforms your smartphone into a sovereign, desktop-class development environment. Built directly on top of a native Android Linux userspace, Jasper combines a touch-ergonomic code editor, multi-session persistent terminals, an autonomous dual-swarm agent engine, and on-device AI inference—operating 100% offline with zero required accounts.

---

## 🧭 The Vision

```
Mobile IDE  ──▶  Mobile Workstation  ──▶  Autonomous Dual-Swarm Studio  ──▶  Sovereign Pocket Lab
```

Jasper is not simply a code editor or a passive chatbot. It is an active software engineer and execution runtime in your pocket:
* **The Phone as a Complete Workstation**: Full GNU C Library userspace running native toolchains (`node`, `python`, `git`, `wrangler`, `cargo`) locally without root via modern PRoot.
* **Dual-Swarm Autonomous Engineering**: **Blue Team** builds, designs, and compiles features; **Red Team** validates surfaces adversarial-style, patches vulnerabilities, and hardens code automatically before task completion.
* **Code Philosophy (Zero AI Bloat)**: Enforces the 5-rung Decision Ladder to eradicate boilerplate, favor native platform APIs, and prevent unnecessary dependency churn on mobile.
* **Constitutional Policy Engine**: The agent proposes actions; the runtime enforces strict security boundaries, human confirmation gates, and AST validation.
* **Air-Gapped & Sovereign**: Works completely offline using quantized local GGUF models (`llama.cpp`) or seamlessly switches to cloud providers (OpenRouter, Anthropic, OpenAI, custom endpoints).

---

## 🏛️ Core Architecture

```
                    ┌─────────────────────────┐
                    │          USER           │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │     AI ORCHESTRATOR     │
                    └────────────┬────────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        ▼                        ▼                        ▼
  ┌────────────┐          ┌────────────┐           ┌────────────┐
  │ BLUE TEAM  │          │  RED TEAM  │           │   MEMORY   │
  │ (Builders) │          │ (Auditors) │           │(Persistent)│
  └─────┬──────┘          └─────┬──────┘           └─────┬──────┘
        │                        │                        │
        └────────────────────────┼────────────────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │   POLICY & GUARDRAILS   │
                    │  Read: Auto-allowed     │
                    │  Write: Scoped          │
                    │  Irreversible: Confirm  │
                    └────────────┬────────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        ▼                        ▼                        ▼
 ┌──────────────┐        ┌──────────────┐         ┌──────────────┐
 │ NATIVE PROOT │        │     MCP      │         │   COMPOSIO   │
 │ LINUX RUNTIME│        │Native/Custom │         │     SDK      │
 └──────┬───────┘        └──────────────┘         └──────────────┘
        │
   ┌────┴────┬───────────┐
   ▼         ▼           ▼
 Linux   Mobile IDE   In-App
 Shell   (Editor)    Browser
   │         │           │
   └─────────┼───────────┘
             ▼
      LOCAL PROJECTS
```

---

## 📚 Technical Documentation & Specifications

Jasper's system architecture, technical design, and implementation specifications are organized into dedicated reference documents:

* 📋 **[`docs/features.md`](./docs/features.md)**: Complete user-facing features, dual-swarm workflow, filesystem boundaries, WakeLock persistence, and project lifecycle.
* 🎨 **[`docs/ui_specs.md`](./docs/ui_specs.md)**: Visual specifications, mobile ergonomics, touch targets, keyboard accessory bar, mission cards, and drawer components.
* ⚙️ **[`docs/logic.md`](./docs/logic.md)**: Complete system logic, PRoot lifecycle, AST route discovery, 10-agent Red Swarm state machines, Decision Ladder engine, and concurrency coordination.
* 🤝 **[`CREDITS.md`](./CREDITS.md)**: Full acknowledgements and links to the upstream open-source projects, tools, and research architectures that inspired Jasper.

---

## ⚡ Highlights at a Glance

| Pillar | Capability |
| :--- | :--- |
| **Linux Subsystem** | ARM64 rootless PRoot v5.4+ with seccomp acceleration and Ubuntu 24.04 LTS userspace. |
| **Autonomous Swarms** | Max-10 concurrent sub-agent execution engine with automatic batch scheduling. |
| **Code Philosophy** | Strict 5-rung Decision Ladder (`Lite`, `Full`, `Ultra`) eliminating AI boilerplate and dependency bloat. |
| **Adversarial Red Team** | Ported 10-agent security audit swarm with PRoot loopback validation and auto-patching. |
| **Mobile Ergonomics** | CodeMirror 6 with custom virtual symbol keyboard bar, gesture zoom locks, and tabbed PTY terminals. |
| **Universal Web Preview** | Dual-engine route discovery (static AST scraper + dynamic loopback sniffer) with auto-starting dev daemons. |
| **Local Inference** | On-device `llama.cpp` ARM NEON runner with PocketPal-inspired RAM safety tiers for 6GB mobile hardware. |

---

## 🛠️ Technology Stack

* **Mobile Container**: Capacitor (Android native bridge, WakeLocks, scoped storage)
* **Frontend UI**: React 19, TypeScript, Tailwind CSS, Motion
* **Editor & Terminal**: CodeMirror 6, xterm.js with loopback WebSocket PTY multiplexing
* **Linux Userspace**: PRoot ARM64, Ubuntu 24.04 Rootfs (`glibc 2.38+`)
* **Local Inference**: `llama.cpp` ARM64 NEON, Qwen2.5-Coder GGUF models
* **Tooling Protocol**: Model Context Protocol (MCP), Composio SDK

---

*For detailed architectural mechanics, refer to the [`docs/`](./docs/) directory.*
