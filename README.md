# ╔══════════════════════════════════════════╗
#  ║  SECURITYX — Moderation Intelligence     ║
#  ╚══════════════════════════════════════════╝

**SecurityX** is an advanced moderation platform designed for Minecraft server networks. It provides a centralized, intelligent system for managing bans, handling reports, processing appeals, scanning plugins for malware, and coordinating staff workflows — all through a unified dashboard.

> Built for scale. Designed for teams. Powered by intelligence.

---

## Overview

SecurityX replaces fragmented moderation tooling with a single cohesive platform. Instead of juggling multiple Discord bots, spreadsheets, and manual processes, staff teams get a purpose-built command center.

The platform is split into two core components:

- **The Backend Engine** — Handles all logic, persistence, authentication, rate limiting, scheduled tasks, and external integrations.
- **The Frontend Dashboard** — A dark-themed web interface where staff manage every aspect of moderation in real time.

Communication between the two is secured through a custom request signing protocol that prevents tampering and replay attacks.

---

## Key Features

### Global Ban Management
Centralized ban database with automatic synchronization across all connected servers. Bans include detailed evidence, server origin, duration, and appeal status. Staff can issue, lift, and review bans from the dashboard or through automated Discord commands.

### Report & Evidence System
Players and staff can submit reports with attached evidence. Reports are organized by type (cheating, toxicity, exploits), assigned to investigators, and tracked through resolution. Evidence can include screenshots, logs, and replay files.

### Appeals & Ticket Workflow
Banned players can submit appeals through a structured form. Each appeal enters a ticket queue where staff review the case, communicate with the appellant, and decide on resolution. The entire conversation history is preserved.

### Plugin Malware Scanner
An automated static analysis engine that scans Minecraft plugin jars for malicious behavior. It extracts strings from compiled class files, correlates them against behavioral patterns, and produces a risk assessment with detailed findings.

> **Scanner capabilities:**
> - String extraction from bytecode
> - Behavioral pattern matching (command execution, class injection, network C2, persistence mechanisms, self-replication)
> - Obfuscation detection (30+ obfuscator signatures, heuristic analysis)
> - Structural anomaly detection (class renaming patterns, suspicious package layouts)
> - Correlation engine that weights findings across categories
> - Confidence scoring with tiered risk levels

The scanner runs asynchronously — upload a plugin, receive a scan ID, and poll for results. Backlogged scans are processed in the background without blocking the dashboard.

### Discord Integration
Real-time event notifications, command synchronization, and identity verification through Discord. Staff actions are logged to designated channels with full context. The platform verifies Discord membership before granting access.

### Role-Based Access Control
Granular permission system built on Discord role IDs. Different staff tiers (Trial Moderator, Moderator, Administrator, Owner) have different levels of access to features and data. API key authentication is available for automated tooling.

### Vault & Evidence Storage
Secure storage for sensitive evidence files with access logging. Files are linked to specific cases and can only be accessed by authorized personnel.

### Recruitment Portal
Staff applications are handled entirely within the platform. Applicants submit detailed responses to scenario-based questions. Applications are reviewed and scored by existing team members, with automated notifications at each stage.

---

## Architecture

```
                        ┌──────────────────────┐
                        │   External Services   │
                        │  (Discord, Minecraft) │
                        └──────────┬───────────┘
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
        ▼                          ▼                          ▼
┌───────────────┐        ┌─────────────────┐        ┌─────────────────┐
│   Dashboard   │◄──────►│   Backend API   │◄──────►│   Data Layer    │
│  (Web UI)     │  signed│  (Engine)        │        │  (Persistence)  │
└───────────────┘        └─────────────────┘        └─────────────────┘
```

### Request Flow
1. The dashboard signs every request using a derived key based on the session token.
2. The backend verifies the signature, checks the timestamp (anti-replay), and validates permissions.
3. Data is fetched, processed, and returned as structured responses.
4. Long-running tasks (malware scanning, evidence processing) are dispatched to background workers.

---

## Security Model

- **Request Signing** — Every API call includes a HMAC-SHA256 signature computed from the HTTP method, a timestamp, and a nonce. This prevents replay attacks and ensures request integrity.
- **Session Management** — Short-lived JWT tokens with automatic refresh. Tokens are bound to the user's Discord identity.
- **Rate Limiting** — Per-endpoint and per-user rate limits prevent abuse. The malware scanner has its own daily quota per user.
- **Input Validation** — All inputs are validated and sanitized at the boundary. File uploads are checked for type, size, and structure.
- **Access Control** — All operations are authorized against Discord role membership. No unauthenticated write operations are permitted.

---

## Malware Scanner Deep Dive

The scanner performs static analysis only — it never executes the plugin. Here's how it works:

1. **Extraction** — The JAR is decompressed and class files are enumerated. Each class file is read and printable strings are extracted from the bytecode.
2. **Filtering** — Strings that match known library patterns, common plugin mechanics, and benign API references are filtered out to reduce noise.
3. **Analysis** — Remaining strings are tested against a library of behavioral patterns organized by category:
   - Backdoor / RAT indicators
   - Code injection techniques
   - Remote payload delivery
   - Persistence mechanisms
   - Network communication (C2)
   - Self-replication
4. **Obfuscation Detection** — The scanner identifies obfuscation through:
   - Known obfuscator signatures (30+ commercial and private obfuscators)
   - Heuristic analysis (entropy, string density, reflection patterns)
   - Structural analysis of class naming conventions
5. **Correlation** — Findings are cross-referenced across categories. Certain combinations (e.g., backdoor + injection + network) receive a confidence boost.
6. **Scoring** — A risk score (0-100) and confidence level (Very Low to Very High) are calculated based on the数量和 severity of findings, correlation strength, and presence of obfuscation.

The scanner is continuously updated with new patterns and obfuscator signatures.

---

## Moderation Workflow

```
Report Filed ──► Queue Assigned ──► Investigation ──► Action Taken
                                              │
                                              ▼
                                        Ban Issued
                                              │
                                              ▼
                                     Appeal Submitted
                                              │
                                              ▼
                                     Staff Review ──► Resolution
```

Each step is tracked, logged, and visible to authorized staff. Notifications are pushed to Discord channels for real-time awareness.

---

## Deployment

The platform is self-hosted. Deployment requires:

- A compatible runtime environment for the backend engine
- A supported data store for persistence
- A Discord application for authentication and notifications
- A Minecraft server or proxy for ban synchronization

Configuration is done through environment variables. No hardcoded secrets exist in the codebase.

---

## License

Proprietary. All rights reserved.

---

*SecurityX — Moderating Minecraft, intelligently.*
