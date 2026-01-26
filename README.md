# 🤖 AI-Prompting-Guide-in-TOML ⚡🦀

![Rust](https://img.shields.io/badge/Rust-000000?style=flat&logo=rust&logoColor=white)
![Dioxus](https://img.shields.io/badge/Dioxus-010101?style=flat&logo=dioxus&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

**TOML-based, deterministic, type-safe AI workflows inspired by Hades’ concurrency-safe state management.**
*"Think like Rust. Reason like Hades. Never assume safety."*

---

## **Table of Contents**
1. [Overview](#overview)
2. [Why TOML & Hades?](#why-toml--hades)
3. [TOML Configuration](#toml-configuration)
4. [Workflow](#workflow)
5. [State Simulation](#state-simulation)
6. [Constraints](#constraints)
7. [Validation](#validation)
8. [Auditing](#auditing)
9. [Extending](#extending)
10. [Quick Start](#quick-start)
11. [References](#references)

---

## **Overview**
This guide enforces **structured, auditable, and deterministic AI pipelines** using TOML, inspired by Hades’ state management (hot/warm/canonical), caching, sharding, **type safety**, and persistence.

**Key Features:**
✅ Deterministic reasoning
✅ Memory & **type safety**
✅ Concurrency awareness
✅ State promotion rules (hot/warm/canonical)
✅ Schema, persistence, and migration checks
✅ Sharding & caching audits

---

## **Why TOML & Hades?**
- **Human-readable:** Clear for audits.
- **Machine-readable:** Parsable by Python, Rust, or AI.
- **Constraint-first:** Validates before execution.
- **Deterministic:** Mirrors Hades’ strict promotion, type safety, and concurrency guarantees.
- **System-aware:** Considers state, sharding, caching, **type correctness**, and persistence.

---

## **TOML Configuration**
**Sample `agent_config.toml`:**

```toml
[Context]
project_name = "Hades-Inspired AI Pipeline"
human_role = "AI Engineer / Rustacean Backend"
goal_summary = "Build deterministic, type-safe AI pipelines respecting concurrency, memory safety, and persistence."

[Reference]
system_name = "Hades"
lessons_learned = [
    "Hot/Warm/Canonical flows",
    "Race condition simulation",
    "Sharding & caching audits",
    "Type safety & migration verification",
    "Deterministic reasoning chain"
]

[Do]
- Follow instructions precisely
- Respect concurrency, memory, and type safety
- Precompute dependencies
- Test outputs rigorously

[DoNot]
- Hallucinate code or unsafe assumptions
- Skip dependency, schema, or type checks
- Ignore concurrency or type safety

[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules/data",
  "Validate schema/types/concurrency",
  "Simulate state promotion",
  "Audit caching/sharding/types",
  "Run deterministic tests",
  "Document reasoning chain"
]

[Constraints]
hard_constraints = [
  "All dependencies available",
  "Schema validation passed",
  "Memory safety enforced",
  "Type safety enforced",
  "Concurrency deterministic",
  "State promotion validated"
]
soft_constraints = [
  { name = "Cache hit ratio", penalty_weight = 0.5, threshold = 0.85 },
  { name = "Shard balance", penalty_weight = 0.3, threshold = 0.9 },
  { name = "Type correctness", penalty_weight = 0.2, threshold = 1.0 }
]
```

---

## **Workflow**
1. **Load TOML** → AI reads tasks, tools, constraints.
2. **Precompute** → Dependencies, modules, data.
3. **Validate** → Schema, types, concurrency.
4. **Simulate** → Hot/Warm/Canonical promotion.
5. **Audit** → Caching, sharding, type correctness.
6. **Test** → Unit, integration, system.
7. **Document** → Execution trace.

---

## **State Simulation**
- **Hot:** Ephemeral, in-memory state (`Arc<DashMap<String, TypedValue>>`).
- **Warm:** Aggregates hot updates, merges deterministically, ensures type correctness.
- **Canonical:** Persistent, schema-validated, type-checked, idempotent.

**Goal:** Prevent race conditions, ensure deterministic updates, and enforce type safety.

---

## **Constraints**
- **Hard:** Must pass (e.g., dependencies, schema, memory, type safety).
- **Soft:** Scored 0–1 (e.g., cache hit ratio ≥ 0.85, shard balance ≥ 0.9, type correctness = 1.0).

---

## **Validation**
- **Services:** Directus, PostgreSQL, Redis, Slack, Auth0.
- **Files:** `schema.sql`, `config.json`, `user_data.csv`.
- **Data:** `embedding_vectors.db`.
- **Types:** Enforce correctness at each layer.
- **Failures:** Simulate to ensure safe pipeline failure.

---

## **Auditing**
- Cache hit ratios and thresholds.
- Shard balance and distribution.
- Type correctness for hot, warm, and canonical state.
- Idempotency in state promotion.

---

## **Extending**
- Add tasks → Extend `tasks_list`.
- Add tools → Update `available_tools`.
- Add constraints → Append to `hard/soft_constraints`.
- Update schema → Ensure new tables/fields are type-safe.
- Add data → Conform to type expectations.

---

## **Quick Start**
```bash
git clone https://github.com/RAliane/AI-Agent-TOML-Workflow.git
cd AI-Agent-TOML-Workflow
python run_agent.py
```
- Set environment variables for services.
- Check logs for deterministic, type-safe reasoning.
- Simulate concurrency, memory, and state promotions.

---

## **References**
- [Hades](https://github.com/RAliane/Hades-A-Replacement-to-Hasura-Redis-in-Rust-Concept): Deterministic Rust GraphQL Engine
- [SQLx](https://github.com/launchbadge/sqlx): Rust ORM
- [Dioxus](https://dioxuslabs.com/): Frontend

---
**Embrace Rust-level reasoning. Audit everything. Enforce type safety. Fail safely.** ⚡🦀

---