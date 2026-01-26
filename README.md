# 🤖 AI-Prompting-Guide-in-TOML ⚡🦀

![Rust](https://img.shields.io/badge/Rust-000000?style=flat&logo=rust&logoColor=white) 
![Dioxus](https://img.shields.io/badge/Dioxus-010101?style=flat&logo=dioxus&logoColor=white) 
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

**TOML prompting guide for deterministic, Hades-aware AI workflows.**  
"Think like Rust. Reason like Hades. Never assume safety."  

This guide enforces **structured, auditable, and deterministic AI pipelines**, inspired by Hades’ concurrency-safe hot/warm/canonical state management, caching, sharding, and persistence strategies.

---

## Table of Contents
1. [Overview](#overview)
2. [Why TOML & Hades Principles](#why-toml--hades-principles)
3. [TOML Configuration](#toml-configuration)
4. [Tasks & Workflows](#tasks--workflows)
5. [Hot/Warm/Canonical Simulation](#hotwarmcanonical-simulation)
6. [Constraint Semantics](#constraint-semantics)
7. [Dependencies & Validation](#dependencies--validation)
8. [Soft & Hard Constraints](#soft--hard-constraints)
9. [Auditing Sharding & Caching](#auditing-sharding--caching)
10. [How to Extend for Your Use Case](#how-to-extend-for-your-use-case)
11. [Quick Start](#quick-start)
12. [References](#references)

---

## Overview
This repository demonstrates how to use **TOML** to define **structured, auditable AI workflows**.  
It enforces:  

- ✅ Deterministic reasoning  
- ✅ Memory safety & concurrency awareness  
- ✅ Hot/Warm/Canonical state promotion rules  
- ✅ Schema, persistence, and migration checks  
- ✅ Sharding & caching audits  

It’s a natural evolution from general AI prompting to **Rust-level system awareness**.

---

## Why TOML & Hades Principles
- **Human-readable**: Clear for humans auditing the workflow.  
- **Machine-readable**: Can be parsed directly by Python, Rust, or your AI.  
- **Constraint-first**: Forces checks before execution, no assumptions.  
- **Deterministic**: Mirrors Hades’ strict promotion rules and type safety.  
- **System-aware**: Considers concurrency, memory safety, persistence, sharding, caching, and promotion rules.

---

## TOML Configuration
**Sample `agent_config.toml`** (Hades-enhanced):

```toml
# 🦀 Hades-Aware AI Agent Configuration
[Context]
project_name = "Hades-Inspired AI Pipeline"
human_role = "AI Engineer / Rustacean Backend"
goal_summary = "Build deterministic AI pipelines respecting concurrency, memory safety, and persistence."
human_chain_of_thought = "Precompute and validate system state before AI executes."

[Reference]
system_name = "Hades"
lessons_learned = [
    "Hot/Warm/Canonical flows",
    "Race condition simulation",
    "Sharding & caching audits",
    "Persistence & migration verification",
    "Memory safety & deterministic reasoning"
]

[Do]
- Follow human instructions precisely
- Respect concurrency, memory safety, and deterministic rules
- Precompute dependencies
- Test outputs rigorously
- Enforce hot/warm/canonical state correctness

[DoNot]
- Never hallucinate code or unsafe assumptions
- Skip dependency, schema, or persistence checks
- Optimize for politeness over correctness
- Ignore race conditions or data corruption

[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules and data",
  "Validate schema and concurrency safety",
  "Simulate Hot/Warm/Canonical promotion",
  "Audit caching and sharding",
  "Run deterministic tests",
  "Document reasoning chain"
]

[Constraints]
hard_constraints = [
  "All dependencies available",
  "Schema validation passed",
  "Memory safety enforced",
  "Concurrency deterministic",
  "Hot->Warm->Canonical validated",
  "Persistence & migration verified"
]

soft_constraints = [
  { name = "Cache hit ratio", penalty_weight = 0.5, threshold = 0.85 },
  { name = "Shard balance", penalty_weight = 0.3, threshold = 0.9 },
  { name = "Promotion latency", penalty_weight = 0.2, threshold = 0.8 }
]
```

⸻

Tasks & Workflows
	1.	Load TOML → AI understands constraints & tasks.
	2.	Precompute dependencies → Libraries, services, files, data.
	3.	Validate schema → Ensure DB & GraphQL schema compliance.
	4.	Simulate Hot/Warm/Canonical → Idempotent promotion, detect conflicts.
	5.	Audit caching & sharding → Check hit ratios & balance.
	6.	Run deterministic tests → Unit, integration, system.
	7.	Document reasoning → Create an execution trace.

Load TOML → Precompute → Validate → Simulate Promotion → Audit → Test → Document


⸻

Hot/Warm/Canonical Simulation
	•	Hot: Ephemeral, fast, in-memory state.
	•	Warm: Aggregates hot updates, resolves conflicts.
	•	Canonical: Persistent, schema-validated, idempotent.

Simulation ensures deterministic updates and prevents race conditions.

⸻

Constraint Semantics

Hard Constraints
	•	Must pass for pipeline execution.
	•	Examples: Dependencies, schema validation, memory safety, deterministic concurrency.

Soft Constraints
	•	Scored 0–1, penalty applied if below threshold.
	•	Examples: Cache hit ratio ≥ 0.85, Shard balance ≥ 0.9.

⸻

Dependencies & Validation
	•	Validate external services: Directus, PostgreSQL, Redis, Slack, Auth0.
	•	Validate files: schema.sql, config.json, user_data.csv.
	•	Validate data: embedding_vectors.db.

Simulate failures to ensure pipeline fails safely.

⸻

Auditing Sharding & Caching
	•	Audit cache hit ratios and thresholds.
	•	Audit shard balance and distribution.
	•	Ensure idempotency in state promotion.

⸻

How to Extend for Your Use Case
	•	Add tasks → Extend tasks_list in TOML.
	•	Add tools → Update available_tools and tool_access.
	•	Add constraints → Append hard/soft constraints in TOML.
	•	Add schema changes → Update schema.sql and reference in TOML.
	•	Add data → Extend user_data.csv and embedding_vectors.db.
	•	Add outputs → Extend outputs_list and generate programmatically.

⸻

Quick Start

git clone https://github.com/RAliane/AI-Agent-TOML-Workflow.git
cd AI-Agent-TOML-Workflow
python run_agent.py

	•	Make sure all environment variables for your services are set.
	•	Observe deterministic reasoning chain in the logs.
	•	Simulate and audit concurrency, memory safety, hot/warm/canonical promotions.

⸻

References
	•	Hades: Deterministic Rust GraphQL Engine￼
	•	SQLx Rust ORM￼
	•	Dioxus Frontend￼

⸻

Embrace Rust-level reasoning. Audit everything. Fail safely. ⚡🦀

---