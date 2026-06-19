<div align="center">
  <img src="https://raw.githubusercontent.com/autonomic-ai-dev/.github/master/assets/logo.png" width="250" alt="Autonomic AI Logo" />
  <h1>🧬 Autonomic AI</h1>
  <p><b>The Unix Philosophy applied to Autonomous Software Engineering.</b></p>
  <p><i>Structure beats intelligence. Deterministic execution over probabilistic hallucination. Built entirely in Rust.</i></p>
</div>

---

## 🛑 The Problem: The Python Monolith
The current generation of autonomous AI agents (Devin, AutoGPT, LangGraph) suffer from three fatal engineering flaws:
1. **The Monolith Trap:** They attempt to handle prompt generation, memory retrieval, tool execution, and state management inside massive, single-process Python loops. When one tool fails, the entire runtime crashes.
2. **Context Collapse:** Pushing 100K+ tokens of conversation history into a single prompt leads to severe "Lost in the Middle" syndrome, infinite hallucination loops, and astronomical API costs.
3. **Zero Data Sovereignty:** Enterprise engineering teams legally cannot send proprietary, unreleased source code to third-party cloud agents. 

## ⚡ The Solution: Biological Separation of Concerns
**Autonomic AI** rejects the monolith. We treat AI architecture like biological evolution: discrete, highly-specialized organs communicating over strict, type-safe interfaces (MCP). 

By providing mathematically strict workflow structures and perfectly precise memory retrieval, we enable **tiny, highly quantized local models (like 1.5B or 8B parameters)** to achieve the same execution reliability as massive $1,000/month cloud agents. All while remaining 100% local, private, and sovereign.

---

## 🫀 The Architecture (The Anatomy)

Our stack is completely decoupled. You do not need to adopt the whole body to use the organs. 

### The Core Triad
* **[`agent-brain`](#)** — *The Memory Layer.* A low-latency Rust context router. Instead of "Mega-prompts," it uses a local SQLite + filterable HNSW vector index to route only the exact ~500 tokens of context strictly required for the current micro-task. 
* **[`agent-spine`](#)** — *The Execution Layer.* A deterministic orchestration engine. It parses declarative YAML workflows into massive parallel DAGs using `tokio`. It features immutable state-transition logs for time-travel debugging and strict Human-in-the-Loop (HITL) approval gates.
* **[`agent-heart`](#)** — *The Background Pulse.* A background daemon that dynamically allocates API budgets, enforces global safety rules (blocking destructive bash commands at the AST layer), and runs cron jobs for memory distillation.

### The Ecosystem (Peripherals)
* **[`agent-immune`](#)** — Dependency fuzzing, AST linting, and sandboxed Firecracker/Docker execution to ensure generated code is perfectly safe.
* **[`agent-eyes`](#)** — Playwright-based visual QA and a LangSmith-style real-time observability dashboard.
* **[`agent-nerves`](#)** — Distributed `nats.rs` pub/sub event bus for asynchronous, multi-node agent communication.
* **[`agent-muscle`](#)** — Remote actuators handling massive local compilations, Kubernetes execution, and local LoRA model fine-tuning.
* **[`agent-mouth`](#)** — The communication layer translating complex JSON workflow states into human-readable Slack/Discord summaries and ChatOps triggers.
* **[`agent-body`](#)** — The sovereign meta-framework, shared `core` crate, and unified CLI installer that binds all organs together.

---

## 🔒 Why Developers Trust This Stack

1. **No "Magic" Prompts:** We do not rely on the LLM to dynamically figure out what to do next. `agent-spine` dictates the exact DAG workflow. The LLM is only used as a micro-translator for tiny, isolated tasks.
2. **Zero Telemetry:** The ecosystem runs natively on your machine. Your codebase, your database, your secrets. Nothing leaves your laptop unless you explicitly configure a remote LLM API.
3. **Memory Safety & Concurrency:** Written purely in Rust. Sub-millisecond state transitions, no Python GIL bottlenecks, and complete memory safety.

---

## 🤝 The Organism
Autonomic AI is completely open-source. Because of our strict separation of concerns, the codebase remains remarkably clean and approachable. You do not need to understand the DAG orchestration engine (`spine`) to optimize the vector search (`brain`). 

We are building the sovereign software engineer of the future.
