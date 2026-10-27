<div align="center">
  <img src="https://raw.githubusercontent.com/autonomic-ai-dev/.github/master/assets/logo.png" width="200" alt="Autonomic AI Logo" />
  <h1>AUTONOMIC AI</h1>
  <p><b>The Local-First Cognitive Governor & Procedure Graph for Autonomous Coding Agents.</b></p>
  <p><i>Token-budgeted turn router, host policy sentry, and self-evolving execution DAGs. Built in Rust.</i></p>

  <p>
    <a href="https://github.com/autonomic-ai-dev/agent-brain"><img src="https://img.shields.io/badge/Component-agent--brain-ffffff?style=flat-square&labelColor=18181b" alt="agent-brain"></a>
    <a href="https://github.com/autonomic-ai-dev/agent-spine"><img src="https://img.shields.io/badge/Component-agent--spine-ffffff?style=flat-square&labelColor=18181b" alt="agent-spine"></a>
    <a href="https://github.com/autonomic-ai-dev/homebrew-tap"><img src="https://img.shields.io/badge/Homebrew-autonomic--ai--dev%2Ftap-ffffff?style=flat-square&logo=homebrew&logoColor=white&labelColor=18181b" alt="Homebrew"></a>
    <a href="https://modelcontextprotocol.io"><img src="https://img.shields.io/badge/Protocol-MCP-ffffff?style=flat-square&labelColor=18181b" alt="MCP"></a>
    <a href="https://autonomic-ai.dev"><img src="https://img.shields.io/badge/Website-autonomic--ai.dev-ffffff?style=flat-square&labelColor=18181b" alt="Website"></a>
  </p>
</div>

---

## The Dual-Engine Architecture

Autonomic AI decouples stochastic reasoning from deterministic execution into two purpose-built engines:

* **`agent-brain`**: The cognitive governor, procedure graph, and token-budgeted memory engine. It controls what skills, rules, and failure traps an agent sees on each turn through a local-first SQLite WAL database (`~/.autonomic/memory/brain.db`), in-memory HNSW vector index, and host pre-tool hooks.
* **`agent-spine`**: The deterministic YAML workflow engine. It executes declarative Directed Acyclic Graphs (DAGs) with milestone approval gates, isolated sandboxes, and immutable cryptographic state snapshots.

---

## 4 Strategic Pillars

### 1. Self-Evolving Procedures & Auto-Distillation
When agents explore codebases, execute shell commands, patch files, and pass `.verify/run.sh`, `agent-brain` automatically captures session transcripts. Passing tool transitions are distilled into state transitions (`procedure_edges` and `workflow_trajectory`). Future tasks query the graph via recursive CTEs, injecting proven execution DAGs rather than generic advice.

### 2. Closed-Loop Negative Reinforcement & Trap Detection
When a command fails or CI exits non-zero, `agent-brain verify` registers the failure fingerprint and squelches the failing recipe from recommendations. If an agent attempts the same defective pattern, the brain injects high-priority `TRAP WARNING: DO NOT USE <command>` constraints into `must_apply`.

### 3. Active Policy Sentry (Host-Level Guardrails)
Passive markdown prompts are easily ignored by LLMs under heavy context load. `agent-brain` hooks directly into the host runtime (`route_gate.py`, `command_policy.rs`) across **Claude Code**, **Cursor**, **Antigravity (AGY)**, and **OpenCode**, physically blocking unrouted turns, destructive commands, or unscouted full-file dumps.

### 4. Universal Cross-Host Neural Bus
Coding agents run in silos—Cursor in the IDE, Claude Code in terminal, Antigravity in agentic loops, and GitHub Actions in CI. `agent-brain` runs as a unified background daemon on `~/.autonomic/memory/brain.db`. A verified bug fix discovered in Claude Code terminal is immediately available to Cursor in the IDE.

---

## Quickstart

### Homebrew (macOS / Apple Silicon Universal)
```bash
brew tap autonomic-ai-dev/tap
brew install agent-brain agent-spine
agent-brain doctor
```

### Cargo (From Source)
```bash
cargo install --git https://github.com/autonomic-ai-dev/agent-brain agent-brain
cargo install --git https://github.com/autonomic-ai-dev/agent-spine agent-spine
agent-brain doctor
```

---

## Verification & Rigor

Claims of correctness are never accepted from conversational statements. Every claim must be backed by a verification receipt produced by `agent-brain verify -- <command>` that exited 0. Test outputs and logs reside strictly in `.verify/`.

---

<div align="center">
  <sub>© 2026 Autonomic AI. The Cognitive Governor & Procedure Graph for Autonomous Coding Agents.</sub>
</div>
