# Run Your AgentOS

**Source:** https://docs.agno.com/agent-os/run-your-os.md
**Section:** Docs

**Description:** Run a local AgentOS in 20 lines of code.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Run Your AgentOS

> Run a local AgentOS in 20 lines of code.

Save the following code to `agno_agent.py`:

```python agno_agent.py lines theme={null}
from agno.os import AgentOS
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.anthropic import Claude

agent = Agent(
    name="Agno Agent",
    model=Claude(id="claude-sonnet-4-5"),
    db=SqliteDb(db_file="agno.db"),
    add_history_to_context=True,
    markdown=True,
)

agent_os = AgentOS(agents=[agent])
app = agent_os.get_app()

if __name__ == "__main__":
    agent_os.serve(app="agno_agent:app", reload=True)
```

<Check>
  In \~20 lines: an Agent with memory and state, served as a FastAPI application.
</Check>

## Run Your AgentOS

<Steps>
  <Step title="Set up your virtual environment">
    <CodeGroup>
      ```bash Mac theme={null}
      uv venv --python 3.12
      source .venv/bin/activate
      ```

      ```bash Windows theme={null}
      uv venv --python 3.12
      .venv\Scripts\activate
      ```
    </CodeGroup>
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno anthropic 'fastapi[standard]' sqlalchemy
    ```
  </Step>

  <Step title="Export your Anthropic API key">
    <CodeGroup>
      ```bash Mac theme={null}
      export ANTHROPIC_API_KEY=sk-***
      ```

      ```bash Windows theme={null}
      setx ANTHROPIC_API_KEY sk-***
      ```
    </CodeGroup>
  </Step>

  <Step title="Run your AgentOS">
    ```bash  theme={null}
    fastapi dev agno_agent.py
    ```
  </Step>
</Steps>

Your AgentOS is now running at `http://localhost:8000`.

| Endpoint                       | Description                   |
| ------------------------------ | ----------------------------- |
| `http://localhost:8000`        | Connect to the control plane  |
| `http://localhost:8000/docs`   | Interactive API documentation |
| `http://localhost:8000/config` | View AgentOS configuration    |
