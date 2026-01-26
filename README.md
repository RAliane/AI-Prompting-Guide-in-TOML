# 🤖 AI-Prompting-Guide-in-TOML ⚡🦀

![Rust](https://img.shields.io/badge/Rust-000000?style=flat&logo=rust&logoColor=white) 
![Dioxus](https://img.shields.io/badge/Dioxus-010101?style=flat&logo=dioxus&logoColor=white) 
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

**TOML prompting guide for deterministic, type-safe, Hades-aware AI workflows.**  
"Think like Rust. Reason like Hades. Never assume safety."  

This guide enforces **structured, auditable, and deterministic AI pipelines**, inspired by Hades’ concurrency-safe hot/warm/canonical state management, caching, sharding, type safety, and persistence strategies.

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
9. [Auditing Sharding, Caching & Type Safety](#auditing-sharding--caching--type-safety)
10. [How to Extend for Your Use Case](#how-to-extend-for-your-use-case)
11. [Quick Start](#quick-start)
12. [References](#references)

---

## Overview
This repository demonstrates how to use **TOML** to define **structured, auditable AI workflows**.  
It enforces:  

- ✅ Deterministic reasoning  
- ✅ Memory safety & **type safety**  
- ✅ Concurrency awareness  
- ✅ Hot/Warm/Canonical state promotion rules  
- ✅ Schema, persistence, and migration checks  
- ✅ Sharding & caching audits  
- ✅ End-to-end reasoning chain verification

---

## Why TOML & Hades Principles
- **Human-readable**: Clear for auditing AI workflows.  
- **Machine-readable**: Can be parsed directly by Python, Rust, or your AI.  
- **Constraint-first**: No execution before verification.  
- **Deterministic**: Mirrors Hades’ strict promotion rules, type safety, and concurrency guarantees.  
- **System-aware**: Considers hot/warm/canonical state, sharding, caching, type correctness, memory safety, and deterministic persistence.

---

## TOML Configuration
**Sample `agent_config.toml`** (Hades-enhanced + type safety):

```toml
# 🦀 Hades-Aware AI Agent Configuration
[Context]
project_name = "Hades-Inspired AI Pipeline"
human_role = "AI Engineer / Rustacean Backend"
goal_summary = "Build deterministic AI pipelines respecting concurrency, memory safety, type safety, and persistence."
human_chain_of_thought = "Precompute and validate system state before AI executes."

[Reference]
system_name = "Hades"
lessons_learned = [
    "Hot/Warm/Canonical flows",
    "Race condition simulation",
    "Sharding & caching audits",
    "Persistence & migration verification",
    "Memory safety & type safety",
    "Deterministic reasoning chain"
]

[Do]
- Follow human instructions precisely
- Respect concurrency, memory safety, and type safety
- Precompute dependencies
- Test outputs rigorously
- Enforce hot/warm/canonical state correctness

[DoNot]
- Never hallucinate code or unsafe assumptions
- Skip dependency, schema, or persistence checks
- Ignore type correctness or concurrency safety
- Optimize for politeness over correctness

[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules and data",
  "Validate schema, types & concurrency safety",
  "Simulate Hot/Warm/Canonical promotion",
  "Audit caching, sharding & type correctness",
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
  "Hot->Warm->Canonical validated",
  "Persistence & migration verified"
]

soft_constraints = [
  { name = "Cache hit ratio", penalty_weight = 0.5, threshold = 0.85 },
  { name = "Shard balance", penalty_weight = 0.3, threshold = 0.9 },
  { name = "Promotion latency", penalty_weight = 0.2, threshold = 0.8 },
  { name = "Type correctness in reasoning chain", penalty_weight = 0.2, threshold = 1.0 }
]
```

⸻

Tasks & Workflows
	1.	Load TOML → AI reads all tasks, tools, constraints.
	2.	Precompute dependencies → Libraries, services, files, data.
	3.	Validate schema → Ensure DB & GraphQL type compliance.
	4.	Enforce Type Safety → Validate all data types across layers.
	5.	Simulate Hot/Warm/Canonical → Idempotent promotion, detect conflicts.
	6.	Audit caching & sharding → Verify hit ratios, shard balance, and type correctness.
	7.	Run deterministic tests → Unit, integration, system.
	8.	Document reasoning chain → Log type-safe deterministic execution.

Load TOML → Precompute → Validate → Enforce Type Safety → Simulate Promotion → Audit → Test → Document


⸻

Hot/Warm/Canonical Simulation
	•	Hot: Ephemeral, fast, in-memory state (Arc<DashMap<String, TypedValue>>)
	•	Warm: Aggregates hot updates, merges deterministically, ensures type correctness
	•	Canonical: Persistent, schema-validated, type-checked, idempotent

Simulation ensures deterministic updates and prevents race conditions and type violations.

⸻

Constraint Semantics

Hard Constraints
	•	Must pass for pipeline execution.
	•	Examples: Dependencies, schema, memory safety, type safety, deterministic concurrency.

Soft Constraints
	•	Scored 0–1, penalty if below threshold.
	•	Examples: Cache hit ratio ≥ 0.85, shard balance ≥ 0.9, reasoning chain type correctness = 1.0.

⸻

Dependencies & Validation
	•	Validate external services: Directus, PostgreSQL, Redis, Slack, Auth0.
	•	Validate files: schema.sql, config.json, user_data.csv.
	•	Validate data: embedding_vectors.db.
	•	Enforce type correctness at each layer.
	•	Simulate failures to ensure pipeline fails safely.

⸻

Auditing Sharding, Caching & Type Safety
	•	Audit cache hit ratios and thresholds.
	•	Audit shard balance and distribution.
	•	Validate type correctness for hot, warm, and canonical state entries.
	•	Ensure idempotency in state promotion and deterministic reasoning.

⸻

How to Extend for Your Use Case
	1.	Add custom tasks → Append to tasks_list and implement type-safe logic.
	2.	Add custom tools → Update available_tools, tool_access, and validate type correctness.
	3.	Add constraints → Update hard/soft constraints including type safety.
	4.	Update schema → Ensure new tables/fields are type-safe.
	5.	Add custom data → Ensure embeddings or input data conform to type expectations.
	6.	Add outputs → Include type-checked outputs in [Output].

⸻

Quick Start

git clone https://github.com/RAliane/AI-Agent-TOML-Workflow.git
cd AI-Agent-TOML-Workflow
python run_agent.py

	•	Make sure all environment variables for your services are set.
	•	Observe deterministic, type-safe reasoning chain in the logs.
	•	Simulate and audit concurrency, memory safety, hot/warm/canonical promotions.

⸻

References
	•	Hades: Deterministic Rust GraphQL Engine￼
	•	SQLx Rust ORM￼
	•	Dioxus Frontend￼

⸻

Embrace Rust-level reasoning. Audit everything. Enforce type safety. Fail safely. ⚡🦀

---