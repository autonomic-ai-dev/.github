<div align="center">
  <img src="https://raw.githubusercontent.com/autonomic-ai-dev/.github/master/assets/logo.png" width="250" alt="Autonomic AI Logo" />
  <h1>☸️ Autonomic AI</h1>
  <p><b>Kubernetes for AI agents — cloud-native infrastructure for autonomous software engineering.</b></p>
  <p><i>Structure beats intelligence. Deterministic execution over probabilistic hallucination. Built entirely in Rust.</i></p>
</div>

---

## 🛑 The Problem: The Python Monolith
The current generation of autonomous AI agents (Devin, AutoGPT, LangGraph) suffer from three fatal engineering flaws:
1. **The Monolith Trap:** They attempt to handle prompt generation, memory retrieval, tool execution, and state management inside massive, single-process Python loops. When one tool fails, the entire runtime crashes.
2. **Context Collapse:** Pushing 100K+ tokens of conversation history into a single prompt leads to severe "Lost in the Middle" syndrome, infinite hallucination loops, and astronomical API costs.
3. **Zero Data Sovereignty:** Enterprise engineering teams legally cannot send proprietary, unreleased source code to third-party cloud agents. 

## ⚡ The Solution: Cloud-Native Separation of Concerns
**Autonomic AI** rejects the monolith. We treat agent architecture like cloud-native infrastructure: discrete, specialized daemons communicating over strict, type-safe interfaces (MCP, NATS, HTTP health).

By providing deterministic workflows and precise memory retrieval, we enable **tiny local models** to match the execution reliability of massive cloud agents — 100% local, private, and sovereign.

[Platform mapping →](https://github.com/autonomic-ai-dev/agent-body/blob/master/docs/cloud-native-platform.md)

---

## ☸️ The Platform Stack

Our stack is composable. Adopt one component or the full control plane.

### Control plane & data plane
* **[`agent-body`](https://github.com/autonomic-ai-dev/agent-body)** — *Control plane.* Agent OS: `autonomic` CLI, supervisor, unified `~/.autonomic/` workspace.
* **[`agent-brain`](https://github.com/autonomic-ai-dev/agent-brain)** — *Memory store.* SQLite + HNSW routing; ~500 tokens per turn instead of mega-prompts.
* **[`agent-spine`](https://github.com/autonomic-ai-dev/agent-spine)** — *Workflow engine.* YAML DAGs, immutable snapshots, HITL gates.
* **[`agent-heart`](https://github.com/autonomic-ai-dev/agent-heart)** — *Controller / GC.* Token budgets and scheduled memory maintenance.

### Mesh, runtime, policy, observability
* **[`agent-nerves`](https://github.com/autonomic-ai-dev/agent-nerves)** — *Service mesh.* NATS JetStream event bus.
* **[`agent-muscle`](https://github.com/autonomic-ai-dev/agent-muscle)** — *Execution runtime.* Sandboxed commands and training jobs.
* **[`agent-immune`](https://github.com/autonomic-ai-dev/agent-immune)** — *Admission policy.* OSV scan and sandboxed execution.
* **[`agent-eyes`](https://github.com/autonomic-ai-dev/agent-eyes)** — *Observability.* DOM index, capture, visual QA.
* **[`agent-mouth`](https://github.com/autonomic-ai-dev/agent-mouth)** — *Ingress / gateway.* AST validation, Slack approvals, notifications.

---

## 🔒 Why Developers Trust This Stack

1. **No "Magic" Prompts:** We do not rely on the LLM to dynamically figure out what to do next. `agent-spine` dictates the exact DAG workflow. The LLM is only used as a micro-translator for tiny, isolated tasks.
2. **Zero Telemetry:** The ecosystem runs natively on your machine. Your codebase, your database, your secrets. Nothing leaves your laptop unless you explicitly configure a remote LLM API.
3. **Memory Safety & Concurrency:** Written purely in Rust. Sub-millisecond state transitions, no Python GIL bottlenecks, and complete memory safety.

---

## 🤝 The Platform
Autonomic AI is open source and composable. You do not need the full stack to adopt one component — e.g. optimize vector search in `agent-brain` without touching the workflow engine.

We are building the sovereign software engineer of the future.
