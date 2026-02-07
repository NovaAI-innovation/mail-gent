# Memory with PostgreSQL

**Source:** https://docs.agno.com/memory/working-with-memories/postgres-memory.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Memory with PostgreSQL

## Code

```python mem-postgres-memory.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb

# Setup Postgres
db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
db = PostgresDb(db_url=db_url)

agent = Agent(
    db=db,
    update_memory_on_run=True,
)

agent.print_response("My name is John Doe and I like to play basketball on the weekends.")
agent.print_response("What's do I do in weekends?")
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set environment variables">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai sqlalchemy 'psycopg[binary]'
    ```
  </Step>

  <Step title="Run Example">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
      python mem-postgres-memory.py
      ```

      ```bash Windows theme={null}
      python mem-postgres-memory.py
      ```
    </CodeGroup>
  </Step>
</Steps>
