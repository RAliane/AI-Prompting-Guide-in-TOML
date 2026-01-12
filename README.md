# AI-Prompting-Guide-in-TOML
TOML prompting guide for consistent and reproducible use of AI chat and agents to do whatever you will.
# AI-Agent-TOML-Workflow


### 1. **README.md**
# AI-Agent-TOML-Workflow

**A structured, TOML-driven workflow for AI agents.**

This repository is a follow-up to [How-To-Build-YOUR-AI-APPs](https://github.com/RAliane/How-To-Build-YOUR-AI-APPs), focusing on how to use **TOML** as a machine- and human-readable configuration for AI agents. TOML allows you to define constraints, tasks, and workflows in a structured way, ensuring the AI "thinks" only after you've defined exactly what it should do.

---

## Why TOML for AI Agents?

- **Human-Readable**: TOML is easy for humans to write and review, making it ideal for defining AI workflows.
- **Machine-Readable**: TOML is easily parsed by code, ensuring the AI can interpret your instructions precisely.
- **Predictable**: By defining constraints, dependencies, and tasks upfront, you reduce the risk of unexpected AI behavior.
- **Auditable**: TOML files serve as a clear record of what the AI was instructed to do, improving transparency and debugging.

---

## TOML Example

Below is a full, working TOML configuration for an AI agent workflow:

```toml
[Context]
project_name = "Decision Intelligence Pipeline"
human_role = "AI Engineer / Platform Consultant"
goal_summary = "Create production-ready AI pipelines with constraint enforcement, ranking, and retrieval."
human_chain_of_thought = "Thinking for the AI before the AI thinks — explaining exactly what I want."

[Do]
- Follow human instructions precisely
- Respect code syntax, linting, and project conventions
- Precompute dependencies and validate before execution
- Test outputs (unit, integration, system)

[DoNot]
- Never hallucinate code or new programming concepts
- Do not make assumptions — ask for missing context
- Never optimize for politeness instead of correctness

[Tools]
available_tools = ["Airtable", "Directus", "Directus MCP", "n8n", "PostgreSQL", "FastAPI", "Redis"]
tool_access = { Directus = "Read/Write", "MCP Server" = "Query/Update", Airtable = "Query" }

[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules and data",
  "Validate schema and config",
  "Generate or manipulate code",
  "Run tests on outputs",
  "Document results"
]

[Dependencies]
required_libraries = ["PostgreSQL", "FastAPI", "Directus", "n8n"]
required_services = ["Auth0", "Redis"]
required_files = ["config.json", "schema.sql"]
required_data = ["user_data.csv", "embedding_vectors.db"]

[Precompute]
compile_modules = true
validate_schema = true
preload_data = true
check_service_availability = true
resolve_external_dependencies = true

[Prompt]
description = "Build AI pipeline enforcing hard/soft constraints, generating code safely, and documenting reasoning."

[Output]
outputs_list = [
  "Code (linted and validated)",
  "Dependency validation report",
  "Test results",
  "Execution reasoning chain",
  "Documentation"
]

[Traits]
agent_traits = [
  "Never make assumptions",
  "Ask clarifying questions",
  "Follow logical reasoning",
  "Validate all outputs",
  "Document chain of thought"
]
```

---

## How to Use

1. **Load the TOML**: The AI agent reads the TOML file to understand the workflow, constraints, and tasks.
2. **Precompute Dependencies**: The agent verifies all dependencies (libraries, services, files, data) are available.
3. **Validate**: The agent checks the schema, config, and data integrity.
4. **Execute Tasks**: The agent performs the tasks in the order defined in the TOML.
5. **Generate Output**: The agent produces the outputs listed in the TOML.
6. **Document Reasoning**: The agent logs its chain of thought and results for auditing.

---

## Workflow Diagram

```
Load TOML → Precompute Dependencies → Validate → Execute Tasks → Generate Output → Document Reasoning
```

---

## Benefits of TOML for AI Pipelines

- **Safety**: Constraints and dependencies are explicitly defined, reducing the risk of unexpected behavior.
- **Predictability**: The AI follows a clear, predefined workflow.
- **Auditability**: TOML files serve as a record of instructions, making it easier to debug and review.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
```

---

### 2. **agent_config.toml**
```toml
[Context]
project_name = "Decision Intelligence Pipeline"
human_role = "AI Engineer / Platform Consultant"
goal_summary = "Create production-ready AI pipelines with constraint enforcement, ranking, and retrieval."
human_chain_of_thought = "Thinking for the AI before the AI thinks — explaining exactly what I want."

[Do]
- Follow human instructions precisely
- Respect code syntax, linting, and project conventions
- Precompute dependencies and validate before execution
- Test outputs (unit, integration, system)

[DoNot]
- Never hallucinate code or new programming concepts
- Do not make assumptions — ask for missing context
- Never optimize for politeness instead of correctness

[Tools]
available_tools = ["Airtable", "Directus", "Directus MCP", "n8n", "PostgreSQL", "FastAPI", "Redis"]
tool_access = { Directus = "Read/Write", "MCP Server" = "Query/Update", Airtable = "Query" }

[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules and data",
  "Validate schema and config",
  "Generate or manipulate code",
  "Run tests on outputs",
  "Document results"
]

[Dependencies]
required_libraries = ["PostgreSQL", "FastAPI", "Directus", "n8n"]
required_services = ["Auth0", "Redis"]
required_files = ["config.json", "schema.sql"]
required_data = ["user_data.csv", "embedding_vectors.db"]

[Precompute]
compile_modules = true
validate_schema = true
preload_data = true
check_service_availability = true
resolve_external_dependencies = true

[Prompt]
description = "Build AI pipeline enforcing hard/soft constraints, generating code safely, and documenting reasoning."

[Output]
outputs_list = [
  "Code (linted and validated)",
  "Dependency validation report",
  "Test results",
  "Execution reasoning chain",
  "Documentation"
]

[Traits]
agent_traits = [
  "Never make assumptions",
  "Ask clarifying questions",
  "Follow logical reasoning",
  "Validate all outputs",
  "Document chain of thought"
]
```

---

### 3. **.gitignore**
```gitignore
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# AI/ML
*.h5
*.pth
*.tflite
*.pb
*.onnx
*.pt
*.ckpt

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Data
*.csv
*.json
*.db
*.sqlite
*.parquet
*.feather

# Logs
*.log
logs/
*.log.*

# IDE
.idea/
.vscode/
*.swp
*.swo
```

---

### 4. **LICENSE**
```plaintext
MIT License

Copyright (c) 2026 Rayan Aliane

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

### 5. **run_agent.py** (Optional)
```python
import tomllib

def load_toml_config(file_path: str) -> dict:
    """Load and parse a TOML configuration file."""
    with open(file_path, "rb") as f:
        config = tomllib.load(f)
    return config

def print_agent_config(config: dict) -> None:
    """Print the parsed TOML configuration."""
    print("=== AI Agent TOML Configuration ===")
    for section, values in config.items():
        print(f"\n[{section}]")
        if isinstance(values, dict):
            for key, value in values.items():
                print(f"{key}: {value}")
        elif isinstance(values, list):
            for item in values:
                print(f"- {item}")
        else:
            print(values)

if __name__ == "__main__":
    config = load_toml_config("agent_config.toml")
    print_agent_config(config)
```

---

### Repository Structure
```
AI-Agent-TOML-Workflow/
├── README.md
├── agent_config.toml
├── run_agent.py
├── .gitignore
└── LICENSE
```

