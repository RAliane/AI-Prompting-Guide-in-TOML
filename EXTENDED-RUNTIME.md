## 🚀 Quick Start

1. **Install UV** (Python package manager):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Set up dependencies**:
   ```bash
   uv add toml pydantic requests httpx typer psycopg2 redis retry
   ```

3. **Run the agent**:
   ```bash
   uv run run_agent.py
   ```

---

## 📋 Overview

This repository presents a **TOML-based framework** for AI workflows, featuring:
- Configuration-driven prompting
- Plugin architecture for tool integration
- MCP (Model Context Protocol) support
- Built-in database connectivity (PostgreSQL, Redis)
- Hasura integration for GraphQL operations
- CLI interface for easy execution

---

## 🛠️ Core Components

### 1. TOML Configuration (`agent_config.toml`)
```toml
[Context]
project_name = "Decision Intelligence Pipeline"
description = "AI workflow for structured prompt execution"

[MCP]
server_url = "https://mcp.yourdomain.com"
api_key = "your_api_key_here"
models = ["gpt-4", "llama-3"]
max_retries = 3

[Tools]
PostgreSQL = { host = "localhost", port = 5432, database = "ai_data", user = "ai_user", password = "secure" }
Redis = { host = "localhost", port = 6379 }
Slack = { webhook_url = "https://hooks.slack.com/..." }
Hasura = { url = "https://your-hasura-instance.com", admin_secret = "your_admin_secret" }

[Tasks]
tasks = [
  "MCP:gpt-4:Validate initial requirements",
  "PLUGIN:postgres.check_connection",
  "PLUGIN:redis.ping",
  "PLUGIN:hasura.introspect",
  "MCP:llama-3:Generate architecture proposal"
]

[Output]
format = "markdown"
verbosity = "detailed"
```

---

## 🤖 Runtime System

### Core Runtime (`run_agent.py`)
```python
import tomllib
from pydantic import BaseModel, validator
from typing import List, Dict, Optional
import httpx
from retry import retry
import typer
from plugins.base import Plugin

# --- Models ---
class MCPConfig(BaseModel):
    server_url: str
    api_key: Optional[str] = None
    models: List[str] = []
    max_retries: int = 3

class AgentConfig(BaseModel):
    context: Dict[str, str]
    role: Dict[str, str]
    tasks: List[str]
    constraints: Dict[str, List[str]]
    mcp: MCPConfig
    tools: Dict[str, Dict[str, str]]
    output: Dict[str, str]

# --- MCP Client with Retry ---
class MCPClient:
    def __init__(self, config: MCPConfig):
        self.config = config
        self.client = httpx.AsyncClient(timeout=30.0)

    @retry(httpx.HTTPError, tries=3, delay=1)
    async def query_model(self, model: str, prompt: str) -> str:
        headers = {"Authorization": f"Bearer {self.config.api_key}"} if self.config.api_key else {}
        response = await self.client.post(
            f"{self.config.server_url}/v1/models/{model}/query",
            json={"prompt": prompt},
            headers=headers
        )
        response.raise_for_status()
        return response.json()["output"]

# --- Agent Runtime ---
class Agent:
    def __init__(self, config_path: str):
        with open(config_path, "rb") as f:
            config = tomllib.load(f)
        self.config = AgentConfig(**config)
        self.mcp_client = MCPClient(self.config.mcp)
        self.plugins = self._load_plugins()

    def _load_plugins(self) -> Dict[str, Plugin]:
        from plugins.postgres import PostgresPlugin
        from plugins.redis import RedisPlugin
        from plugins.slack import SlackPlugin
        from plugins.hasura import HasuraPlugin

        return {
            "postgres": PostgresPlugin(**self.config.tools.get("PostgreSQL", {})),
            "redis": RedisPlugin(**self.config.tools.get("Redis", {})),
            "slack": SlackPlugin(**self.config.tools.get("Slack", {})),
            "hasura": HasuraPlugin(**self.config.tools.get("Hasura", {}))
        }

    async def run(self):
        typer.echo(f"🚀 Starting agent: {self.config.context['project_name']}")

        for step in self.config.tasks:
            typer.echo(f"📋 Executing: {step}")

            if step.startswith("MCP:"):
                model = step.split(":")[1].strip()
                output = await self.mcp_client.query_model(
                    model=model,
                    prompt=" ".join(step.split(":")[2:])
                )
                typer.echo(f"✨ MCP Output: {output}")

            elif step.startswith("PLUGIN:"):
                plugin_name, action = step.split(":")[1].split(".")
                result = self.plugins[plugin_name].execute(action)
                typer.echo(f"🔌 Plugin Result: {result}")

# --- CLI ---
app = typer.Typer()

@app.command()
def run(config_path: str = "agent_config.toml"):
    """Run the AI agent with the given TOML configuration"""
    import asyncio
    agent = Agent(config_path)
    asyncio.run(agent.run())

if __name__ == "__main__":
    app()
```

---

## 🧩 Plugin System

### Base Plugin (`plugins/base.py`)
```python
from abc import ABC, abstractmethod

class Plugin(ABC):
    def __init__(self, **kwargs):
        self.config = kwargs

    @abstractmethod
    def execute(self, action: str) -> str:
        pass
```

### PostgreSQL Plugin (`plugins/postgres.py`)
```python
import psycopg2
from .base import Plugin

class PostgresPlugin(Plugin):
    def execute(self, action: str) -> str:
        conn = psycopg2.connect(
            host=self.config.get("host", "localhost"),
            port=self.config.get("port", 5432),
            dbname=self.config["database"],
            user=self.config["user"],
            password=self.config["password"]
        )
        cursor = conn.cursor()

        if action == "check_connection":
            cursor.execute("SELECT 1")
            return "PostgreSQL connection successful"

        elif action.startswith("query:"):
            query = action.split(":", 1)[1]
            cursor.execute(query)
            return f"Query executed: {cursor.fetchall()}"

        return "Unknown action"
```

### Redis Plugin (`plugins/redis.py`)
```python
import redis
from .base import Plugin

class RedisPlugin(Plugin):
    def execute(self, action: str) -> str:
        r = redis.Redis(
            host=self.config.get("host", "localhost"),
            port=self.config.get("port", 6379)
        )

        if action == "ping":
            return "PONG" if r.ping() else "Connection failed"

        elif action.startswith("get:"):
            key = action.split(":", 1)[1]
            return r.get(key) or "Key not found"

        return "Unknown action"
```

### Hasura Plugin (`plugins/hasura.py`)
```python
import httpx
from .base import Plugin

class HasuraPlugin(Plugin):
    def execute(self, action: str) -> str:
        url = self.config["url"]
        admin_secret = self.config.get("admin_secret")

        if action.startswith("query:"):
            query = action.split(":", 1)[1]
            headers = {"x-hasura-admin-secret": admin_secret} if admin_secret else {}
            response = httpx.post(
                f"{url}/v1/graphql",
                json={"query": query},
                headers=headers
            )
            return f"GraphQL Result: {response.json()}"

        elif action.startswith("introspect:"):
            headers = {"x-hasura-admin-secret": admin_secret} if admin_secret else {}
            response = httpx.post(
                f"{url}/v1/graphql",
                json={"query": """
                    query {
                      __schema {
                        types {
                          name
                        }
                      }
                    }
                """},
                headers=headers
            )
            return f"Schema: {response.json()['data']['__schema']['types']}"

        return "Unknown action"
```

---

## 📁 File Structure

```
AI-Agent-TOML-Workflow/
├── run_agent.py            # Core runtime
├── agent_config.toml       # Configuration
├── plugins/               # Plugin system
│   ├── __init__.py
│   ├── base.py
│   ├── postgres.py
│   ├── redis.py
│   ├── slack.py
│   └── hasura.py
├── .gitignore
└── LICENSE
```

---

## 🎯 Usage Examples

### 1. Basic Execution
```bash
uv run run_agent.py
```

### 2. Custom Configuration
```bash
uv run run_agent.py run ./custom_config.toml
```

### 3. Task Examples
```toml
[Tasks]
tasks = [
  "MCP:gpt-4:Analyze these requirements: [text]",
  "PLUGIN:postgres.query:SELECT * FROM users",
  "PLUGIN:redis.get:user_cache_123",
  "PLUGIN:hasura.query:{ users { id name } }"
]
```

---

## 🔧 Advanced Features

### 1. MCP with Retry Logic
- Automatic retries on HTTP errors
- Configurable retry count and delay

### 2. Plugin Architecture
- Extensible base class
- Auto-loaded from config
- Clean error handling

### 3. Database Integration
- PostgreSQL connection management
- Redis key-value operations

### 4. Hasura Integration
- GraphQL query execution
- Schema introspection
- Admin secret support

---

## 🔮 Future Directions

1. **Additional Plugins**:
   - Directus integration
   - Airtable support
   - Custom tool plugins

2. **Enhanced MCP**:
   - Streaming responses
   - Model chaining
   - Context management

3. **Runtime Improvements**:
   - Logging system
   - Plugin auto-discovery
   - Async task queue

4. **Deployment**:
   - Docker support
   - Cloud integration
   - Monitoring

---

## 🏗️ Development

### Adding New Plugins
1. Create a new file in `plugins/`
2. Extend the `Plugin` base class
3. Add to `Agent._load_plugins()`

### Customizing MCP
Edit the `MCPConfig` section in `agent_config.toml`:
```toml
[MCP]
server_url = "https://your-mcp-server.com"
api_key = "your_key_here"
models = ["custom-model-1", "custom-model-2"]
max_retries = 5
```

---

## 📄 License

MIT License. See `LICENSE` for details.

---

## 👋 About

Created by **Rayan Aliane** for structured, reproducible AI workflows. Built on the principle that prompts should be infrastructure, not conversation.

For questions or contributions, please open an issue or pull request.