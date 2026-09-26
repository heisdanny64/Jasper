# 🎨 Jasper: Complete Mobile UI/UX Design Specification

> **Target Platform:** Android (Capacitor Container + React 19 + TypeScript + Tailwind CSS v4)  
> **Component System:** Shadcn UI Primitives  
> **Iconography:** Hugeicons (`hugeicons-react`)  
> **Design Philosophy:** Monochrome Elegance, Touch-First Ergonomics, Zero-Friction Navigation  
> **Date:** September 2026

---

## 📑 Table of Contents

1. [Design System & Theming](#1-design-system--theming)
2. [Global Navigation & Screen Architecture](#2-global-navigation--screen-architecture)
3. [Global Home: Chat-First & The Dual-Section Drawer](#3-global-home-chat-first--the-dual-section-drawer)
4. [Projects Hub (Workspaces & Expanding FAB)](#4-projects-hub-workspaces--expanding-fab)
5. [In-Project Experience & Dual Bottom Navigation](#5-in-project-experience--dual-bottom-navigation)
6. [Code Editor & Multi-Session Terminal Drawer](#6-code-editor--multi-session-terminal-drawer)
7. [Web Preview UI & Universal App Pages Engine](#7-web-preview-ui--universal-app-pages-engine)
8. [Reusable Chat Input & Discuss/Build Mode Drawer](#8-reusable-chat-input--discussbuild-mode-drawer)
9. [Mobile Ergonomics, Virtual Keyboard Bar & Zoom Lock](#9-mobile-ergonomics-virtual-keyboard-bar--zoom-lock)
10. [Memory Vault & Project Deletion Pruning Flow](#10-memory-vault--project-deletion-pruning-flow)
11. [Application Settings & Default Launch Screen](#11-application-settings--default-launch-screen)
12. [AI Providers & Local Model Setup (PocketPal Flow)](#12-ai-providers--local-model-setup-pocketpal-flow)
13. [AI Providers & 9Router Management UI](#13-ai-providers--9router-management-ui)
14. [Project Settings: Code Philosophy Configuration](#14-project-settings-code-philosophy-configuration)
15. [Skills & MCP Management UI (Composio & Custom Servers)](#15-skills--mcp-management-ui-composio--custom-servers)

---

## 1. Design System & Theming

### 1.1. Default Monochrome Palette
Jasper uses a pure black-and-white visual foundation for high contrast, minimal battery consumption on OLED displays, and distraction-free focus:

* **Dark Mode (Default on OLED/Dark System):**
  * Background: Pure `#000000` (true pitch black)
  * Surface / Cards: `#0A0A0A` with subtle `#18181B` borders
  * Text / Primary Elements: Pure `#FFFFFF`
  * Secondary Text: `#A1A1AA`
* **Light Mode:**
  * Background: Pure `#FFFFFF`
  * Surface / Cards: `#FAFAFA` with subtle `#E4E4E7` borders
  * Text / Primary Elements: Pure `#000000`
  * Secondary Text: `#71717A`

### 1.2. System Theme Sync & Custom Accent Color
* **Theme Modes:** `System Default` (follows Android OS), `Dark`, or `Light` (configured in Settings).
* **Accent Color Customization:**
  * While backgrounds remain pure monochrome, users can select an accent tint for active tabs, mode badges, focus rings, and action buttons.
  * Presets: `Monochrome` (Default White/Black), `Electric Indigo`, `Emerald Green`, `Amber Flame`, `Rose Crimson`, or `Custom Hex Picker`.

### 1.3. UI Component Library & Iconography
* **Component Primitives:** **Shadcn UI** (Radix/Headless primitives customized with Tailwind CSS v4):
  * Drawer, Sheet, Dialog, DropdownMenu, Tooltip, Badge, Tabs, ScrollArea.
* **Icon Library:** **Hugeicons** (`hugeicons-react`):
  * Crisp, modern geometric strokes with consistent stroke widths optimized for high-DPI Android touchscreens.

---

## 2. Global Navigation & Screen Architecture

```
                               ┌───────────────────────────┐
                               │       APP LAUNCH          │
                               │  (Configurable Default)   │
                               └─────────────┬─────────────┘
                                             │
             ┌───────────────────────────────┼───────────────────────────────┐
             ▼                               ▼                               ▼
   ┌───────────────────┐           ┌───────────────────┐           ┌───────────────────┐
   │    GLOBAL CHAT    │           │   PROJECTS HUB    │           │  GLOBAL TERMINAL  │
   │   (Default Home)  │           │  (Workspaces List)│           │ (Standalone PTY)  │
   └─────────┬─────────┘           └─────────┬─────────┘           └───────────────────┘
             │                               │
             ▼                               ▼
   ┌───────────────────┐           ┌───────────────────┐
   │  HAMBURGER DRAWER │           │ IN-PROJECT SHELL  │
   │  - Navigation     │           │ [ 💬 Chat ]       │
   │  - Chat History   │           │ [ 📁 Files ]      │
   └───────────────────┘           └───────────────────┘
```

---

## 3. Global Home: Chat-First & The Dual-Section Drawer

The default opening view is a clean, conversational Chat UI. There is **no bottom navigation bar** on the home screen.

```
┌─────────────────────────────────────────────────────────────┐
│ [≡ Menu]                   Jasper              [+ New Chat] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   🤖 Jasper:                                                │
│   Hey Danny! Ready to brainstorm a new concept, or did     │
│   you want to jump into PulseFit?                           │
│                                                             │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Discuss ▾ ]  Message Jasper...                  [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### The Hamburger Menu (`≡`) — Two-Section Slide-Out Drawer
Tapping the top-left hamburger icon smoothly slides in a Shadcn drawer divided into two purposeful sections:

```
┌─────────────────────────────────────────────────────────────┐
│ 🚀 JASPER                                                   │
├─────────────────────────────────────────────────────────────┤
│ 🧭 NAVIGATION                                               │
│   📁 Projects (Workspaces & Active Repos)                   │
│   💻 Terminal (Global Linux PRoot Shell)                    │
│   🧩 Skills & MCP Tools                                     │
│   ⚙️ Settings                                               │
├─────────────────────────────────────────────────────────────┤
│ 🕒 RECENT CONVERSATIONS                                     │
│   • Brainstorming PulseFit backend architecture             │
│   • Debugging Tailwind CSS configuration in Vite            │
│   • History of the US Constitution                          │
│   • Composio GitHub OAuth token setup                       │
│   • Python web scraper with BeautifulSoup                   │
│   • Android PRoot syscall analysis                          │
└─────────────────────────────────────────────────────────────┘
```

* **Section 1 (System Navigation):** Fast routing to Projects, Global Terminal, Skills/MCP, and Settings.
* **Section 2 (Chat History):** Chronological log of past conversations. Tapping any conversation immediately restores that chat session and its contextual memory.

---

## 4. Projects Hub (Workspaces & Expanding FAB)

Accessed via the hamburger menu or configured as the default launch screen:

```
┌─────────────────────────────────────────────────────────────┐
│ [← Back]                   Projects               [🔍 Search]│
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 📁 PulseFit                                         [⋮] │ │
│ │ ~/workspace/pulsefit                                    │ │
│ │ [ React ] [ TypeScript ] [ Tailwind ] [ IndexedDB ]     │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 📁 PulseFit-API                                     [⋮] │ │
│ │ ~/workspace/pulsefit-api                                │ │
│ │ [ Python ] [ FastAPI ] [ SQLite ]                       │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│                                     [ ➕ Create / Action ]  │
└─────────────────────────────────────────────────────────────┘
```

### 4.1. Project Cards
* **Card Details:** Project Name, Storage Path on device, and Tech Stack badge tags.
* **Direct Tap:** Opens the project into the Project Workspace.
* **Three-Dot Menu (`⋮`):**
  * `Rename Project`: Inline rename of directory and metadata.
  * `Delete Project`: Triggers the smart memory pruning modal.

### 4.2. Expanding Speed-Dial Floating Action Button (FAB)
Tapping the bottom-right `➕` button fans out a floating speed-dial stack:
* 🐙 **Import from GitHub**: Clones a repository via Git/Composio into `~/workspace/`.
* 💬 **Ask Jasper**: Conversational scaffolding (Jasper brainstorms requirements, creates the directory, and configures the stack).
* 📁 **Upload from Device**: Imports a `.zip` archive or existing Android folder.
* ➕ **Create New**: Scaffolds from standard templates (React, Vite, Next.js, FastAPI, Node, Rust, Vanilla).

---

## 5. In-Project Experience & Dual Bottom Navigation

Entering a project loads the Project Workspace. The bottom navigation bar is minimal with exactly **two tabs**:

```
┌─────────────────────────────────────────────────────────────┐
│ [← Projects]    PulseFit (main)    [ ▶ Preview ] [⚙️ Settings]│
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   🤖 Jasper (Project Context):                              │
│   I've reviewed our IndexedDB workout schemas. Ready to    │
│   implement the offline sync queue?                         │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Build ▾ ]  Ask Jasper about PulseFit...         [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│             [ 💬 Chat ]             [ 📁 Files ]            │
└─────────────────────────────────────────────────────────────┘
```

### 5.1. Navigation Tabs
* **`[ 💬 Chat ]`**: The active project AI conversation, inline code diffs, Ask Cards, and swarm activity pills.
* **`[ 📁 Files ]`**: The file explorer and full-featured code editor.

### 5.2. Project-Specific Settings (`⚙️` at Top-Right)
Opens a project-scoped modal:
* **Project Knowledge & Memory**: View and edit the specific architectural notes, schemas, and decisions Jasper holds for this project.
* **Environment Variables**: In-app `.env` key-value editor.
* **Git Remote & Branch Manager**: Branch switching, commits, and remotes.

### 5.3. Conversational Play/Preview Access (`[ ▶ Preview ]`)
Positioned directly in the chat header so non-technical users and "vibe coders" can instantly launch and test the running app without having to navigate into code files.

---

## 6. Code Editor & Multi-Session Terminal Drawer

Tapping the **`[ 📁 Files ]`** bottom tab opens the file manager and code editing canvas:

```
┌─────────────────────────────────────────────────────────────┐
│ [📁 Files]  src/App.tsx                     [💻 Terminal] [▶]│
├─────────────────────────────────────────────────────────────┤
│ 1  import React, { useState } from 'react';                 │
│ 2  import { useWorkouts } from './hooks/useWorkouts';       │
│ 3                                                           │
│ 4  export function App() {                                  │
│ 5    const { workouts } = useWorkouts();                    │
│ 6    return (                                               │
│ 7      <main className="p-4 bg-black text-white">           │
│ 8        <WorkoutList items={workouts} />                   │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ Tab | Esc | { | } | ( | ) | [ | ] | ; | " | ' | / | Ctrl|Fn │
├─────────────────────────────────────────────────────────────┤
│             [ 💬 Chat ]             [ 📁 Files ]            │
└─────────────────────────────────────────────────────────────┘
```

### 6.1. Top Action Bar
* **`[ 📁 Files ]` Drawer Button (Top-Left):** Slides out the project directory tree with file creation, deletion, and folder nesting.
* **`[ 💻 Terminal ]` Drawer Button (Top-Right):**
  * Opens a draggable bottom sheet containing `xterm.js` connected to PRoot.
  * Drag handle allows three snap points: **Peek** (bottom 30%), **Half-Screen** (50%), and **Full Screen** (100%).
  * **Multi-Session Tabs:** Supports up to **5 concurrent terminal sessions** (`[ 1: bash ✕ ] [ 2: vite dev ✕ ] [ + ]`).
* **`[ ▶ Play ]` Preview Button (Top-Right):**
  * Launches the dedicated in-app project Web Preview interface directly from the editor.

### 6.2. macOS-Styled Terminal Chrome & Prompt Layout
The terminal drawer adopts an aesthetic, professional macOS window styling:

```
┌─────────────────────────────────────────────────────────────┐
│ 🔴 🟡 🟢  [ 1: bash ✕ ] [ 2: vite dev ✕ ] [ + ]      ⚡ WAKE │
├─────────────────────────────────────────────────────────────┤
│ my-portfolio~$ npm run dev                                  │
│                                                             │
│   VITE v6.0.1  ready in 240 ms                              │
│                                                             │
│   ➜  Local:   http://localhost:3000/                        │
│   ➜  Network: use --host to expose                          │
│                                                             │
│ my-portfolio~$ █                                            │
└─────────────────────────────────────────────────────────────┘
```

* **Window Controls (Traffic Lights)**:
  * `🔴` (Red): Closes active session tab (or exits terminal if only 1 tab open).
  * `🟡` (Yellow): Minimizes / collapses the terminal drawer.
  * `🟢` (Green): Maximizes terminal to full screen.
* **Prompt Format**: Clean and structured: `<project_name>~$ ` (e.g. `my-portfolio~$ npm run dev`).
* **Session Tab Actions**: Each tab features a clear `[✕]` icon. Sessions also terminate upon typing `exit`.
* **Terminal WakeLock Indicator (`⚡ WAKE`)**: An ambient pill in the header indicating that the Android Terminal WakeLock is actively protecting background servers and CLI processes from sleeping.

---

## 7. Web Preview UI & Universal App Pages Engine

Jasper provides a dedicated, touch-first mobile Web Preview inspired by modern browser testbeds (Base44 style), purpose-built for validating multi-page applications on physical Android devices.

### 7.1. Preview Canvas Anatomy

```
┌─────────────────────────────────────────────────────────────┐
│ [ 🔄 Reload ]   [ Home ▾ ]      [ ↗ Open ]  [ ⛶ Fullscreen ]│
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                                                             │
│                                                             │
│                        LIVE APP                             │
│                  (Iframe / Localhost)                       │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ ⚠️ Build Error: TS2339 in Card.tsx       [ Fix ]  [✕] │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

* **Left Action (`[ 🔄 Reload ]`)**: Hard reload of the preview iframe.
* **Center Address Bar Pill (`[ Home ▾ ]`)**: Displays the active page title or route. Tapping it opens the **App Pages** drawer.
* **External Browser Action (`[ ↗ Open ]`)**: Directly launches the active localhost URL (`http://localhost:3000`) in the user's external Android browser (Chrome, Brave, etc.).
* **Right Action (`[ ⛶ Fullscreen ]`)**: Expands the preview into immersive Fullscreen mode.
* **Autonomous Server Auto-Detection**: When a dev server starts inside PRoot, the preview automatically detects the bound port and refreshes to that URL without requiring the user to type or paste addresses.

### 7.2. "App Pages" Bottom Drawer
Tapping the center address bar pill slides up a Shadcn bottom sheet:

```
┌─────────────────────────────────────────────────────────────┐
│ App pages                                               [✕] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Home                                                       │
│                                                             │
│  Auth                                                       │
│                                                             │
│  Auth/verified                                              │
│                                                             │
│  Auth/verify-expired                                        │
│                                                             │
│  Terms                                                      │
│                                                             │
│  Privacy                                                    │
│                                                             │
│  Avatar                                                     │
│                                                             │
│  Avatar/customize                                           │
│                                                             │
│  Me                                                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

* **Instant Route Jumping**: Tapping any listed page immediately instructs the preview iframe to navigate to that route and smoothly closes the drawer. Eliminates tedious manual clicking through multi-step app flows on mobile.

### 7.3. Universal Route Discovery Across Any Tech Stack
To make the "App Pages" drawer work automatically regardless of what language or framework the user or Jasper chooses, Jasper uses a two-layer discovery engine:

1. **Layer 1: Static AST & File Route Scraper (Background)**:
   * **Next.js (App Router)**: Scans `app/**/page.{tsx,jsx,js}` to extract routes (`/`, `/auth`, `/dashboard`).
   * **Next.js (Pages Router), Nuxt, SvelteKit, Astro**: Scans `pages/` or `routes/` filesystem tree.
   * **React Router / TanStack Router**: Parses router config files (`createBrowserRouter` or `<Route path="...">`) using Tree-sitter AST.
   * **Vite / Vanilla / Static HTML**: Scans all `.html` files in project root and `public/`.
   * **FastAPI / Flask / Express / Go / Rust**: Scans declared GET endpoints serving HTML or views.
2. **Layer 2: Dynamic Iframe Loopback Synchronization (Runtime)**:
   * Because the preview iframe runs on the shared Android local loopback (`http://localhost:<port>`), Jasper listens to the iframe's `history.pushState`, `replaceState`, and `hashchange` events.
   * Whenever navigation occurs inside the running web app, the top address bar pill automatically updates its label (e.g. from `Home` to `Auth/verified`).
   * Any newly discovered dynamic routes are automatically added to the App Pages drawer list in real time.

### 7.4. Fullscreen & Minimize Gesture Navigation
Tapping **`[ ⛶ Fullscreen ]`** transitions into an immersive view:

```
┌─────────────────────────────────────────────────────────────┐
│ [ ← Back to Workspace ]                                 [✕] │ <-- Floating Auto-Hide Bar
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                                                             │
│                                                             │
│                    TRUE FULLSCREEN VIEW                     │
│               (Hides all Jasper tabs & chrome)              │
│                                                             │
│                                                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

* **Total Immersion**: Hides Jasper's headers, tabs, and status bars so the developer can experience the app exactly as an end user would on a phone.
* **Exiting Fullscreen**:
  * **Top Swipe-Down Gesture**: Pulling down from the top edge reveals the floating control bar with a **Minimise icon (`✕`)** and **`[ ← Back to Workspace ]`**.
  * **Android System Back Gesture**: Swiping the screen edge back gesture or tapping the hardware back button cleanly exits fullscreen back to the editor or chat.

### 7.5. Floating Web Preview Error Toast
If a compilation failure, Vite overlay error, or unhandled runtime exception occurs while testing the app in the preview:
* A discreet floating toast card slides into the bottom of the preview canvas:
  `[ ⚠️ Build Error: TS2339 in Card.tsx   [ Fix ]   [✕] ]`
* **Swipe to Dismiss / Auto-Dismiss**: The toast can be swiped away or automatically dismisses after 8 seconds so it never obstructs UI testing.
* **1-Tap Fix**: Tapping **`[ Fix ]`** immediately switches the screen to the Chat tab and dispatches a high-priority diagnostic payload to the agent to heal the error.

---

## 8. Reusable Chat Input & Discuss/Build Mode Drawer

The chat input is implemented as a single, modular component (`ChatInput.tsx`) shared across Global Chat and Project Chat.

### 8.1. Mode Button & Drawer Trigger
Instead of a clumsy horizontal switch, the input embeds an interactive badge button:
`[ Discuss ▾ ]` or `[ Build ▾ ]`.

```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Discuss ▾ ]  Message Jasper...                  [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### 8.2. The Mode Drawer
Tapping the mode badge slides up a Shadcn drawer:

```
┌─────────────────────────────────────────────────────────────┐
│ ⚙️ SELECT EXECUTION MODE                                     │
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (●) 💬 Discuss                                          │ │
│ │     Ideate, brainstorm, plan, and analyze architecture   │ │
│ │     without touching files or running bash commands.      │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (○) ⚡ Build                                            │ │
│ │     Full autonomous agency. Write code, execute         │ │
│ │     commands in PRoot, and manage project files.        │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```
* Selecting a mode immediately updates the badge and closes the drawer.
* Default mode on fresh conversations: **Discuss**.

### 8.3. Pre-Input Sticky Build Error Banner
Whenever active build or preview errors exist in the project, an alert banner docks **immediately above the chat input box**:

```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🚨 Build Error in Preview: TS2339 in Card.tsx           │ │
│ │ [ 🩹 Fix Build Error ]                              [✕] │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Discuss ▾ ]  Message Jasper...                  [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Position**: Always floats directly on top of the input container so the user is immediately aware of existing failures before typing.
* **One-Tap Action**: Clicking `[ 🩹 Fix Build Error ]` activates the agent in Build mode to resolve the bug immediately.
* **Auto-Healing on Prompt Submission**: If the user dismisses the banner and types a new prompt (e.g. *"Add user avatars to the card"*), Jasper automatically runs a **Two-Phase Turn** (heals the build error in Phase 1, then creates the avatars in Phase 2).

### 7.6. Dual Play/Preview Button Architecture
* **In Project Chat Header**: `[← Projects]  PulseFit (main)  [ ▶ Preview ]  [⚙️ Settings]`  
  Allows non-technical users to preview their app immediately after a conversational brainstorming or build session.
* **In Code Editor Header**: `[📁 Files]  src/App.tsx  [💻 Terminal]  [ ▶ Preview ]`  
  Allows developers to test changes with zero tab-switching while editing code.

---

## 8. Reusable Chat Input & Discuss/Build Mode Drawer

The chat input is implemented as a single, modular component (`ChatInput.tsx`) shared across Global Chat and Project Chat.

### 8.1. Mode Button & Drawer Trigger
Instead of a clumsy horizontal switch, the input embeds an interactive badge button:
`[ Discuss ▾ ]` or `[ Build ▾ ]`.

```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Discuss ▾ ]  Message Jasper...                  [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### 8.2. The Mode Drawer
Tapping the mode badge slides up a Shadcn drawer:

```
┌─────────────────────────────────────────────────────────────┐
│ ⚙️ SELECT EXECUTION MODE                                     │
├─────────────────────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (●) 💬 Discuss                                          │ │
│ │     Ideate, brainstorm, plan, and analyze architecture   │ │
│ │     without touching files or running bash commands.      │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (○) ⚡ Build                                            │ │
│ │     Full autonomous agency. Write code, execute         │ │
│ │     commands in PRoot, and manage project files.        │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```
* Selecting a mode immediately updates the badge and closes the drawer.
* Default mode on fresh conversations: **Discuss**.

### 8.3. Pre-Input Sticky Build Error Banner
Whenever active build or preview errors exist in the project, an alert banner docks **immediately above the chat input box**:

```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🚨 Build Error in Preview: TS2339 in Card.tsx           │ │
│ │ [ 🩹 Fix Build Error ]                              [✕] │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ Discuss ▾ ]  Message Jasper...                  [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Position**: Always floats directly on top of the input container so the user is immediately aware of existing failures before typing.
* **One-Tap Action**: Clicking `[ 🩹 Fix Build Error ]` activates the agent in Build mode to resolve the bug immediately.
* **Auto-Healing on Prompt Submission**: If the user dismisses the banner and types a new prompt (e.g. *"Add user avatars to the card"*), Jasper automatically runs a **Two-Phase Turn** (heals the build error in Phase 1, then creates the avatars in Phase 2).

### 8.4. Global Concurrency Lock Badge (`[ 🔒 Agent Busy in <Project> ]`)
When an autonomous Build Mode task is running in Project A, and the user navigates to Global Chat or Project B:

```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ 🔒 Agent Busy in "PulseFit" ]  Message Jasper... [ ➔ ] │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Discuss Mode Remains Unlocked**: The user can continue chatting, asking technical questions, or brainstorming anywhere in the app.
* **Transparent Feedback (Zero Silent Greying)**: If the user attempts to switch to Build Mode in another workspace while a task is running, Jasper shows an informative popover:

```
┌─────────────────────────────────────────────────────────────┐
│ 🔒 Agent Currently Active in "PulseFit"                     │
├─────────────────────────────────────────────────────────────┤
│ Jasper is currently running a build task in PulseFit.       │
│ To protect mobile CPU and memory, only one build task can   │
│ run at a time.                                              │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │        Stay Here          │ │      View Active Task     │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```
* **Teleport Action**: Tapping `[ View Active Task ]` instantly navigates the user back to the active project's chat and live agent timeline.

### 8.5. Chat Mission Card Red Team Visuals & Pre-Push Checkpoint

#### A. Interactive Mission Card Red Team Feedback
During autonomous tasks, Blue Team and Red Team operations appear sequentially inside the Chat Mission Card with distinctive visual indicators:

```
┌─────────────────────────────────────────────────────────────┐
│ 🚀 Task: Implement User Profile & Settings API              │
│ Status: Active • Step 4 of 5                                │
├─────────────────────────────────────────────────────────────┤
│ [✓] 🔵 1. Architect: Planned endpoints & database schema    │
│ [✓] 🔵 2. Coder: Scaffolding /api/user/profile.ts           │
│ [✓] 🔵 3. Runtime: TypeScript build passed (0 errors)       │
│ [⏳] 🔴 4. Red Team: 10-Agent Swarm auditing security       │
│     └─ 🛡️ Auto-patched: Added authorization guard to route  │
│ [ ] 5. Git checkpoint commit                                │
└─────────────────────────────────────────────────────────────┘
```

* **Color Cues**:
  * `🔵` indicates Blue Team construction tasks (Planning, Scaffolding, UI, Build).
  * `🔴` indicates Red Team security auditing (Surface Graphing, Injection, IDOR, Secrets).
* **Auto-Patch Indication**: When Agent 10 synthesizes and applies a patch, a nested green shield note appears: `🛡️ Auto-patched: <summary of fix>`.
* **Zero UI Interruption**: No separate security drawers, modal popups, or manual triage checklists during autonomous builds.

#### B. Pre-Push Security Checkpoint Dialog (Manual Sessions)
If a developer manually enters code in the Code Editor or executes a command in the Terminal that attempts to `git push` a hardcoded secret or unhashed credential:

```
┌─────────────────────────────────────────────────────────────┐
│ ⚠️ Security Checkpoint                                      │
├─────────────────────────────────────────────────────────────┤
│ Hardcoded secret detected in `src/config.ts`:               │
│ Potential OpenAI API key on line 14.                        │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │        Push Anyway        │ │    Move to .env (Fix)     │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Non-Blocking Choice**: Offers a 1-tap automated resolution (`Move to .env (Fix)`) or lets the user bypass if it is an intended mock string (`Push Anyway`).

---

## 9. Mobile Ergonomics, Virtual Keyboard Bar & Zoom Lock

### 8.1. Virtual Accessory Keyboard Bar
Stationed directly above the Android soft keyboard whenever the Code Editor or Terminal is focused:
```
[ Tab ] [ Esc ] [ { ] [ } ] [ ( ] [ ) ] [ [ ] [ ] ] [ ; ] [ | ] [ / ] [ \ ] [ " ] [ ' ] [ Ctrl ] [ Alt ]
```
* **One-Tap Code Symbols**: Eliminates Gboard symbol page-switching.
* **Auto-Pairing**: Tapping `{` inserts `{}` and centers cursor.
* **Modifier Key Combos**: Tapping `Ctrl` + `C` on Gboard sends `SIGINT` to the terminal.
* **Haptic Feedback**: 15ms haptic pulse on key tap.

### 8.2. Viewport Zoom-Lock Architecture
* Standard viewport meta tag locks all UI chrome:
  `<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">`
* Headers, drawers, tabs, and accessory bars **never pinch or drift**.
* Only the CodeMirror text editor canvas and the Preview iframe allow pinch gestures for font resizing.

---

## 10. Memory Vault & Project Deletion Pruning Flow

### 9.1. Mobile Memory Vault (Settings ➔ Memory Vault)
Presents the cognitive memory graph as plain-English, interactive cards (zero raw graph clutter):
* **Categories**: `🏷️ Preferences & Habits`, `📁 Projects`, `👤 About You`.
* **Actions per Card**: Inline edit (`✏️`), single-tap delete (`🗑️`), search bar (`🔍`), and filter chips.
* **In-Chat Memory Commands**: Supported natively (*"Forget what I said about SQLite"*).

### 9.2. Project Deletion Modal
Deleting a project workspace displays an explicit memory pruning dialog:

```
┌─────────────────────────────────────────────────────────────┐
│ 🗑️ Delete "PulseFit"?                                       │
├─────────────────────────────────────────────────────────────┤
│ This will permanently delete the project workspace and files │
│ from your device storage: ~/workspace/pulsefit/              │
│                                                             │
│ 🧠 Associated Project Memories                              │
│ Jasper has 14 memories linked to this project (schemas,     │
│ architectural decisions, design choices).                   │
│                                                             │
│ [✓] Also delete all memories linked to PulseFit             │
│     (Uncheck if you want Jasper to remember the lessons     │
│      and architecture from this project for future work)    │
│                                                             │
│ ℹ️ Global preferences (coding style, tools) will NOT be     │
│    affected.                                                │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │          Cancel           │ │       Delete Project      │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 11. Application Settings & Default Launch Screen

Located in **Hamburger Menu ➔ ⚙️ Settings**:

### 11.1. Default Launch Screen Selection
Users can customize which screen opens on app start:
* `(●) Global Chat`: Conversation-first, brainstorming, recent chat history.
* `(○) Projects Hub`: Workspaces list and card overview.
* `(○) Terminal`: Instant fullscreen Linux PRoot terminal session.

### 11.2. Time & Date Configuration
* `(●) Automatic`: Synchronizes with host Android system clock and timezone.
* `(○) Manual Override`: Custom date, time, timezone offset, and clock drift fine-tuning.

### 11.3. Theme & Accent Settings
* **Theme**: `System Default` | `Dark` | `Light`.
* **Accent**: `Monochrome` | `Electric Indigo` | `Emerald Green` | `Amber Flame` | `Rose Crimson` | `Custom Hex`.

---

## 12. AI Providers & Local Model Setup (PocketPal Flow)

Inspired by the PocketPal mobile onboarding experience, Jasper provides an intuitive, risk-free interface for configuring AI providers and downloading on-device models with hardware protection.

### 12.1. Provider Selection with Expandable Local Accordion
When selecting providers during initial setup or in **Settings ➔ AI Engine**:

```
┌─────────────────────────────────────────────────────────────┐
│ 🤖 SELECT AI PROVIDER                                       │
├─────────────────────────────────────────────────────────────┤
│ [ ] Anthropic (Claude 3.5 Sonnet, Claude 3.7)               │
│ [ ] OpenAI (GPT-4o, GPT-4o-mini)                            │
│ [ ] Google Gemini (Gemini 2.0 Flash, Pro)                   │
│ [ ] OpenRouter / DeepSeek                                   │
│ [▼] 📱 Local On-Device Model (100% Sovereign & Offline)    │
├─────────────────────────────────────────────────────────────┤
│  RECOMMENDED FOR YOUR DEVICE (POCO C85 • 6GB RAM • 32GB Free)│
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ ⚡ Qwen2.5-Coder-1.5B-Instruct            [ ⬇ Download ]│  │
│  │ Q4_K_M • 980 MB ROM • ~1.4 GB RAM                    │  │
│  │ 🟢 Optimal Fit: Fast code generation on your CPU      │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ 🪶 Qwen2.5-Coder-0.5B-Instruct            [ ⬇ Download ]│  │
│  │ Q4_K_M • 390 MB ROM • ~600 MB RAM                    │  │
│  │ 🟢 Ultra-lightweight: Maximum battery efficiency      │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
│  [ 📁 Import from Device (.gguf) ]                          │
│  [ 🤗 Import from Hugging Face ]                            │
└─────────────────────────────────────────────────────────────┘
```

* **Device Profile Banner**: Automatically detects and displays device specifications (e.g. `POCO C85 • 6GB RAM • 32GB Free`).
* **Recommended Cards**: Displays optimal models with disk size, working RAM, and clear compatibility badges (`🟢 Optimal Fit`).
* **One-Tap Download**: Direct resumable download without terminal interaction.

### 12.2. Hugging Face Search Drawer
Tapping **`[ 🤗 Import from Hugging Face ]`** pulls up a smooth slide-up drawer:

```
┌─────────────────────────────────────────────────────────────┐
│ 🤗 Import from Hugging Face                             [✕] │
├─────────────────────────────────────────────────────────────┤
│ [ 🔍 Search GGUF models (e.g. Qwen, Llama, DeepSeek)... ]   │
├─────────────────────────────────────────────────────────────┤
│ Search Results:                                             │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ Qwen/Qwen2.5-Coder-3B-Instruct-GGUF                 [➔] │ │
│ │ 🟢 Runs on this device (Needs ~2.5 GB RAM)              │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ bartowski/Llama-3.2-3B-Instruct-GGUF                [➔] │ │
│ │ 🟡 Tight fit: May cause background app reload           │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ unsloth/DeepSeek-R1-Distill-Qwen-7B-GGUF            [➔] │ │
│ │ 🔴 High risk: Requires 5.2 GB RAM (Device has 3.2 GB free)│ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Live Search**: Direct integration with Hugging Face Hub API for GGUF model repositories.
* **Inline Risk Badges**: Each search result is tagged with `🟢 Runs on device`, `🟡 Tight fit`, or `🔴 High risk`.

### 12.3. Model Detail & Device Compatibility Analyzer Page
Tapping any model opens a dedicated detail page within the drawer:

```
┌─────────────────────────────────────────────────────────────┐
│ [← Back]  DeepSeek-R1-Distill-Qwen-7B-GGUF              [✕] │
├─────────────────────────────────────────────────────────────┤
│ Author: unsloth • Quant: Q4_K_M • Size: 4.68 GB             │
│                                                             │
│ 📊 DEVICE COMPATIBILITY CHECK                               │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ • Total Device RAM:     6.0 GB                          │ │
│ │ • Available System RAM: 3.2 GB                          │ │
│ │ • Model Working RAM:    ~5.2 GB (Weights + 4K KV Cache) │ │
│ │ • Storage Required:     4.7 GB (32.4 GB Available) [✓]  │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ 🔴 NOT RECOMMENDED FOR THIS DEVICE                          │
│ This model exceeds your available RAM. Running this will    │
│ likely cause Android to force-close Jasper.                 │
│                                                             │
│                     [ ⬇ Download Anyway ]                   │
└─────────────────────────────────────────────────────────────┘
```

### 12.4. High RAM Warning & Confirmation Modal
If a user taps `[ Download Anyway ]` on a model marked `🔴 High Risk`, Jasper presents an explicit confirmation modal to safeguard the phone:

```
┌─────────────────────────────────────────────────────────────┐
│ ⚠️ High RAM Warning                                         │
├─────────────────────────────────────────────────────────────┤
│ This model requires approximately 5.2 GB of working RAM to  │
│ run. Your phone currently has 3.2 GB of available memory.    │
│                                                             │
│ Loading this model is almost certain to freeze Jasper or    │
│ cause Android's Low Memory Killer to force-close the app.    │
│                                                             │
│ We strongly recommend using the 1.5B or 3B model instead.   │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │ Cancel & Pick Recommended │ │    I Understand, Download │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 13. AI Providers & 9Router Management UI

Jasper centralizes all model configuration, multi-account rotation, and combo orchestration inside **Settings ➔ AI Providers & Router**, keeping the main chat and project workspaces 100% focused and uncluttered.

### 13.1. Zero Chat Clutter Principle
* The Chat UI remains completely devoid of model selectors, provider dropdowns, or token tickers.
* The only bottom controls are the conversational prompt input and the mode badge button (`[ Discuss ▾ ]` / `[ Build ▾ ]`).
* All intelligence routing happens transparently behind the scenes according to the user's configured combos and defaults.

### 13.2. Provider Configuration & "Free-First" Import Drawer
When inspecting or adding a cloud provider (e.g. OpenRouter, Groq, Anthropic, DeepSeek, Google Gemini):

```
┌─────────────────────────────────────────────────────────────┐
│ [← Providers]       OpenRouter                              │
├─────────────────────────────────────────────────────────────┤
│ API Key:                                                    │
│ [ sk-or-v1-**************************************** ] [👁️]  │
│ 🔗 Don't have a key? Get it here (links to openrouter.ai/keys)│
│                                                             │
│ [ ⚡ Test & Save Key ]  ➔ (✓ Validated in 280ms)            │
├─────────────────────────────────────────────────────────────┤
│ IMPORTED MODELS (2 Active):                                 │
│ • meta-llama/llama-3.3-70b-instruct:free             [✕]    │
│ • google/gemini-2.0-flash-exp:free (👁️)               [✕]    │
│                                                             │
│                     [ + Import Models ]                     │
└─────────────────────────────────────────────────────────────┘
```

#### The "Free-First" Import Drawer
Tapping **`[ + Import Models ]`** pulls up a slide-up drawer:

```
┌─────────────────────────────────────────────────────────────┐
│ Import Models from OpenRouter                           [✕] │
├─────────────────────────────────────────────────────────────┤
│ [ 🔍 Search any model (e.g. claude-3-5, deepseek-r1)...   ] │
├─────────────────────────────────────────────────────────────┤
│ 🎁 FREE TIER MODELS (Default View):                         │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ deepseek/deepseek-r1:free                           [✓] │ │
│ │ 🧠 Reasoning • 64K Context • Free                       │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ meta-llama/llama-3.3-70b-instruct:free             [✓] │ │
│ │ Free community tier • 128K Context                      │ │
│ └─────────────────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ google/gemini-2.0-flash-exp:free                    [ ] │ │
│ │ 👁️ Vision • 1M Context • Free                            │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│                 [ Import Selected (2) ]                     │
└─────────────────────────────────────────────────────────────┘
```

* **Clean Default**: Only models with `:free` or cost=0 are displayed by default, eliminating infinite scrolling through hundreds of models.
* **Instant Search**: Typing in the search bar immediately searches the full catalog (including paid and frontier models like `claude-3-7-sonnet` or `o3-mini`).
* **Visual Capability Badges**: Models clearly display **`👁️` (Vision)** and **`🧠` (Reasoning)** badges alongside context window sizes.
* **Multi-Select**: Checkboxes allow batch-importing only the required models.

### 13.3. Add Custom Provider Modal
For self-hosted vLLM, Ollama, or third-party endpoints:

```
┌─────────────────────────────────────────────────────────────┐
│ ➕ Add Custom Provider                                  [✕] │
├─────────────────────────────────────────────────────────────┤
│ Select Protocol:                                            │
│   (●) OpenAI Compatible   (○) Anthropic Messages Compatible │
│                                                             │
│ Provider Name: [ Local vLLM Server                        ] │
│ Base URL:      [ http://192.168.1.100:8000/v1             ] │
│ API Key:       [ ******************** (Optional)          ] │
│ Default Model: [ mistralai/Mistral-Small-24B-Instruct-2501] │
│                                                             │
│ [ ⚡ Test Connection ] ➔ (✓ Handshake Successful)           │
│                                                             │
│ ℹ️ If this provider does not support GET /models, you can    │
│    manually paste model IDs to import them.                 │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │          Cancel           │ │        Save Provider      │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### 13.4. Dedicated Vision Adapter Configuration
Located in **Settings ➔ AI Providers & Router ➔ Vision Adapter**:

```
┌─────────────────────────────────────────────────────────────┐
│ 👁️ Vision Adapter Configuration                             │
├─────────────────────────────────────────────────────────────┤
│ Automatically handles image and screenshot tasks whenever   │
│ the primary coding model is text-only.                      │
│                                                             │
│ Active Vision Models (Tried in Priority Order):             │
│   1. ≡ google/gemini-2.0-flash-exp:free                     │
│   2. ≡ openai/gpt-4o                                        │
│                                                             │
│ [ + Assign Vision Model ]                                   │
│ Status: Active • Zero Prompt Failures on Multimodal Tasks   │
└─────────────────────────────────────────────────────────────┘
```

### 13.5. Typed Combo Builder Modal
Users can create as many combos as they wish to ensure uninterrupted coding:

```
┌─────────────────────────────────────────────────────────────┐
│ ⚡ Create Model Combo                                   [✕] │
├─────────────────────────────────────────────────────────────┤
│ Combo Name: [ Free-Coding-Beast                           ] │
│                                                             │
│ Combo Type:                                                 │
│   (○) 💬 Chat (Used for discussions & ideation)             │
│   (●) 💻 Coding (Used for building & agentic editing)       │
│   (○) 🛡️ Other / General (Used as backup fallback)          │
│                                                             │
│ Execution Strategy:                                         │
│   (●) Fallback (Sequentially attempt models on error)       │
│   (○) Round-Robin (Distribute across keys/models evenly)    │
│                                                             │
│ Models in Priority Order:                                   │
│   1. ≡ deepseek/deepseek-r1:free (🧠)          [Primary]    │
│   2. ≡ meta-llama/llama-3.3-70b-instruct:free  [Fallback 1] │
│   3. ≡ qwen2.5-coder-1.5b (Local On-Device)    [Fallback 2] │
│                                                             │
│ [ + Add Model to Combo ]                                    │
│                                                             │
│ ┌───────────────────────────┐ ┌───────────────────────────┐ │
│ │          Cancel           │ │         Save Combo        │ │
│ └───────────────────────────┘ └───────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Drag-and-Drop Prioritization**: Reorder models using drag handles (`≡`).
* **Default Assignment**: Users can mark one Chat Combo and one Coding Combo as default.
* **Intelligent Non-Combo Fallbacks**: If no combos are configured, users select a **Default Chat Model** and **Default Coding Model**, and Jasper automatically uses remaining imported models as fallbacks.

### 13.6. External Tool Connection Cards
Displays the integration status with developer environments:
* **Google Antigravity**: Session authenticated (`🟢 Connected • Models provisioned via Antigravity`).
* **GitHub Models**: Token authenticated (`🟢 Connected • Access to hosted GitHub catalog`).

---

## 14. Project Settings: Code Philosophy Configuration

Located in `[⚙️ Project Settings] ➔ Agent & Compilation ➔ Code Philosophy`:

```
┌─────────────────────────────────────────────────────────────┐
│ 📐 CODE PHILOSOPHY                                          │
├─────────────────────────────────────────────────────────────┤
│ Governs how strictly Jasper avoids unnecessary boilerplate, │
│ duplicate helpers, and redundant dependencies.              │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (○) 🟢 Lite                                             │ │
│ │     Standard clean code. Minimal constraints on         │ │
│ │     scaffolding and utility packages.                   │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (●) 🔵 Full (Default)                                   │ │
│ │     Disciplined engineering. Enforces native platform   │ │
│ │     APIs, reuses existing code from project graph, and  │ │
│ │     writes minimal viable code.                         │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (○) 🟣 Ultra                                            │ │
│ │     Radical minimalism. Blocks all new dependencies     │ │
│ │     without manual approval, co-locates code to single  │ │
│ │     files, and aggressively eliminates all indirection. │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Interactive Radio Group**: Standard Android touch target (min 48px height per option) with immediate state persistence to `.jasper/project-config.json`.
* **Zero UI Noise Policy**: The Code Philosophy rules execute silently inside the agent runtime. The Chat Mission Card does not display noisy metrics or bragging text, keeping the interface completely focused on the developer's goals.

---

## 15. Skills & MCP Management Page (`/skills-mcp`)

Accessed via the Hamburger Menu (`≡`) ➔ **`🧩 Skills & MCP`** (navigates to a dedicated full-screen page, not a drawer).

This page provides a clean, touch-ergonomic command center for managing all skills and Model Context Protocol (MCP) integrations.

```
┌─────────────────────────────────────────────────────────────┐
│ [← Back]                 Skills & MCP                [+ Add]│
├─────────────────────────────────────────────────────────────┤
│  [ Skills (12) ]                    [ MCP Tools (4) ]       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🐙 GitHub                                         (●)   │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🎯 Linear                                         (●)   │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ ▲ Vercel                                          (○)   │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 🌐 Puppeteer Web Operator                         (●)   │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 15.1. Page Header & Minimalist Card Anatomy
* **Header Architecture**:
  * Top Left: `[← Back]` button returns to previous screen (Chat or Projects Hub).
  * Center: Clean title `Skills & MCP`.
  * Top Right: `[+ Add]` action button triggers the Add Integration modal flow.
* **Minimalist Rectangular Cards**:
  * **Visual Cleanliness**: Displays strictly the verified **Icon** and **Tool Name** on the left, and the **Toggle Switch `(●) / (○)`** on the right. No provenance labels, no redundant badges, no clutter.
  * **Master Toggle**: Tapping the toggle switch enables or disables the tool inside the active agent runtime immediately without revoking authentication or deleting credentials.
  * **Card Click Behavior**: Directly clicking anywhere on the card body (outside the toggle) opens the **Tool Capabilities & Inspection Sheet**.

---

### 15.2. Tool Capabilities & Inspection Sheet (On Card Click)

Tapping an MCP card slides up a bottom sheet revealing its exposed tools and removal action:

```
┌─────────────────────────────────────────────────────────────┐
│ 🐙 GitHub                                             [✕]   │
├─────────────────────────────────────────────────────────────┤
│ EXPOSED CAPABILITIES & TOOLS                                │
│                                                             │
│ • search_repositories(query, sort)                          │
│ • create_pull_request(title, head, base, body)              │
│ • list_issues(repo, state)                                  │
│ • create_issue(title, body, labels)                         │
│ • get_file_contents(repo, path, ref)                        │
│ • push_commit(branch, message, files)                       │
│                                                             │
│ ─────────────────────────────────────────────────────────── │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │                  🗑️ Delete Connection                   │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Exposed Functions List**: Human-scannable inventory of callable tools (`search()`, `create_issue()`, etc.) currently accessible to Jasper's Blue and Green teams.
* **Delete Button (`🗑️ Delete Connection`)**: Placed at the bottom in destructive styling. Tapping it opens a confirmation dialog:
  * *"Are you sure you want to delete this connection? Jasper will no longer have access to this tool."*
  * If confirmed, immediately revokes remote OAuth tokens (if Composio) or terminates stdio processes, deletes the local record, and dismisses the sheet.

---

### 15.3. The Add Integration Modal Flow (`[+ Add]`)

Tapping `[+ Add]` in the top header launches a two-step guided setup modal.

#### Step 1: Type Selection
```
┌─────────────────────────────────────────────────────────────┐
│ Add Integration                                       [✕]   │
├─────────────────────────────────────────────────────────────┤
│ What would you like to add?                                 │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (●) 🔌 MCP Tool                                         │ │
│ │     Connect an external tool or service API via MCP     │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ (○) 🧩 Skill                                            │ │
│ │     Add new capabilities via instructions (skill.md)    │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │                        [ Next ➔ ]                       │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

#### Step 2 (Option A): Adding an MCP Tool
```
┌─────────────────────────────────────────────────────────────┐
│ Connect MCP Tool                                      [✕]   │
├─────────────────────────────────────────────────────────────┤
│ Tool Name                                                   │
│ [ Supabase Inspector                                      ] │
│                                                             │
│ Server URL / Endpoint                                       │
│ [ https://mcp.supabase.com/sse                            ] │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ Requires Authentication                             (●) │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ [ 🔐 Authenticate Tool ]                                │ │
│ │ (Opens OAuth sheet / Bearer token prompt)               │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │                        [ Save ]                         │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Requires Authentication Toggle**:
  * Off: Direct open connection (public or local stdio).
  * On: Prompts inline authentication via `[ 🔐 Authenticate Tool ]` (OAuth or token entry).
* **Validation & Icon Resolution on Save**:
  * Tapping `[ Save ]` initiates an instant handshake check against the endpoint (`tools/list`).
  * Jasper verifies protocol compliance. If invalid, displays an inline error banner.
  * Automatically fetches and parses the server's favicon/logo to populate the card's verified icon.
  * Mounts the verified MCP tool immediately into the active list.

#### Step 2 (Option B): Adding a Skill
```
┌─────────────────────────────────────────────────────────────┐
│ Add New Skill                                         [✕]   │
├─────────────────────────────────────────────────────────────┤
│ Skill Name                                                  │
│ [ Next.js Migration Specialist                            ] │
│                                                             │
│ Choose Installation Method:                                 │
│ [ 📁 Upload skill.md ]           [ 💻 Run Skill Command ]   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ── If "Upload skill.md" selected: ──                        │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ 📄 Choose File from Device                              │ │
│ │ [ Browse Storage... ]                                   │ │
│ │ (Selected: nextjs-migration.md)                         │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ── If "Run Skill Command" selected: ──                      │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ Installation Command                                    │ │
│ │ [ npx skills add vercel/nextjs-skill                    ] │ │
│ │                                                         │ │
│ │ [ ⚡ Install ]                                          │ │
│ │ (Executes inside PRoot shell with inline terminal logs) │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │                        [ Save ]                         │ │
│ └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

* **Option 1: Upload `skill.md`**: User browses local Android storage, selects a `.md` file, inputs a skill name, and clicks `Save`. Stored in `~/.jasper/skills/<name>/SKILL.md`.
* **Option 2: Run Skill Command**: User pastes a CLI install command (e.g. `npx skills add ...`), clicks `[ ⚡ Install ]` which executes in PRoot with inline progress logs, then clicks `Save` to mount it.

---

### 15.4. In-Chat Just-in-Time Connect Prompt
When an agent encounters a goal requiring an unauthenticated Composio tool (e.g., user asks *"Create a Linear ticket for this"*), the agent suspends execution and injects an interactive authorization card directly into the chat:

```
┌─────────────────────────────────────────────────────────────┐
│ 🎯 Linear Integration Required                              │
│ Jasper needs permission to create issues in your Linear     │
│ workspace to complete this task.                            │
│                                                             │
│ [ 🔗 Connect Linear ]                           [ Cancel ]  │
└─────────────────────────────────────────────────────────────┘
```

* **One-Tap Authorization**: Tapping `[ 🔗 Connect Linear ]` launches the secure Composio-hosted Connect Link in an Android Chrome Custom Tab.
* **Auto-Resume**: Upon completing OAuth, the Custom Tab closes automatically, the tool card in the chat updates to `🟢 Connected`, and Jasper immediately resumes and completes the action.

---

*Document compiled and verified for Jasper Mobile User Interface Specifications.*

