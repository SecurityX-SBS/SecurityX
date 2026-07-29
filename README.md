<p align="center">
<img width="220" height="360"src="https://github.com/SecurityX-SBS/.github/blob/9557bc54321800171756de0ec7fd396d64ea8744/profile/assets/logo.png" />
</p>

<div align="center">

  ### ⚡ *Moderation Intelligence for Minecraft Networks* ⚡

<br>

[![Status](https://img.shields.io/badge/status-active-success?style=flat-square)]()
[![Version](https://img.shields.io/badge/version-2.0-informational?style=flat-square)]()
[![Discord](https://img.shields.io/badge/discord-securityx.sbs-5865F2?style=flat-square)](https://discord.securityx.sbs)
[![Website](https://img.shields.io/badge/web-securityx.sbs-ff2b2b?style=flat-square)](https://securityx.sbs)
[![Status Page](https://img.shields.io/badge/status-status.securityx.sbs-00b894?style=flat-square)](https://status.securityx.sbs)

<br>

<br>
> **SecurityX** is an advanced, unified moderation platform designed for Minecraft server networks.  
> It replaces fragmented tooling with a single, intelligent command center — managing bans, reports, appeals,  
> plugin malware scanning, staff workflows, and Discord integration in one cohesive system.

</br>

| 🔗 Links |  |
|:---|---:|
| 🌐 **Website** | [securityx.sbs](https://securityx.sbs) |
| 💬 **Discord** | [discord.securityx.sbs](https://discord.securityx.sbs) |
| 📊 **Status** | [status.securityx.sbs](https://status.securityx.sbs) |

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Security Model](#-security-model)
- [Malware Scanner](#-malware-scanner-deep-dive)
- [Moderation Workflow](#-moderation-workflow)
- [Deployment](#-deployment)
- [License](#-license)

---

## 🌌 Overview

SecurityX replaces fragmented moderation tooling with a single cohesive platform. Instead of juggling multiple Discord bots, spreadsheets, and manual processes, staff teams get a purpose-built command center.

The platform is split into two core components:

| 🧠 Backend Engine | 🎨 Frontend Dashboard |
|:---|:---|
| Handles all logic, persistence, authentication, rate limiting, scheduled tasks, and external integrations | A dark-themed web interface where staff manage every aspect of moderation in real time |
| Processes data, enforces rules, and coordinates workers | Provides clear visualization, controls, and feedback |

Communication between the two is secured through a **custom request signing protocol** that prevents tampering and replay attacks — every request is verified before any operation occurs.

---

## 🔥 Key Features

### 🌍 Global Ban Management
Centralized ban database with **automatic synchronization** across all connected servers. Bans include detailed evidence, server origin, duration, and appeal status. Staff can issue, lift, and review bans from the dashboard or through automated Discord commands.

### 📋 Report & Evidence System
Players and staff can submit reports with attached evidence. Reports are organized by type — cheating, toxicity, exploits — assigned to investigators, and tracked through resolution. Evidence can include screenshots, logs, and replay files.

### ⚖️ Appeals & Ticket Workflow
Banned players can submit appeals through a structured form. Each appeal enters a ticket queue where staff review the case, communicate with the appellant, and decide on resolution. The entire conversation history is preserved.

### 🔬 Plugin Malware Scanner
An automated **static analysis engine** that scans Minecraft plugin jars for malicious behavior. It extracts strings from compiled class files, correlates them against behavioral patterns, and produces a risk assessment with detailed findings.

<details>
<summary><b>📌 Scanner capabilities</b></summary>
<br>

| Capability | Description |
|:---|:---|
| 🔍 **String Extraction** | Extracts printable strings from compiled bytecode |
| 🧩 **Pattern Matching** | Detects command execution, class injection, network C2, persistence, self-replication |
| 🕵️ **Obfuscation Detection** | Identifies 30+ obfuscators via signatures + heuristic analysis |
| 📐 **Structural Analysis** | Detects class renaming patterns and suspicious package layouts |
| 🔗 **Correlation Engine** | Cross-references findings across categories for confidence boosting |
| 📊 **Confidence Scoring** | Produces tiered risk levels from Very Low to Very High |

</details>
<br>

### 💬 Discord Integration
Real-time event notifications, command synchronization, and identity verification through Discord. Staff actions are logged to designated channels with full context. The platform verifies Discord membership before granting access.

### 🔐 Role-Based Access Control
Granular permission system built on Discord role IDs. Different staff tiers — Trial Moderator, Moderator, Administrator, Owner — have different levels of access to features and data. API key authentication is available for automated tooling.

### 🗄️ Vault & Evidence Storage
Secure storage for sensitive evidence files with access logging. Files are linked to specific cases and can only be accessed by authorized personnel.

### 🎮 Recruitment Portal
Staff applications are handled entirely within the platform. Applicants submit detailed responses to scenario-based questions. Applications are reviewed and scored by existing team members, with automated notifications at each stage.

### 🔌 Minecraft Plugin
SecurityX includes a lightweight server-side plugin that connects your game servers to the moderation platform. It operates silently in the background and requires no player interaction.

| Feature | Description |
|:---|:---|
| 🔄 **Ban Synchronization** | Bans issued from the dashboard or Discord are instantly enforced across all connected servers |
| 📢 **Report Forwarding** | In-game reports from players are sent directly to the moderation queue |
| 🧾 **Command Logging** | Suspicious commands and chat messages are captured for investigation |
| 🔐 **Secure Communication** | All traffic between the plugin and the backend is encrypted and authenticated |
| ⚡ **Zero Overhead** | Minimal performance impact — designed for servers of any scale |

The plugin binds to the Minecraft server lifecycle, intercepts key events, and communicates with the backend through the same signed request protocol used by the dashboard. No player data leaves your network without proper authorization.

---

## ⚙️ How It Works

SecurityX operates as a **centralized command center** that connects your Minecraft servers, staff team, and community through a single secure backbone.

### High-Level Flow

<p align="center">
<img width="880" height="360"src="https://github.com/SecurityX-SBS/SecurityX/blob/21076ac9cbaba3652377e795d4e7931423f1d2d7/assets/arquict1.png" />
</p>

### What Happens When a Player Cheats

1. **Detection** — A player is reported by others or caught by anti-cheat. The plugin forwards the event.
2. **Evaluation** — Staff review the evidence through the dashboard. Chat logs, command history, and past infractions are available instantly.
3. **Action** — A ban is issued with one click. The plugin enforces it across **every server** in the network within seconds.
4. **Follow-up** — The player can appeal through the website. The appeal creates a ticket that staff review.
5. **Resolution** — Permanent record is archived. If unbanned, all servers are notified simultaneously.

### What Happens When a Plugin Is Scanned

1. **Upload** — A plugin `.jar` file is submitted through the dashboard.
2. **Analysis** — The scanner decompiles the bytecode, extracts strings, and tests them against behavioral patterns.
3. **Report** — A detailed report is generated showing risk level, flagged patterns, and obfuscation indicators.
4. **Decision** — Staff review the report and decide whether to allow, quarantine, or reject the plugin.

### Key Principles

| Principle | Why It Matters |
|:---|:---|
| 🔒 **Privacy-first** | Player data is only stored when relevant to a case. No telemetry, no tracking. |
| ⚡ **Real-time** | Bans and actions propagate in seconds, not minutes. |
| 🧩 **Decoupled** | The plugin, backend, and dashboard are independent — a failure in one doesn't bring down the rest. |
| 🛡️ **Defense in depth** | Multiple validation layers, signed requests, and role-based access prevent abuse of the system itself. |

<p align="center">
<img width="880" height="360"src="https://github.com/SecurityX-SBS/SecurityX/blob/ab69c77e2395b9385352fbf090a6698498b2f9c8/assets/arquict2.png" />
</p>

### 🔄 Request Flow

```
  ① Dashboard signs request with HMAC-SHA256
  ② Backend verifies signature + timestamp (anti-replay)
  ③ Permissions are validated against Discord roles
  ④ Data is fetched, processed, and returned
  ⑤ Long-running tasks → background workers
```

### 🧩 Component Design

| Component | Role |
|:---|:---|
| **🖥️ Dashboard** | Client-side interface, real-time updates, drag-and-drop evidence upload |
| **⚙️ API Engine** | Request validation, business logic, rate limiting, session management |
| **🗃️ Data Layer** | Persistent storage, indexing, query optimization, backup coordination |
| **🤖 Workers** | Background processing for malware scanning, evidence handling, notifications |

---

## 🔒 Security Model

| Layer | Mechanism |
|:---|:---|
| 🔑 **Request Signing** | HMAC-SHA256 over method + timestamp + nonce — prevents replay and tampering |
| 🎫 **Session Management** | Short-lived tokens bound to Discord identity, automatic refresh |
| ⏱️ **Rate Limiting** | Per-endpoint and per-user quotas; daily scan limits per user |
| 🧪 **Input Validation** | Multi-layer validation; file type, size, and structure verification |
| 🚪 **Access Control** | Every operation authorized against Discord role membership |
| 🔒 **Secrets** | No hardcoded secrets in codebase — all configuration through environment |

---

## 🔬 Malware Scanner Deep Dive (Out of service for testing.)

The scanner performs **static analysis only** — it never executes the plugin. Here's the pipeline:

### Step-by-Step

```
📦 JAR Upload
    │
    ▼
📂 Extraction ────── Decompress archive, enumerate class files
    │
    ▼
🔍 Extraction ────── Read bytecode, extract printable strings
    │
    ▼
🧹 Filtering ─────── Remove known library patterns and benign API noise
    │
    ▼
🧪 Analysis ──────── Test strings against behavioral pattern library
    │                    • Backdoor / RAT
    │                    • Code injection
    │                    • Remote payload delivery
    │                    • Persistence mechanisms
    │                    • Network C2 communication
    │                    • Self-replication
    ▼
🕵️ Obfuscation ───── Detect 30+ obfuscators via signatures + heuristics
    │
    ▼
🔗 Correlation ────── Cross-reference findings across categories
    │                    • backdoor + injection + network → boost
    │                    • payload + persistence → boost
    ▼
📊 Scoring ────────── Risk score (0–100) + Confidence level
                         Very Low • Low • Medium • High • Very High
```

### Key Design Decisions

- **No execution** — Static analysis only. Zero risk of triggering malware during scanning.
- **Async processing** — Upload returns immediately with a scan ID. Results are polled asynchronously.
- **Library filtering** — Known library paths and common API patterns are pre-filtered to reduce false positives.
- **Continuous updates** — Pattern library and obfuscator signatures are regularly expanded.

---

## 📋 Moderation Workflow

```
📮 Report Filed
    │
    ▼
📌 Queue Assigned
    │
    ▼
🔎 Investigation ────────► 🚫 False Report (closed)
    │
    ▼
⚖️ Action Taken ─────────► ⚠️ Warning
    │                      │
    │                      └── 🚫 Ban Issued
    │                              │
    │                              ▼
    │                         📩 Appeal Submitted
    │                              │
    │                              ▼
    │                         👥 Staff Review ────► ✅ Unban
    │                                                └── ❌ Denied
    ▼
📝 Case Closed — Full log archived
```

Every step is **tracked, logged, and visible** to authorized staff. Notifications are pushed to Discord channels for real-time awareness.

---

## 🚀 Deployment

The platform is **self-hosted**. Deployment requires:

| Requirement | Purpose |
|:---|:---|
| ☁️ **Runtime Environment** | To run the backend engine and workers |
| 🗄️ **Data Store** | Persistent storage for all platform data |
| 💬 **Discord Application** | Authentication, notifications, and staff identity |
| 🎮 **Minecraft Connection** | Ban synchronization with game servers |

> Configuration is done through environment variables. Zero hardcoded secrets.

---

## ⚠️ Disclaimer

**SecurityX is not affiliated, associated, authorized, endorsed by, or in any way officially connected with Mojang Studios, Microsoft Corporation, or any of its subsidiaries or affiliates.**

The official Minecraft game and all related trademarks, including "Minecraft," are the property of Mojang Studios and Microsoft Corporation. Our platform operates independently to provide server moderation tools that help server owners maintain a fair and enjoyable environment for their communities.

Our goal is to detect and prevent unfair advantages — cheats, hacked clients, exploit abuse — that undermine the integrity of the game experience. By taking proactive measures against malicious actors, we help foster **competitive balance, community trust, and a level playing field** for all legitimate players.

> *We are not stopping hackers to protect Mojang. We are stopping hackers because an unfair game is not fun for anyone.*

---

## 📜 License

**Proprietary** — All rights reserved.

---

<div align="center">


**SecurityX** — *Moderating Minecraft, intelligently.*

<br>

</div>
