<div align="center">
  <img src="https://raw.githubusercontent.com/autonomic-ai-dev/.github/master/assets/logo.png" width="220" alt="Autonomic AI Logo" />
  <h1>🧬 AUTONOMIC AI</h1>
  <p><b>Right skill, right memory, right time, for AI coding agents.</b></p>
  <p><i>Local-first. Deterministic workflows. Built in Rust.</i></p>

  <p>
    <a href="https://github.com/autonomic-ai-dev/agent-brain"><img src="https://img.shields.io/badge/Component-agent--brain-00f2fe?style=flat-square" alt="agent-brain"></a>
    <a href="https://github.com/autonomic-ai-dev/agent-spine"><img src="https://img.shields.io/badge/Component-agent--spine-00f2fe?style=flat-square" alt="agent-spine"></a>
    <a href="https://github.com/autonomic-ai-dev/homebrew-tap"><img src="https://img.shields.io/badge/Homebrew-autonomic--ai--dev%2Ftap-10b981?style=flat-square&logo=homebrew&logoColor=white" alt="Homebrew"></a>
    <a href="https://modelcontextprotocol.io"><img src="https://img.shields.io/badge/Protocol-MCP-6366f1?style=flat-square" alt="MCP"></a>
  </p>
</div>

---

## Scope

Autonomic AI is two components: **agent-brain** and **agent-spine**. They are the whole product.

- **agent-brain** decides which skills, rules, and memories an agent sees on each turn.
- **agent-spine** runs deterministic YAML workflows with approval gates.

Earlier work on a wider 11-organ stack is out of scope. `agent-body-core` is no longer a dependency of either component.

---

## agent-brain: right context on every turn

agent-brain is a local MCP router. Each turn, `route_task` returns a small, ranked set of skills, rules, and memory within a token budget, so the agent does not get the whole library. Host hooks block brain tools until the agent has routed the turn.

- Warm-cache route p95 is **24 ms** on a synthetic 1,000-item index (`agent-brain bench --scale`).
- Recall@3 on the repository's 20-case CI eval is **0.95**, against a threshold of 0.85. The sample is small; it measures known phrasings, not real sessions.
- **Known issue:** route latency has a long tail in real use. One user's 7-day stats show a P95 of about 28 s across 506 routes. This is under investigation.

---

## agent-spine: deterministic workflows

agent-spine parses YAML workflow DAGs and runs them with explicit state transitions and human-in-the-loop approval gates. The LLM works inside the steps the workflow defines; it does not choose the next step itself.

NATS is optional. Set `AUTONOMIC_NATS_URL` to publish workflow events. Credentials come only from the environment:

| Variable | Purpose |
| :--- | :--- |
| `AUTONOMIC_NATS_URL` | Server URL (default `nats://127.0.0.1:4222` when a connection is made) |
| `AUTONOMIC_NATS_USER`, `AUTONOMIC_NATS_PASSWORD` | Optional user and password |
| `AUTONOMIC_NATS_TLS`, `AUTONOMIC_NATS_CA`, `AUTONOMIC_NATS_CERT`, `AUTONOMIC_NATS_KEY` | Optional TLS and client certificate |
| `AUTONOMIC_NATS_INSECURE` | Set to `1` or `true` to skip user and password |

---

## Install

```bash
brew tap autonomic-ai-dev/tap
brew install agent-brain agent-spine

agent-brain install --global   # configure MCP and host hooks
agent-brain doctor             # check the install
agent-spine init               # set up agent-spine
```

Update with `brew upgrade agent-brain agent-spine`. `agent-spine update` prints this command; it no longer downloads releases itself.

agent-brain reads its settings from `config.yaml` in its home directory, `~/.autonomic/memory` by default. Set `AGENT_BRAIN_HOME` to use another directory.

---

## Local first

agent-brain stores its database, vector index, and route logs under `~/.autonomic/`. Nothing leaves your machine unless you configure a NATS server or a remote model API.

---

## Open source

Autonomic AI is planned as open source. The repositories are private during development, so the links above will not open for people outside the team yet.

---

<div align="center">
  <sub>Autonomic AI · Right context, right time</sub>
</div>
