# ⚙️ Jasper: Technical Implementation & Architecture Specification (`logic.md`)

> **Document Type:** Technical & Engineering Implementation Guide  
> **Target Runtime:** Android (Capacitor Container + React 19 + TypeScript + Native Linux PRoot)  
> **Referenced Repositories & Engines:**
> - **9Router:** [`https://github.com/decolua/9router`](https://github.com/decolua/9router) (Provider federation, translation, combos, token compression)
> - **Graphify:** Knowledge Graph & AST Memory Representation
> - **llama.cpp:** Native ARM64 Local LLM Inference Daemon
> - **Claude Agent SDK:** Autonomous Tool-Use & Agentic Loop Architecture
> **Date:** September 2026

---

## 📑 Table of Contents

1. [High-Level System Architecture](#1-high-level-system-architecture)
2. [Claude Agent SDK Integration & Agentic Execution Loop](#2-claude-agent-sdk-integration--agentic-execution-loop)
3. [9Router Native Port & Federation Engine](#3-9router-native-port--federation-engine)
   - 3.1. Universal Protocol Translation Layer (Anthropic ⇄ OpenAI ⇄ Gemini)
   - 3.2. Streaming SSE Bidirectional Transformer
   - 3.3. RTK (Reduced Token Kit) Token Saver
   - 3.4. Vision & Reasoning Capability Detection Engine
   - 3.5. Dedicated Vision Adapter & Multimodal Handoff
   - 3.6. Typed Combos & Load Balancing Engine
   - 3.7. External Tool Connectors (Google Antigravity & GitHub Models)
4. [Graphify Cognitive Memory & AST Code Graph Engine](#4-graphify-cognitive-memory--ast-code-graph-engine)
   - 4.1. Tree-sitter AST Parsing & Code Knowledge Extraction
   - 4.2. Hybrid Graph-Vector Context Retrieval
   - 4.3. Dual Memory Graphs (Global Persona vs. Project Isolation)
   - 4.4. Memory Pruning on Project Deletion
5. [Local On-Device Inference Engine (`llama.cpp` + Qwen2.5-Coder)](#5-local-on-device-inference-engine-llamacpp--qwen25-coder)
   - 5.1. ARM64 Compilation & Assembly Micro-Kernels
   - 5.2. Memory Mapping (`mmap`) & FlashAttention KV Cache
   - 5.3. Dynamic Low-Memory Killer (LMK) Protection & Idle Unload
   - 5.4. Hardware Safety Analyzer & PocketPal Risk Scoring
6. [Universal Route Discovery Engine (Web Preview)](#6-universal-route-discovery-engine-web-preview)
   - 6.1. Static AST Route Scraper
   - 6.2. Dynamic Iframe Loopback Synchronization
7. [Mobile PRoot Terminal & Multi-Session PTY Multiplexer](#7-mobile-proot-terminal--multi-session-pty-multiplexer)
8. [Autonomous Dev Server Lifecycle & PTY Port Sniffer](#8-autonomous-dev-server-lifecycle--pty-port-sniffer)
9. [Real-Time Error Interception & Self-Healing Pipeline](#9-real-time-error-interception--self-healing-pipeline)
10. [Dual WakeLock & Android Persistent Foreground Architecture](#10-dual-wakelock--android-persistent-foreground-architecture)
11. [Red Team Swarm Architecture & Automated Self-Hardening (Ported from Strix)](#11-red-team-swarm-architecture--automated-self-hardening-ported-from-strix)
    - 11.1. Dual-Swarm Sequential Pipeline
    - 11.2. The 10-Agent Red Swarm Specialization Matrix
    - 11.3. PRoot Sandbox Behavioral Validation (Zero False Positives)
    - 11.4. Automated Defensive Patch Synthesis & AST Rewriting
    - 11.5. Pre-Push Security Interception Hook
12. [Code Philosophy Engine & Decision Ladder (Ported from Ponytail)](#12-code-philosophy-engine--decision-ladder-ported-from-ponytail)
    - 12.1. The 5-Rung Decision Ladder Algorithmic Contract
    - 12.2. Graphify Knowledge Graph Deduplication Hook
    - 12.3. Platform Standard API Substitution Heuristics
    - 12.4. Intensity Profile State Machine (`Lite`, `Full`, `Ultra`)

---

## 1. High-Level System Architecture

Jasper runs entirely on the host Android device without relying on remote virtual machines or cloud compute servers.

```
┌────────────────────────────────────────────────────────────────────────┐
│                      CAPACITOR WEBVIEW CONTAINER                       │
│  • React 19 + TypeScript + Tailwind CSS v4 + Shadcn UI + Hugeicons     │
│  • CodeMirror 6 Code Editor + xterm.js Terminal Canvas                 │
│  • Dedicated Web Preview Iframe (`http://localhost:<dev_port>`)       │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ IPC Bridge (Capacitor Plugin / Local WebSocket)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                    NODE.JS / TYPESCRIPT RUNTIME CORE                   │
├────────────────────────────────────────────────────────────────────────┤
│  1. Agent Core (Claude Agent SDK Loop, Prompts, Self-Correction)       │
│  2. 9Router Engine (Translation, Combos, Vision Adapter, RTK Saver)    │
│  3. Graphify Engine (Tree-sitter AST, Semantic Memory Graph, Pruning)  │
│  4. Route Discovery Engine (Static AST Scanner + Dynamic Loopback Sync)│
└───────────────────┬────────────────────────────────┬───────────────────┘
                    │                                │
                    ▼                                ▼
┌──────────────────────────────────────┐ ┌───────────────────────────────┐
│     ROOTLESS LINUX ENVIRONMENT       │ │   LOCAL INFERENCE DAEMON      │
│               (PRoot)                │ │         (`llama.cpp`)         │
├──────────────────────────────────────┤ ├───────────────────────────────┤
│ • Ubuntu ARM64 Rootfs                │ │ • Compiled with NEON +        │
│ • Real PTY Sessions (Node-pty)       │ │   Arm KleidiAI Micro-kernels  │
│ • Tooling: Node, Python, Git, Cargo  │ │ • Memory-mapped Q4_K_M GGUF   │
│ • User Workspaces (`~/workspace/`)   │ │ • Bound to `127.0.0.1:8080`   │
└──────────────────────────────────────┘ └───────────────────────────────┘
```

---

## 2. Claude Agent SDK Integration & Agentic Execution Loop

Jasper implements the autonomous agent loop following the **Claude Agent SDK** architectural pattern:

### 2.1. The Continuous Execution Loop
```
   ┌──────────────────────────────────────────────────────────┐
   │                     USER INTENT                          │
   │           "Create a responsive dashboard page"           │
   └────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
   ┌──────────────────────────────────────────────────────────┐
   │ 1. CONTEXT INGESTION (Graphify + RTK)                    │
   │    • Semantic search retrieves relevant AST subgraphs    │
   │    • Injects project schemas, AGENTS.md, & conventions   │
   └────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
   ┌──────────────────────────────────────────────────────────┐
   │ 2. MODEL GENERATION (Via 9Router Translation Engine)      │
   │    • Calls active model/combo (Claude, DeepSeek, Qwen)   │
   │    • Emits structured tool calls with JSONSchema args    │
   └────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
   ┌──────────────────────────────────────────────────────────┐
   │ 3. AGENT TOOL EXECUTION (Inside PRoot)                   │
   │    • `read_file`, `write_file`, `edit_file`               │
   │    • `execute_command` (e.g. `npm install`, `vitest`)    │
   └────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
   ┌──────────────────────────────────────────────────────────┐
   │ 4. OBSERVATION & CRITIC EVALUATION                       │
   │    • Output captured and compressed by RTK Token Saver   │
   │    • Evaluates exit code, stderr, and AST syntax errors  │
   └────────────────────────────┬─────────────────────────────┘
                                │
            ┌───────────────────┴───────────────────┐
            │ Success?                              │
            ▼                                       ▼
       [YES: STOP]                             [NO: RE-LOOP]
  Update UI, notify user               Inject error into history,
                                       execute self-correction step
```

### 2.2. Standardized Agent Tool Definitions
The Agent SDK exposes discrete, atomic tools inside PRoot:
* `file_read(path, start_line, end_line)`: Line-sliced reading for large files.
* `file_write(path, content)`: Complete file creation.
* `file_edit(path, old_content, new_content)`: Precise surgical text replacement.
* `directory_list(path, recursive)`: Filesystem discovery.
* `bash_run(command, timeout_ms)`: Interactive command execution in dedicated PTY.
* `web_preview_inspect(route)`: Captures DOM/screenshot for visual self-correction.

---

## 3. 9Router Native Port & Federation Engine
*Reference Repository: [`https://github.com/decolua/9router`](https://github.com/decolua/9router)*

Jasper natively integrates 9Router's complete routing, formatting, and model orchestration architecture directly into TypeScript without external daemon dependencies.

### 3.1. Universal Protocol Translation Layer (Anthropic ⇄ OpenAI ⇄ Gemini)
The Agent SDK produces Anthropic Messages API calls (`/v1/messages`). 9Router’s translation layer converts these into the native payload formats of external providers:

```
[Agent SDK: Anthropic /v1/messages]
               │
               ▼
┌─────────────────────────────────────────────────────────────┐
│ 9ROUTER TRANSLATION MATRIX                                  │
├─────────────────────────────────────────────────────────────┤
│ Target Provider       │ Target Endpoint & Format            │
├───────────────────────┼─────────────────────────────────────┤
│ Anthropic             │ Direct Pass-through (/v1/messages)  │
│ OpenAI / Groq / vLLM  │ Translated to /v1/chat/completions  │
│ DeepSeek              │ OpenAI format with reasoning_content│
│ Google Gemini         │ Translated to :generateContent API  │
│ Local llama-server    │ Translated to local OpenAI format   │
└─────────────────────────────────────────────────────────────┘
```

#### Transformation Rules:
1. **System Prompt**: Anthropic `system: "..."` is mapped to OpenAI `{"role": "system", "content": "..."}` or Gemini `systemInstruction`.
2. **Tool Definitions**:
   * Anthropic: `{ name, description, input_schema: { type: "object", properties: {...} } }`
   * OpenAI: `{ type: "function", function: { name, description, parameters: {...} } }`
   * Gemini: `{ functionDeclarations: [{ name, description, parameters: {...} }] }`
3. **Tool Call Execution & Responses**:
   * Anthropic `tool_use` (with `id`) ➔ OpenAI `tool_calls` array with `function: { name, arguments: JSON.stringify(args) }`.
   * Anthropic `tool_result` ➔ OpenAI `{"role": "tool", "tool_call_id": id, "content": output}`.

### 3.2. Streaming SSE Bidirectional Transformer
To support real-time token streaming in mobile chats, the translation layer intercepts Server-Sent Events (SSE):
* Listens for OpenAI `choices[0].delta.content` chunks.
* Emits corresponding Anthropic `content_block_delta` SSE packets.
* Listens for OpenAI `choices[0].delta.tool_calls` chunks and progressively accumulates arguments, emitting Anthropic `input_json_delta` packets.
* On OpenAI `finish_reason: "stop"` or `"tool_calls"`, emits Anthropic `message_delta` with `stop_reason` followed by `message_stop`.

### 3.3. RTK (Reduced Token Kit) Token Saver
Coding agents burn substantial context windows ingesting verbose build outputs. The RTK engine cleanses inputs before dispatch:
* **`git diff` Minimization**: Drops unchanged context lines beyond 3 anchor lines; strips excessive whitespace while maintaining line number tracking.
* **Stack Trace Deduplication**: Merges repeating compiler errors (e.g. 50 identical TypeScript type mismatch errors condensed into a summarized counter with top 3 instances).
* **Terminal ANSI Stripping**: Cleans escape sequences, cursor control codes, and spinner characters.
* **Token Savings**: **Reduces token consumption by 20% to 40% per prompt**, saving API costs and preventing context window overflows.

### 3.4. Vision & Reasoning Capability Detection Engine
Jasper inspects models across a 3-tier heuristic pipeline to badge them with **`👁️` (Vision)** and **`🧠` (Reasoning)**:

1. **Tier 1: Aggregator Metadata (OpenRouter / Hugging Face API)**:
   * Inspects `architecture.modality`. If `multimodal` or `image->text`, flags `👁️`.
   * Inspects `instruct_type`. If `reasoning` or `cot`, flags `🧠`.
2. **Tier 2: Curated Regex Pattern Matcher**:
   * **Vision Regex**: `/(vision|-vl|multimodal|gpt-4o|gemini-2|gemini-1\.5|claude-3|pixtral|minicpm-v|qwen.*-vl)/i`
   * **Reasoning Regex**: `/(r1\b|\bo1\b|\bo3\b|reasoner|thinking|qwq|marco-o1)/i`
3. **Tier 3: Dynamic Runtime `<think>` Extraction**:
   * If a model streams thoughts encapsulated inside `<think>...</think>` tags (or passes a discrete `reasoning_content` field), Jasper marks the model as `🧠 Reasoning` in local storage for future invocations.

### 3.5. Dedicated Vision Adapter & Multimodal Handoff
When an agent prompt contains images (e.g. Web Preview screenshots, UI mockups, diagrams) and the primary model is text-only (e.g. `deepseek-chat` or `qwen2.5-coder`):
1. **Interception**: Jasper's router identifies an image block in the payload.
2. **Handoff**: The payload is dispatched to the user's configured **Vision Adapter Pool** (e.g. `gemini-2.0-flash`, `gpt-4o`, or `claude-3.5-sonnet`).
3. **Synthesis**: The vision model inspects the visual asset and returns a rich textual and spatial representation.
4. **Resumption**: The main coding model receives this description in place of the raw image data, continuing execution without failing or rejecting the prompt.

### 3.6. Typed Combos & Load Balancing Engine
A Combo is a virtual model identifier that executes complex routing strategies across multiple underlying providers:

* **Combo Types**:
  * **`💬 Chat Combos`**: Optimized for ideation, low latency, and broad conversational knowledge.
  * **`💻 Coding Combos`**: Optimized for strict JSON schema tool calling, AST diffing, and code generation.
  * **`🛡️ Other / General Combos`**: Acts as a safety net fallback pool.
* **Execution Strategies**:
  * **Fallback Chain**: Executes Provider 1 ➔ on HTTP 429 / 503 / Timeout, immediately re-issues payload to Provider 2 ➔ then Provider 3 ➔ ultimately fallback to Local Qwen model.
  * **Round-Robin Multi-Account**: Evenly cycles requests across multiple API keys for the same provider (e.g. 4 Google AI Studio keys), multiplying effective requests-per-minute limits.

### 3.7. External Tool Connectors
Jasper integrates OAuth and session-based connectors inspired by 9Router:
* **Google Antigravity**: Reuses authenticated browser developer sessions to access Google's experimental model endpoints.
* **GitHub Models**: Connects via personal GitHub tokens to route through GitHub's hosted model catalog.

---

## 4. Graphify Cognitive Memory & AST Code Graph Engine

Jasper relies on a persistent knowledge graph representation of the user, workspace codebases, and architectural decisions, eliminating hallucinations and context drift across long sessions.

### 4.1. Tree-sitter AST Parsing & Code Knowledge Extraction
When a project is created, cloned, or edited:
1. **Incremental Tree-sitter Parsing**: Runs AST parsers for TypeScript, JavaScript, Python, Rust, Go, HTML, and CSS.
2. **Entity Node Creation**: Creates nodes for `Files`, `Classes`, `Functions`, `Interfaces`, and `Exported Constants`.
3. **Relational Edge Wiring**:
   * `IMPORTS`: Source file dependencies.
   * `CALLS`: Function invocation trees.
   * `IMPLEMENTS / EXTENDS`: Type inheritance hierarchy.
   * `MUTATES`: State and database schema alterations.

### 4.2. Hybrid Graph-Vector Context Retrieval
When the user submits a prompt:
1. **Intent Extraction**: Identifies key symbols, filenames, and architectural concepts.
2. **Graph Traversal (1–2 Hops)**: Extracts the immediate "blast radius"—the exact files, interfaces, and functions that depend on or are called by the target code.
3. **Context Packing**: Injects only the precise AST subgraphs into the system prompt, keeping token usage under 4,000 tokens while providing complete project awareness.

### 4.3. Dual Memory Graphs (Global Persona vs. Project Isolation)
To keep memory clean and organized, Jasper maintains two strictly decoupled SQLite graph databases:

```
┌─────────────────────────────────────────────────────────────┐
│ 🧠 GLOBAL MEMORY GRAPH (`~/.jasper/global_memory.sqlite`)    │
├─────────────────────────────────────────────────────────────┤
│ • User Preferences: "Prefers TypeScript, Tailwind, dark mode"│
│ • Coding Habits: "Avoids barrel files; uses functional React"│
│ • Tool Configurations & Global API Provider Preferences     │
└─────────────────────────────────────────────────────────────┘
                               ▲
                               │ (Never contaminated by project code)
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ 📁 PROJECT MEMORY GRAPH (`<project>/.jasper/memory.sqlite`)  │
├─────────────────────────────────────────────────────────────┤
│ • Codebase AST Graph: Function relationships, imports       │
│ • Architectural Decisions: "Using IndexedDB for offline"    │
│ • Database Schemas & Active API Contracts                   │
└─────────────────────────────────────────────────────────────┘
```

### 4.4. Memory Pruning on Project Deletion
When a user deletes a project:
* The local project graph (`<project>/.jasper/memory.sqlite`) and its associated files are removed.
* A pruning modal allows the user to decide whether to delete project-specific memories or retain architectural lessons learned.
* **Global memories remain completely untouched**, ensuring user preferences persist forever.

---

## 5. Local On-Device Inference Engine (`llama.cpp` + Qwen2.5-Coder)

For sovereign, offline, or air-gapped coding, Jasper includes an integrated native C++ inference server based on `llama.cpp`.

### 5.1. ARM64 Compilation & Assembly Micro-Kernels
* **NEON Vectorization**: Compiled with `-DGGML_NEON=ON` to utilize ARM64 128-bit SIMD execution units.
* **Arm KleidiAI Micro-Kernels**: Directly incorporated to accelerate matrix-vector multiplications on Cortex-A75 / Cortex-A55 cores by up to 2.5×.
* **Thread Clamping**: Clamped to 2–4 physical efficiency/performance cores (`--threads 4`) to prevent thermal throttling and battery drain.

### 5.2. Memory Mapping (`mmap`) & FlashAttention KV Cache
* **`mmap` Direct Access**: GGUF weights are memory-mapped directly from the filesystem, enabling model startup in under 1.5 seconds.
* **FlashAttention (`--flash-attn`)**: Compacts the key-value context cache by 40%–50%, maintaining up to 4,096 tokens of active context within a ~1.4GB RAM envelope.

### 5.3. Dynamic Low-Memory Killer (LMK) Protection & Idle Unload
To prevent Android from killing Jasper during heavy multitasking:
* **Active RAM Monitoring**: Constantly queries `/proc/meminfo`.
* **5-Minute Idle Unload**: If no inference requests are received within 5 minutes, `llama-server` calls `madvise(MADV_DONTNEED)` to release physical RAM pages back to Android.
* **Emergency Compiling Pause**: If free system RAM drops below 400MB during a build, local inference is paused until the compiler finishes.

### 5.4. Hardware Safety Analyzer & PocketPal Risk Scoring
Before initiating model downloads, Jasper calculates a safety score:

$$\text{Safety Margin} = \text{Available RAM} - (\text{Model Disk Size} \times 1.15 + \text{KV Cache Size})$$

* $\text{Margin} > 800\text{ MB}$: **`🟢 Optimal Fit`** (Safe to download and execute).
* $200\text{ MB} < \text{Margin} \le 800\text{ MB}$: **`🟡 Tight Fit`** (May trigger background tab reloading).
* $\text{Margin} \le 200\text{ MB}$: **`🔴 High Risk`** (Triggers explicit warning modal requiring user confirmation).

---

## 6. Universal Route Discovery Engine (Web Preview)

To populate the **App Pages** drawer across any frontend or backend framework, Jasper uses a hybrid static-dynamic discovery pipeline.

### 6.1. Static AST Route Scraper (Background Thread)
Scans project files using Tree-sitter and pattern scrapers:
* **Next.js (App Router)**: Scans for `app/**/page.{tsx,jsx,js}` ➔ generates `/`, `/dashboard`, `/settings`.
* **Next.js (Pages Router), Nuxt, SvelteKit, Astro**: Scans `pages/` and `routes/` filesystem directories.
* **React Router / TanStack Router**: Parses router declarations (e.g. `createBrowserRouter([{ path: '...' }])`) using AST queries.
* **Static HTML**: Scans root and `public/` directories for `*.html` files.
* **FastAPI / Flask / Express**: Scans router decorator ASTs (`@app.get('/api/view')`, `router.get(...)`).

### 6.2. Dynamic Iframe Loopback Synchronization (Runtime)
* Since the preview iframe runs on `http://localhost:<port>`, Jasper attaches a lightweight listener to `window.history.pushState`, `replaceState`, and `hashchange`.
* Whenever a user clicks an internal link inside the running app, the top address bar pill (`[ Home ▾ ]`) updates in real time.
* Any newly accessed dynamic routes are appended to the App Pages drawer catalog immediately.

---

## 7. Mobile PRoot Terminal & Multi-Session PTY Multiplexer

Jasper provides a native Linux development environment on Android without requiring root access:

### 7.1. Rootless Linux via PRoot
* **Syscall Interception**: Uses `ptrace` and seccomp to intercept Linux system calls, spoofing paths and user identities (simulating `root` within the container).
* **Isolated Rootfs**: Standard Ubuntu ARM64 root filesystem deployed in app private storage (`/data/data/com.jasper.app/files/rootfs`).
* **Package Management**: Native `apt` package manager allowing installation of Node.js, Python, Git, Rust, Go, and build essentials.

### 7.2. Multi-Session PTY Daemon
* **Multiplexing Engine**: Manages up to **5 concurrent pseudoterminal (PTY) streams** via `node-pty`.
* **State Persistence**: Terminal processes (such as `npm run dev` or long-running Python scripts) continue executing in the background when the user closes the terminal drawer or switches to the code editor.
* **Websocket Bridge**: Communicates with the xterm.js frontend over a low-latency Unix domain socket / localhost WebSocket with raw terminal window resizing (`SIGWINCH`) synchronization.

---

## 8. Autonomous Dev Server Lifecycle & PTY Port Sniffer

To eliminate manual terminal interaction for non-technical users while providing complete flexibility for developers, Jasper implements an automated dev server daemon and stream sniffer.

### 8.1. Autonomous Startup Pipeline
1. **Framework Fingerprinting**:
   * Inspects `package.json` for scripts (`dev`, `start`, `serve`) or framework signatures (Vite, Next.js, Nuxt, Astro, SvelteKit, Remix).
   * For Python projects, scans for `manage.py`, `app.py`, `uvicorn`, `fastapi`, or `flask`.
2. **Dedicated Background PTY Session**:
   * Launches the server in a designated background PTY channel (`Session 0: Dev Server Daemon`).
   * Passes `--host 0.0.0.0` or `--host localhost` to ensure proper socket binding within PRoot.
3. **Health Check Probing**:
   * Jasper's internal client performs periodic HTTP `HEAD /` requests to verify that the server is ready before signaling the UI.

### 8.2. Stream Port Sniffer Engine
Whenever *any* terminal session outputs text (whether started autonomously or typed manually by a developer), the sniffer regex processes chunks in real time:

```ts
const PORT_BIND_REGEX = /(?:https?:\/\/)?(?:localhost|127\.0\.0\.1|0\.0\.0\.0):(?<port>\d{3,5})/i;

function onPtyData(chunk: string) {
  const match = chunk.match(PORT_BIND_REGEX);
  if (match?.groups?.port) {
    const detectedPort = parseInt(match.groups.port, 10);
    // Ignore internal ports like llama.cpp (8080)
    if (detectedPort !== 8080) {
      previewManager.bindPort(detectedPort);
      eventBus.emit('dev-server-ready', { url: `http://localhost:${detectedPort}` });
    }
  }
}
```

* **Instant Preview Synchronization**: The Web Preview iframe immediately binds to `http://localhost:<detectedPort>` without requiring the user to type or paste a URL.
* **External Link Provider**: Publishes the URL to the preview header `[ ↗ Open ]` action and ambient chat link.

---

## 9. Real-Time Error Interception & Self-Healing Pipeline

Jasper monitors runtime execution across three surfaces to intercept and repair errors before they compound.

### 9.1. Error Interception Surfaces
1. **Terminal Stderr & Process Exits**: Captures compilation crashes from `tsc`, `esbuild`, `webpack`, `vite`, and Python tracebacks.
2. **Vite / Next.js HMR Error WebSocket**: Intercepts Vite HMR overlay messages (`vite:ws` `error` payload) over the local loopback WebSocket.
3. **Iframe `window.onerror` Bridge**: Injects a lightweight snippet into the preview iframe to capture client-side unhandled promise rejections and React render errors.

### 9.2. UI Notification Dispatch
* Intercepted errors are formatted into a normalized structure: `{ file, line, column, code, message }`.
* Dispatches simultaneous notifications to:
  * **Preview Floating Toast**: Slides in over the preview canvas with `[ Fix ]` action.
  * **Pre-Chat-Input Sticky Banner**: Persistently docks directly above the chat input container:
    `[ 🚨 Build Error in Preview: <brief error>  [ 🩹 Fix Build Error ]  [✕] ]`.

### 9.3. Two-Phase Turn Self-Healing Algorithm
When the user submits a new prompt while an error is active (or taps `[ Fix ]`):

```
┌─────────────────────────────────────────────────────────────┐
│                 USER SUBMITS NEW PROMPT                     │
│                (or taps [ Fix Build Error ])                │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
               Active Unresolved Build Error?
                               │
            ┌──────────────────┴──────────────────┐
            │ YES                                 │ NO
            ▼                                     ▼
┌──────────────────────────────────────┐ ┌────────────────────┐
│ PHASE 1: SELF-HEALING TURN           │ │ STANDARD TURN      │
│ • Loads AST context of failing file  │ │ • Executes prompt  │
│ • Applies surgical patch             │ └────────────────────┘
│ • Re-compiles to verify fix          │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│ PHASE 2: FEATURE EXECUTION TURN      │
│ • Executes original user request     │
│ • Builds on clean, verified codebase │
└──────────────────────────────────────┘
```

---

## 10. Dual WakeLock & Android Persistent Foreground Architecture

Mobile operating systems enforce aggressive CPU throttling and process termination for background apps. Jasper solves this through dual WakeLock coordination.

### 10.1. Android Native WakeLock Engine
Implemented via a Capacitor Android native bridge:

```java
public class WakeLockPlugin extends Plugin {
    private PowerManager.WakeLock agentWakeLock;
    private PowerManager.WakeLock terminalWakeLock;

    public void acquireAgentWakeLock(PluginCall call) {
        PowerManager pm = (PowerManager) getContext().getSystemService(Context.POWER_SERVICE);
        agentWakeLock = pm.newWakeLock(PowerManager.PARTIAL_WAKE_LOCK, "Jasper::AgentWakeLock");
        agentWakeLock.acquire();
        startForegroundService("Jasper Agent Running", "Autonomous sub-agent executing tasks...");
    }

    public void acquireTerminalWakeLock(PluginCall call) {
        PowerManager pm = (PowerManager) getContext().getSystemService(Context.POWER_SERVICE);
        terminalWakeLock = pm.newWakeLock(PowerManager.PARTIAL_WAKE_LOCK, "Jasper::TerminalWakeLock");
        terminalWakeLock.acquire();
        startForegroundService("Jasper Terminal Active", "Background dev server & processes running...");
    }
}
```

### 10.2. Lifecycle Management Rules
1. **Agent WakeLock**:
   * **Acquired**: When the user sends a prompt in Build mode or when a background task begins.
   * **Foreground Notification**: Shows live progress (e.g. `Step 2/4: Running Vitest`), and a `[ Pause Agent ]` action.
   * **Cross-Project Roaming**: Ensures tasks run uninterrupted even if the user navigates to other projects or switches to another Android app.
   * **Released**: When the task finishes (or pauses); fires a local completion notification with vibration: `✅ Task Finished: ...`.
2. **Terminal WakeLock**:
   * **Acquired**: Automatically when the first terminal session tab is opened.
   * **Maintained**: Remains held as long as at least one terminal tab is open (even if minimized).
   * **Released**: Only when all terminal tabs are closed (via `exit` command or `[✕]` tab button) and the agent is idle.
   * **Result**: Zero unexpected dev server crashes when the user switches apps or locks their screen.

### 10.3. Global Concurrency Lock & Cross-Project State Coordination
To protect limited mobile RAM (e.g. 6GB devices) against concurrent compiler processes and Android Low Memory Killer (LMK) eviction, Jasper enforces a global singleton execution coordinator:

```ts
interface ActiveTaskState {
  projectId: string;
  projectName: string;
  taskId: string;
  step: string;
  timestamp: number;
}

class ConcurrencyCoordinator {
  private activeTask: ActiveTaskState | null = null;

  public requestBuildLock(projectId: string, projectName: string, taskId: string): boolean {
    if (this.activeTask && this.activeTask.projectId !== projectId) {
      return false; // Concurrency lock active in another project
    }
    this.activeTask = { projectId, projectName, taskId, step: 'Initializing', timestamp: Date.now() };
    eventBus.emit('build-lock-acquired', this.activeTask);
    nativeBridge.acquireAgentWakeLock();
    return true;
  }

  public releaseBuildLock(projectId: string) {
    if (this.activeTask?.projectId === projectId) {
      this.activeTask = null;
      eventBus.emit('build-lock-released');
      nativeBridge.releaseAgentWakeLock();
    }
  }

  public getActiveTask(): ActiveTaskState | null {
    return this.activeTask;
  }
}
```

* **Discuss Mode Bypass**: Discuss mode requests do not spawn compiler tools, execute bash commands, or alter files—allowing users to freely converse, plan, and ask questions anywhere while an agent builds in the background.
* **Reactive UI Synchronization**: The `build-lock-acquired` and `build-lock-released` events automatically update all chat inputs, switching secondary project inputs into the `[ 🔒 Agent Busy in "<Project>" ]` state with zero polling.

---

## 11. Red Team Swarm Architecture & Automated Self-Hardening (Ported from Strix)

Jasper integrates the core architectural principles of Strix (`usestrix/strix`), translating multi-agent adversarial penetration testing into a native, automated defensive code-hardening pipeline.

### 11.1. Dual-Swarm Sequential Pipeline
Every build task executes as a two-phase swarm:

```
┌─────────────────────────────────────────────────────────────┐
│                 AUTONOMOUS DUAL-SWARM FLOW                  │
├─────────────────────────────────────────────────────────────┤
│ 🔵 PHASE 1: BLUE TEAM (CONSTRUCTION)                        │
│ • Architect Agent ➔ Coder Agent(s) ➔ Runtime Agent          │
│ • Validates TypeScript compilation & local dev server run   │
│                                                             │
│                          ▼                                  │
│                 [ Build Succeeded ]                         │
│                          ▼                                  │
│                                                             │
│ 🔴 PHASE 2: RED TEAM (ADVERSARIAL AUDITING - STRIX)         │
│ • Spawns 10 specialized Red Team sub-agents in parallel     │
│ • Agents 1–9 evaluate static AST, routes, configs, and deps │
│ • Agent 10 performs dynamic loopback validation in PRoot    │
│ • If vulnerability confirmed: Agent 10 synthesizes patch    │
│ • Re-compiles to verify clean build                         │
│                                                             │
│                          ▼                                  │
│ 🏁 TASK COMPLETE: Verified, Hardened & Committed            │
└─────────────────────────────────────────────────────────────┘
```

### 11.2. The 10-Agent Red Swarm Specialization Matrix

| Agent ID | Specialization Role | Inspection Domain & Heuristics |
| :--- | :--- | :--- |
| **Agent 1** | **Lead Orchestrator & Surface Grapher** | Ingests AST, parses route trees (Express, Next.js, FastAPI), and generates a directed graph of all external inputs and database boundaries. |
| **Agent 2** | **Route & API Enumerator** | Scans for untyped route parameters, debug endpoints (`/debug`, `/admin`, `/test`), and unprotected REST/GraphQL methods. |
| **Agent 3** | **Secret & Credential Auditor** | Scans commit staging, `.env` files, and client-side bundles using high-entropy regex to detect leaked API keys (AWS, OpenAI, Stripe). |
| **Agent 4** | **Config & Headers Auditor** | Checks CORS origins (`Access-Control-Allow-Origin: *`), Content Security Policy (CSP), Cookie security flags (`HttpOnly; Secure; SameSite=Lax`). |
| **Agent 5** | **Injection Specialist** | Detects raw SQL/NoSQL query concatenation, unsafe template literals, and unsanitized inputs passed to `child_process.exec()` / `os.system()`. |
| **Agent 6** | **Broken Access Control & IDOR** | Tests horizontal and vertical authorization: verifies whether routes accessing `/api/resource/:id` validate session ownership before returning records. |
| **Agent 7** | **Auth & Session Hardener** | Audits brute-force protections: checks for missing rate-limiting on login/password-reset endpoints, bcrypt work factors, and token expiration. |
| **Agent 8** | **Client-Side & SSRF Specialist** | Analyzes React code for unsanitized `dangerouslySetInnerHTML`, open client redirects, and server-side request forgery in outbound HTTP fetches. |
| **Agent 9** | **Supply Chain & CVE Auditor** | Compares `package-lock.json` and `pnpm-lock.yaml` dependencies against live vulnerability advisories (OSV.dev / GitHub Advisory Database). |
| **Agent 10** | **Dynamic Validator & Patch Synthesizer** | Fires simulated local loopback requests in PRoot to verify whether flagged issues are genuinely exploitable (zero false positives), then outputs the defensive patch. |

### 11.3. PRoot Sandbox Behavioral Validation (Zero False Positives)
To eliminate the flood of false positives produced by conventional static analyzers, Agent 10 uses Strix's **dynamic behavioral validation**:
* Runs exclusively against the isolated internal loopback interface (`http://localhost:<detectedPort>`) inside the user's PRoot container.
* Sends targeted boundary payloads (e.g. malformed JSON payloads, IDOR parameter substitutions, boundary probe values).
* Evaluates the server's response:
  * **False Positive**: Endpoint cleanly handles validation, returns `400 Bad Request` or `401 Unauthorized` without leaking internal stack traces. Issue is dismissed.
  * **Confirmed Vulnerability**: Endpoint returns `500 Internal Server Error` exposing database schemas, or returns unauthorized records (`200 OK`). Issue is escalated for immediate patching.

### 11.4. Automated Defensive Patch Synthesis & AST Rewriting
When an issue is confirmed, Agent 10 synthesizes a targeted, defensive AST patch without disrupting the user's business logic:

```ts
interface SecurityPatch {
  vulnerabilityType: 'SQLi' | 'IDOR' | 'RateLimit' | 'SecretLeak' | 'XSS';
  targetFile: string;
  lineRange: [number, number];
  diff: string;
  rationale: string;
}

// Example patch generation: Raw SQL -> Parameterized Query
const patch: SecurityPatch = {
  vulnerabilityType: 'SQLi',
  targetFile: 'src/routes/users.ts',
  lineRange: [24, 25],
  diff: `- const user = await db.query(\`SELECT * FROM users WHERE id = '\${req.params.id}'\`);
+ const user = await db.query('SELECT * FROM users WHERE id = $1', [req.params.id]);`,
  rationale: 'Converted string concatenation query into parameterized statement to prevent SQL injection.'
};
```

* **Immediate Application**: Jasper applies the unified diff directly to the project filesystem.
* **Compilation Gate**: Re-runs `tsc --noEmit` and tests to verify that the patch introduced zero syntax or runtime regressions.

### 11.5. Pre-Push Security Interception Hook
For manual developer coding sessions in the editor or terminal, Jasper injects a lightweight pre-push git hook:
* **Trigger**: Intercepts `git push` commands.
* **Checks**: Scans git staging diffs for high-entropy tokens and private keys (`sk-`, `ghp_`, `AKIA`, private PEM keys).
* **Behavior**:
  * If a secret is detected, pauses the push and renders the non-blocking UI alert:
    `[ ⚠️ Security Checkpoint: Secret detected in src/config.ts ] [ Push Anyway ] [ Move to .env (Fix) ]`.
  * Tapping `[ Move to .env (Fix) ]` extracts the secret to `.env`, adds `.env` to `.gitignore`, and substitutes `process.env.SECRET_NAME` in the source file automatically.

---

## 12. Code Philosophy Engine & Decision Ladder (Ported from Ponytail)

To prevent the common failure mode of AI-generated code bloat, premature abstraction, and redundant package churn on resource-constrained mobile hardware, Jasper implements the **Decision Ladder** engine derived from the Ponytail framework (`DietrichGebert/ponytail`).

### 12.1. The 5-Rung Decision Ladder Algorithmic Contract
The Blue Team's Architect and Coder agents operate under a system prompt directive that forces sequential reasoning through five distinct hurdles before generating any code:

```
┌─────────────────────────────────────────────────────────────┐
│                 THE 5-RUNG DECISION LADDER                  │
├─────────────────────────────────────────────────────────────┤
│ Rung 1: 🛑 Necessity Check                                   │
│         Does the prompt solve a genuine problem? Can an     │
│         existing flag, prop, or parameter achieve this?     │
│                               ▼                             │
│ Rung 2: 🔍 Codebase Reuse Check (via Graphify)              │
│         Does a utility, helper, hook, or schema already     │
│         exist in the AST index? (Mandatory import)          │
│                               ▼                             │
│ Rung 3: 🌐 Platform & Standard Library Check                │
│         Can modern Web APIs (`fetch`, `crypto`, `Intl`,     │
│         `structuredClone`) solve this without third-party   │
│         dependencies?                                       │
│                               ▼                             │
│ Rung 4: 📦 Dependency Scrutiny                              │
│         Can an already-installed package in `package.json`   │
│         handle it? (Hard block on `npm install` for trivial │
│         utilities).                                         │
│                               ▼                             │
│ Rung 5: ✍️ Minimal Viable Implementation                    │
│         Write the leanest possible code: inline over        │
│         indirection, co-location over micro-files, and      │
│         zero premature abstraction factories.               │
└─────────────────────────────────────────────────────────────┘
```

### 12.2. Graphify Knowledge Graph Deduplication Hook
Before a Coder Agent writes a helper function (e.g. date formatting, debouncing, class merging), it executes an AST graph lookup against the project index:

```ts
interface CodebaseDeduplicationCheck {
  intent: string;
  candidateSymbols: string[];
}

// Blue Team Architect runs deduplication query:
const check = await projectGraph.searchSymbols({
  query: 'debounce | throttle | formatCurrency | useAuth',
  kinds: ['function', 'hook', 'class']
});

if (check.matches.length > 0) {
  // Decision Ladder Rung 2: Force reuse
  coderAgent.injectContext({
    directive: `REUSE_EXISTING_SYMBOL: Import \`${check.matches[0].name}\` from \`${check.matches[0].filePath}\`. Do NOT generate a duplicate helper.`
  });
}
```

### 12.3. Platform Standard API Substitution Heuristics
Jasper maintains an internal substitution dictionary injected into the agent runtime to replace common bloated npm packages with modern native equivalents:

| Redundant npm Package | Native Modern JavaScript / Web Standard Replacement |
| :--- | :--- |
| `uuid` | `crypto.randomUUID()` |
| `lodash/cloneDeep` | `structuredClone(obj)` |
| `axios` | Native `fetch()` with `AbortController` |
| `dayjs` / `moment` | Native `Intl.DateTimeFormat` and `Date` APIs |
| `classnames` / `clsx` | Template literals or array join: `[cond && 'cls'].filter(Boolean).join(' ')` |
| `query-string` | Native `URLSearchParams` |

### 12.4. Intensity Profile State Machine (`Lite`, `Full`, `Ultra`)
Managed via `[⚙️ Project Settings] ➔ Code Philosophy`:

```ts
export type CodePhilosophyMode = 'lite' | 'full' | 'ultra';

export interface CodePhilosophyPolicy {
  blockRedundantNpmPackages: boolean;
  enforceGraphifyReuse: boolean;
  disallowNewDependenciesWithoutPrompt: boolean;
  enforceSingleFileCoLocation: boolean;
}

export const CODE_PHILOSOPHY_POLICIES: Record<CodePhilosophyMode, CodePhilosophyPolicy> = {
  lite: {
    blockRedundantNpmPackages: false,
    enforceGraphifyReuse: true,
    disallowNewDependenciesWithoutPrompt: false,
    enforceSingleFileCoLocation: false,
  },
  full: { // DEFAULT
    blockRedundantNpmPackages: true,
    enforceGraphifyReuse: true,
    disallowNewDependenciesWithoutPrompt: false,
    enforceSingleFileCoLocation: false,
  },
  ultra: {
    blockRedundantNpmPackages: true,
    enforceGraphifyReuse: true,
    disallowNewDependenciesWithoutPrompt: true, // Blocks npm i until confirmed
    enforceSingleFileCoLocation: true,          // Maximize co-location
  }
};
```

---

*Document compiled and verified for Jasper System Logic & Technical Implementation.*

