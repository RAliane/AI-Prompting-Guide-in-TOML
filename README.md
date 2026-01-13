# AI-Prompting-Guide-in-TOML
TOML prompting guide for consistent and reproducible use of AI chat and agents to do whatever you will.
# AI-Agent-TOML-Workflow

**A deterministic, TOML-driven workflow for AI agents.**

This repository demonstrates how to use **TOML** to define **structured, auditable, and constraint-driven** AI workflows. It’s a follow-up to [How-To-Build-YOUR-AI-APPs](https://github.com/yourusername/How-To-Build-YOUR-AI-APPs), focusing on **pre-thinking** for AI agents: defining constraints, dependencies, and tasks *before* the AI executes anything.

---

## **Why TOML for AI Agents?**
- **Human-readable**: Easy to write, review, and audit.
- **Machine-readable**: Parsed directly by code, reducing ambiguity.
- **Constraint-first**: Define rules before the AI executes.
- **Modular**: Separate concerns (e.g., dependencies, tasks, constraints).

---

## **What’s Inside?**
- A **complete TOML configuration** for AI workflows.
- **Schema, config, and data templates** (no ambiguity).
- **Validation and testing scripts** (ready to run).
- **Best practices** for constraint-driven AI.

---

## **TOML Configuration**
Below is the **full, working TOML** for an AI agent workflow. Copy this into `agent_config.toml`:

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
required_files = ["config.json", "schema.sql", "user_data.csv"]
required_data = ["embedding_vectors.db"]

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

[Constraints]
hard_constraints = [
  "All dependencies must be available",
  "Schema validation must pass",
  "Auth0 token must be valid"
]
soft_constraints = [
  { name = "Precomputed modules coverage", penalty_weight = 0.5, threshold = 0.9 },
  { name = "Retrieval relevance score", penalty_weight = 0.3, threshold = 0.85 }
]

[Schema]
# SQL schema for constraints, rankings, and embeddings
schema_definition = """
CREATE TABLE constraints (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    type TEXT CHECK (type IN ('hard', 'soft')),
    description TEXT,
    penalty_weight FLOAT DEFAULT 1.0,
    validation_query TEXT
);

CREATE TABLE rankings (
    id SERIAL PRIMARY KEY,
    task_id INTEGER REFERENCES tasks(id),
    item_id INTEGER,
    score FLOAT NOT NULL,
    rationale TEXT,
    timestamp TIMESTAMP DEFAULT NOW()
);

CREATE TABLE retrieval_metadata (
    id SERIAL PRIMARY KEY,
    query TEXT NOT NULL,
    source TEXT NOT NULL,
    results_count INTEGER,
    relevance_score FLOAT,
    timestamp TIMESTAMP DEFAULT NOW()
);

CREATE TABLE embedding_vectors (
    id SERIAL PRIMARY KEY,
    data_id INTEGER,
    vector FLOAT[],
    model_name TEXT,
    timestamp TIMESTAMP DEFAULT NOW()
);
"""

[Config]
# JSON config for services, embeddings, and testing
config_definition = """
{
  "environment": "development",
  "services": {
    "Directus": {
      "endpoint": "https://directus.example.com",
      "auth": { "strategy": "jwt", "token_env_var": "DIRECTUS_TOKEN" },
      "permissions": { "collections": ["read", "write"], "mcp_server": ["query", "update"] }
    },
    "PostgreSQL": {
      "host": "localhost",
      "port": 5432,
      "database": "ai_pipeline",
      "user_env_var": "PG_USER",
      "password_env_var": "PG_PASSWORD"
    },
    "Redis": { "host": "localhost", "port": 6379, "use_for": ["caching", "locking"] },
    "Auth0": {
      "domain": "your-domain.auth0.com",
      "client_id_env_var": "AUTH0_CLIENT_ID",
      "client_secret_env_var": "AUTH0_CLIENT_SECRET"
    }
  },
  "embeddings": {
    "model": "sentence-transformers/all-MiniLM-L6-v2",
    "vector_dimensions": 384,
    "storage": "SQLite"
  },
  "constraints": {
    "hard_fail_on_violation": true,
    "soft_constraint_threshold": 0.7
  },
  "testing": {
    "unit_test_coverage_threshold": 0.9,
    "integration_test_timeout": 30
  }
}
"""

[Data]
# Sample structure for user_data.csv and embedding_vectors.db
user_data_csv = """
user_id,input_text,metadata,expected_output
1,"Build a ranking pipeline","{""timestamp"": ""2026-01-13""}","Pipeline built; rankings generated."
2,"Validate schema","{""timestamp"": ""2026-01-13""}","Schema valid; no errors."
"""
```

---

## **How It Works**
1. **Load the TOML**: The AI agent reads `agent_config.toml` to understand the workflow.
2. **Precompute Dependencies**: Verify all dependencies (libraries, services, files, data).
3. **Validate**: Check schema, config, and data integrity.
4. **Execute Tasks**: Follow the task list in order.
5. **Generate Output**: Produce the outputs defined in the TOML.
6. **Document Reasoning**: Log all actions and constraints checked.

---

## **Workflow Diagram**
```
Load TOML → Precompute Dependencies → Validate → Execute Tasks → Generate Output → Document Reasoning
```

---

## **Key Files**
### **1. `agent_config.toml`**
Copy the TOML above into this file.

### **2. `schema.sql`**
```sql
-- Constraints
CREATE TABLE constraints (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    type TEXT CHECK (type IN ('hard', 'soft')),
    description TEXT,
    penalty_weight FLOAT DEFAULT 1.0,
    validation_query TEXT
);

-- Rankings
CREATE TABLE rankings (
    id SERIAL PRIMARY KEY,
    task_id INTEGER REFERENCES tasks(id),
    item_id INTEGER,
    score FLOAT NOT NULL,
    rationale TEXT,
    timestamp TIMESTAMP DEFAULT NOW()
);

-- Retrieval metadata
CREATE TABLE retrieval_metadata (
    id SERIAL PRIMARY KEY,
    query TEXT NOT NULL,
    source TEXT NOT NULL,
    results_count INTEGER,
    relevance_score FLOAT,
    timestamp TIMESTAMP DEFAULT NOW()
);

-- Embedding vectors
CREATE TABLE embedding_vectors (
    id SERIAL PRIMARY KEY,
    data_id INTEGER,
    vector FLOAT[],
    model_name TEXT,
    timestamp TIMESTAMP DEFAULT NOW()
);
```

### **3. `config.json`**
```json
{
  "environment": "development",
  "services": {
    "Directus": {
      "endpoint": "https://directus.example.com",
      "auth": {
        "strategy": "jwt",
        "token_env_var": "DIRECTUS_TOKEN"
      },
      "permissions": {
        "collections": ["read", "write"],
        "mcp_server": ["query", "update"]
      }
    },
    "PostgreSQL": {
      "host": "localhost",
      "port": 5432,
      "database": "ai_pipeline",
      "user_env_var": "PG_USER",
      "password_env_var": "PG_PASSWORD"
    },
    "Redis": {
      "host": "localhost",
      "port": 6379,
      "use_for": ["caching", "locking"]
    },
    "Auth0": {
      "domain": "your-domain.auth0.com",
      "client_id_env_var": "AUTH0_CLIENT_ID",
      "client_secret_env_var": "AUTH0_CLIENT_SECRET"
    }
  },
  "embeddings": {
    "model": "sentence-transformers/all-MiniLM-L6-v2",
    "vector_dimensions": 384,
    "storage": "SQLite"
  },
  "constraints": {
    "hard_fail_on_violation": true,
    "soft_constraint_threshold": 0.7
  },
  "testing": {
    "unit_test_coverage_threshold": 0.9,
    "integration_test_timeout": 30
  }
}
```

### **4. `user_data.csv`**
```csv
user_id,input_text,metadata,expected_output
1,"Build a ranking pipeline","{""timestamp"": ""2026-01-13""}","Pipeline built; rankings generated."
2,"Validate schema","{""timestamp"": ""2026-01-13""}","Schema valid; no errors."
```

### **5. `run_agent.py`**
```python
import tomllib
import json
import sqlite3
import os

def load_toml_config(file_path: str) -> dict:
    """Load and parse the TOML config."""
    with open(file_path, "rb") as f:
        return tomllib.load(f)

def validate_schema(schema_path: str, db_path: str = "embedding_vectors.db") -> bool:
    """Validate the schema against the live database."""
    with open(schema_path, "r") as f:
        schema = f.read()
    conn = sqlite3.connect(db_path)
    cursor = conn.cursor()
    try:
        cursor.executescript(schema)
        print("Schema validation: PASSED")
        return True
    except sqlite3.Error as e:
        print(f"Schema validation: FAILED\nError: {e}")
        return False
    finally:
        conn.close()

def check_dependencies(config: dict) -> bool:
    """Check if all dependencies are available."""
    for service, settings in config["services"].items():
        if service == "Directus":
            token = os.getenv(settings["auth"]["token_env_var"])
            if not token:
                print(f"Missing {settings['auth']['token_env_var']}")
                return False
        elif service == "PostgreSQL":
            if not os.getenv(settings["user_env_var"]) or not os.getenv(settings["password_env_var"]):
                print(f"Missing PostgreSQL credentials")
                return False
    print("Dependency check: PASSED")
    return True

if __name__ == "__main__":
    config = load_toml_config("agent_config.toml")
    print("=== AI Agent Configuration ===")
    for section, values in config.items():
        print(f"\n[{section}]")
        if isinstance(values, dict):
            for key, value in values.items():
                print(f"{key}: {value}")
    validate_schema("schema.sql")
    check_dependencies(json.loads(config["Config"]["config_definition"]))
```

### **6. `.gitignore`**
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

# Data
*.csv
*.db
*.sqlite
*.parquet
*.feather

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Logs
*.log
logs/
*.log.*
```

### **7. `LICENSE` (MIT)**
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

## **How to Use**
1. **Clone the repo**:
   ```bash
   git clone https://github.com/yourusername/AI-Agent-TOML-Workflow.git
   cd AI-Agent-TOML-Workflow
   ```
2. **Set up the files**:
   - Save the TOML as `agent_config.toml`.
   - Save the SQL as `schema.sql`.
   - Save the JSON as `config.json`.
   - Save the CSV as `data/user_data.csv`.
3. **Run the agent**:
   ```bash
   python run_agent.py
   ```
4. **Customize**:
   - Update `agent_config.toml` for your workflow.
   - Extend `run_agent.py` with your tasks.

---

## **Constraint Semantics**
### **Hard Constraints**
- **Definition**: Must be satisfied for the pipeline to proceed.
- **Examples**:
  - "All dependencies must be available."
  - "Schema validation must pass."

### **Soft Constraints**
- **Definition**: Scored (0.0–1.0). Pipeline passes if cumulative score ≥ threshold.
- **Examples**:
  - "Precomputed modules should cover 90% of tasks."
  - "Retrieval relevance score should average ≥ 0.85."

---

## **Testing**
### **Unit Tests**
- Coverage ≥ 90%.
- Example:
  ```python
  def test_schema_validation():
      assert validate_schema("schema.sql") == True
  ```

### **Integration Tests**
- Compare outputs to `expected_output` in `user_data.csv`.
- Tolerance: ±5% for ranking scores.

### **System Tests**
- Simulate failures (e.g., missing dependencies).
- Pipeline must fail gracefully.

---

## **Best Practices**
1. **Redundancy > Ambiguity**: Repeat constraints in multiple sections.
2. **Fail Fast**: Hard constraints halt execution immediately.
3. **Audit Everything**: Log all actions and constraints checked.
4. **Test Early**: Validate schema, config, and data before execution.

---

## **Next Steps**
- [ ] Review and customize `agent_config.toml`.
- [ ] Add your data to `user_data.csv`.
- [ ] Extend `run_agent.py` with your tasks.
- [ ] Run `python run_agent.py` to validate your setup.

Here’s the **new section** to add to your `README.md` under **"How to Extend for Your Use Case"**. This will guide Rayan (or anyone else) on how to customize the workflow for their specific needs:

---

## **How to Extend for Your Use Case**
This section explains how to **customize** the workflow for your specific tasks, tools, or constraints.

---

### **1. Adding Custom Tasks**
To add a new task to the pipeline:
1. **Update `agent_config.toml`**:
   Add your task to the `tasks_list` under `[Tasks]`:
   ```toml
   [Tasks]
   tasks_list = [
     "Verify dependencies",
     "Precompute modules and data",
     "Validate schema and config",
     "Generate or manipulate code",
     "Run tests on outputs",
     "Document results",
     "Your custom task here"  # <-- Add this line
   ]
   ```
2. **Implement the task in `run_agent.py`**:
   Add a function to handle your task, e.g.:
   ```python
   def your_custom_task():
       print("Running your custom task...")
       # Add your logic here
   ```
3. **Call the function in the workflow**:
   Update the execution flow in `run_agent.py` to include your task.

---

### **2. Adding Custom Tools**
To integrate a new tool (e.g., a new API or service):
1. **Update `agent_config.toml`**:
   Add the tool to `[Tools]`:
   ```toml
   [Tools]
   available_tools = ["Airtable", "Directus", "Directus MCP", "n8n", "PostgreSQL", "FastAPI", "Redis", "YourTool"]
   tool_access = { Directus = "Read/Write", "MCP Server" = "Query/Update", Airtable = "Query", YourTool = "Read" }
   ```
2. **Update `config.json`**:
   Add the tool’s configuration (e.g., API endpoint, credentials):
   ```json
   "YourTool": {
     "endpoint": "https://yourtool.example.com",
     "auth": {
       "strategy": "api_key",
       "key_env_var": "YOURTOOL_API_KEY"
     }
   }
   ```
3. **Add validation logic**:
   Update `check_dependencies.py` to verify the tool’s availability:
   ```python
   elif service == "YourTool":
       api_key = os.getenv(settings["auth"]["key_env_var"])
       if not api_key:
           print(f"Missing {settings['auth']['key_env_var']}")
           return False
   ```

---

### **3. Adding Custom Constraints**
To define a new constraint:
1. **Update `agent_config.toml`**:
   Add your constraint to `[Constraints]`:
   ```toml
   [Constraints]
   hard_constraints = [
     "All dependencies must be available",
     "Schema validation must pass",
     "Auth0 token must be valid",
     "Your hard constraint here"  # <-- Add this line
   ]
   soft_constraints = [
     { name = "Precomputed modules coverage", penalty_weight = 0.5, threshold = 0.9 },
     { name = "Retrieval relevance score", penalty_weight = 0.3, threshold = 0.85 },
     { name = "Your soft constraint", penalty_weight = 0.2, threshold = 0.7 }  # <-- Add this line
   ]
   ```
2. **Implement validation logic**:
   Add a function to validate your constraint in `run_agent.py`:
   ```python
   def validate_your_constraint():
       # Add your validation logic here
       return True  # or False if the constraint fails
   ```
3. **Integrate the validation**:
   Call your function in the workflow and handle failures.

---

### **4. Customizing the Schema**
To extend the database schema:
1. **Update `schema.sql`**:
   Add your tables or columns:
   ```sql
   CREATE TABLE your_table (
       id SERIAL PRIMARY KEY,
       your_column TEXT NOT NULL
   );
   ```
2. **Update `agent_config.toml`**:
   Reference your new table in the `[Schema]` section:
   ```toml
   [Schema]
   schema_definition = """
   CREATE TABLE your_table (
       id SERIAL PRIMARY KEY,
       your_column TEXT NOT NULL
   );
   """
   ```
3. **Validate the schema**:
   Run `python scripts/validate_schema.py` to ensure everything is correct.

---

### **5. Customizing Data**
To use your own data:
1. **Update `user_data.csv`**:
   Add your data rows:
   ```csv
   user_id,input_text,metadata,expected_output
   3,"Your custom input","{""timestamp"": ""2026-01-13""}","Your expected output"
   ```
2. **Update `embedding_vectors.db`**:
   Add your embeddings (if applicable) using SQLite or your preferred tool.

---

### **6. Customizing the Workflow**
To modify the workflow logic:
1. **Update `run_agent.py`**:
   Adjust the execution order or add new steps:
   ```python
   def run_custom_workflow():
       # Your custom workflow logic here
       pass
   ```
2. **Test your changes**:
   Run `python run_agent.py` and verify the output.

---

### **7. Adding Custom Outputs**
To define new outputs:
1. **Update `agent_config.toml`**:
   Add your output to `[Output]`:
   ```toml
   [Output]
   outputs_list = [
     "Code (linted and validated)",
     "Dependency validation report",
     "Test results",
     "Execution reasoning chain",
     "Documentation",
     "Your custom output here"  # <-- Add this line
   ]
   ```
2. **Generate the output**:
   Update `run_agent.py` to produce your output:
   ```python
   def generate_custom_output():
       # Your logic here
       return "Your custom output"
   ```

---

### **8. Testing Your Extensions**
To ensure your customizations work:
1. **Add unit tests**:
   Extend `test_pipeline.py` with tests for your new logic:
   ```python
   def test_your_custom_task():
       assert your_custom_task() == "Expected result"
   ```
2. **Run tests**:
   ```bash
   python -m pytest scripts/test_pipeline.py --cov=scripts --cov-fail-under=90
   ```

---

### **9. Example: Adding a Custom Task**
Let’s say you want to add a task to **"Send a notification"** after generating outputs.

#### **Step 1: Update `agent_config.toml`**
```toml
[Tasks]
tasks_list = [
  "Verify dependencies",
  "Precompute modules and data",
  "Validate schema and config",
  "Generate or manipulate code",
  "Run tests on outputs",
  "Document results",
  "Send notification"  # <-- New task
]
```

#### **Step 2: Implement the Task in `run_agent.py`**
```python
def send_notification():
    print("Sending notification...")
    # Add your notification logic here (e.g., email, Slack, etc.)
    return True
```

#### **Step 3: Integrate the Task**
Update the workflow in `run_agent.py`:
```python
if __name__ == "__main__":
    config = load_toml_config("agent_config.toml")
    validate_schema("schema.sql")
    check_dependencies(json.loads(config["Config"]["config_definition"]))
    send_notification()  # <-- Call your new task
```

---

### **10. Example: Adding a Custom Tool**
Let’s say you want to integrate **Slack** for notifications.

#### **Step 1: Update `agent_config.toml`**
```toml
[Tools]
available_tools = ["Airtable", "Directus", "Slack"]
tool_access = { Directus = "Read/Write", Slack = "Post" }
```

#### **Step 2: Update `config.json`**
```json
"Slack": {
  "webhook_url_env_var": "SLACK_WEBHOOK_URL",
  "channel": "#ai-pipeline"
}
```

#### **Step 3: Add Validation Logic**
Update `check_dependencies.py`:
```python
elif service == "Slack":
    webhook_url = os.getenv(settings["webhook_url_env_var"])
    if not webhook_url:
        print(f"Missing {settings['webhook_url_env_var']}")
        return False
```

#### **Step 4: Use the Tool in `run_agent.py`**
```python
def send_slack_notification(message: str):
    import requests
    webhook_url = os.getenv("SLACK_WEBHOOK_URL")
    payload = {"text": message, "channel": "#ai-pipeline"}
    response = requests.post(webhook_url, json=payload)
    return response.status_code == 200
```

---

### **11. Debugging Tips**
- **Log everything**: Use `print()` or a logging library to track execution.
- **Fail fast**: If a constraint fails, stop the pipeline and log the error.
- **Test incrementally**: Add one customization at a time and test it.

---

### **12. Contributing Back**
If you’ve extended this workflow in a useful way, consider:
- Opening a **pull request** to share your improvements.
- Adding your use case to the **examples** section.

