# Jasper

> **Autonomous, privacy-first AI development workstation and Linux runtime for Android.**

Jasper transforms your smartphone into a sovereign, desktop-class development environment. Built directly on top of a native Android Linux userspace, Jasper combines a mobile-first code editor, persistent terminal sessions, autonomous agent orchestration, and on-device AI inference—operating 100% offline with zero required accounts.

---

## 🧭 The Vision

```
Mobile IDE  ──▶  Mobile Workstation  ──▶  AI Development Environment  ──▶  Autonomous Digital Agent
```

Jasper is not simply an editor or a passive chatbot. It is an active software engineer and execution engine that works alongside you on your phone:
* **The Phone as a Complete Workstation**: Native toolchains (`node`, `python`, `git`, `wrangler`, `clang`) running locally without root.
* **Autonomous Agent Orchestration**: A hierarchy of specialized sub-agents that plan, write code, run tests, diagnose errors, and manage git.
* **Constitutional Policy Engine**: The agent proposes actions; the runtime enforces security boundaries and human confirmation.
* **Air-Gapped & Sovereign**: Works completely offline using quantized local models or connects to cloud models when requested.

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
  │ SUB-AGENTS │          │   SKILLS   │           │   MEMORY   │
  │ (~300 Spec)│          │ (User/Ext) │           │(Persistent)│
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

## ⚡ Key Systems

### 1. Embedded Linux Userspace (PRoot Engine)
* **Modern PRoot Core (v5.4+)**: Features updated syscall emulation (`clone3`, `epoll_pwait2`, `statx`) and seccomp acceleration for modern Android (Android 11–15+).
* **Ubuntu 24.04 LTS / Debian 12 Rootfs**: Full GNU C Library (`glibc 2.38+`), native OpenSSL 3.x, and standard Linux toolchains.
* **Deterministic Environment & Path Management**:
  * Guarantees `$PATH` persistence across interactive and non-interactive subshells:
    ```bash
    export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$HOME/.local/bin:$HOME/.npm-global/bin"
    ```
  * Pre-configured npm global prefix (`/usr/local`) preventing `command not found` errors.
  * Native compatibility with tools that normally fail on Android (e.g., Cloudflare `wrangler`, modern `npm`, `cargo`, `pip`).

### 2. Privacy-First & 100% Offline by Default
* **Zero Authentication**: No logins, no accounts, no telemetry, no tracking.
* **Local Inference via `llama.cpp`**:
  * Optimized for ARM64 with NEON vector instructions.
  * Tailored for devices with 6GB RAM (e.g., POCO C85): loads compact, high-performance coding models like **Qwen2.5-Coder 1.5B/3B (Q4_K_M)** within a 1.2GB–2.2GB memory footprint.
  * In-app model manager with resumable download progress and SHA256 integrity verification.
* **Provider Abstraction**: Switch seamlessly between local GGUF models, Anthropic Claude, OpenAI, OpenRouter, 9router, or custom API endpoints.

### 3. Native Mobile IDE & Terminal
* **Touch-Ergonomic Editor**: Built on CodeMirror 6 with syntax highlighting, search/replace, code navigation, and project-wide diagnostics.
* **Virtual Keyboard Accessory Bar**: Dedicated strip docked above soft keyboards providing instant access to:
  * `{`, `}`, `[`, `]`, `(`, `)`, `;`, `|`, `/`, `\`, `_`, `-`, `~`, `"`, `'`, `Tab`, `Esc`, `Ctrl`.
* **Integrated PTY Terminal**: Multi-tab xterm.js sessions backed by real Unix pseudoterminals over internal low-latency loopback WebSockets.
* **Background Persistence & Wake Locks**: Android Foreground Service with persistent notifications prevents process termination and keeps compilers/dev servers running when the screen dims.

### 4. Sub-Agent Fabric & Skills Engine
* **~300 Specialized Agents**: Hidden internal talent pool (Frontend, Backend, DevOps, Architect, Security Auditor, Test Engineer) coordinated automatically by the primary orchestrator.
* **Minimal Ambient UI**: Instead of overwhelming the user with massive agent lists, Jasper displays a live activity timeline pill:
  ```
  ✔ Architect Agent: Outlined project structure (1.2s)
  ✔ Dependency Resolver: Running npm install (4.8s)
  ⚡ Frontend Engineer: Generating responsive view (in progress...)
  ```
* **Extensible Skills**:
  * **Agents** = *Who* does the work.
  * **Skills** = *How* the work is done.
  * Manage, create, toggle, and inspect custom skills that guide agent behavior.

### 5. Policy Engine & Human Confirmation
```
READ Operations (Auto)       ──▶ Read files, git status, inspect preview
WRITE Operations (Scoped)    ──▶ Edit project source within workspace root
IRREVERSIBLE (Requires Sign) ──▶ rm -rf, git push --force, install system tools, credential connect
```
When an irreversible action is triggered, Jasper presents an interactive **Policy Action Sheet** detailing the requesting agent, exact command/diff, risk level, and allows one-tap approval or rejection.

### 6. Composio & Model Context Protocol (MCP)
* **Native & Custom MCP**: Connect arbitrary MCP servers for extended tooling.
* **Composio SDK**: Dynamic OAuth discovery for external tools (GitHub, Vercel, Supabase, Cloudflare, Linear, Slack) directly within the mobile UI without leaving the app.

---

## 🗄️ Project & Storage Structure

All projects reside in POSIX-compliant internal storage:
```
/data/data/com.jasper.app/files/home/
├── .jasper/
│   ├── models/            # Downloaded .gguf local weights
│   ├── skills/            # Custom and built-in agent skills
│   └── memory/            # Persistent contextual project memory
└── workspace/
    └── <project_name>/    # Standard Linux directory structure with POSIX permissions
```
* **Exporting**: One-tap export to GitHub repositories or `.zip` archives saved directly into the device's Android `Downloads` folder.

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend UI** | React 19, TypeScript, Tailwind CSS, Lucide Icons, Motion |
| **Mobile Runtime** | Capacitor (Native Android Container, Wake Lock, Scoped Storage) |
| **Editor** | CodeMirror 6 (Mobile touch & virtual key extensions) |
| **Terminal** | xterm.js with WebSocket PTY bridge |
| **Subsystem** | PRoot (ARM64 v5.4+ with seccomp patch), Ubuntu 24.04 Rootfs |
| **Local AI** | `llama.cpp` (ARM NEON optimized), Qwen2.5-Coder GGUF models |
| **Tool Protocol** | Model Context Protocol (MCP), Composio SDK |

---

## 📜 Core Philosophy

1. **AI works alongside the developer, never replaces them.** Manual editor and terminal control are always available.
2. **The agent requests; the runtime decides.** Real security policies are enforced in code, not left to prompt luck.
3. **Zero cloud dependence.** A developer stranded without Wi-Fi should still possess a complete, autonomous software studio in their pocket.
4. **No marketing fluff or bloat.** High performance, clean aesthetics, and immediate utility.
