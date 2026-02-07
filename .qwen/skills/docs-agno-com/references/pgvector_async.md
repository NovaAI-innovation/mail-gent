# PgVector Async

**Source:** https://docs.agno.com/knowledge/vector-stores/pgvector/usage/async-pgvector-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# PgVector Async

## Code

```python cookbook/08_knowledge/vector_db/pgvector/async_pg_vector.py theme={null}
import asyncio

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

vector_db = PgVector(table_name="recipes", db_url=db_url)

knowledge_base = Knowledge(
    vector_db=vector_db,
)

agent = Agent(knowledge=knowledge_base)

if __name__ == "__main__":

    asyncio.run(
        knowledge_base.ainsert(url="https://docs.agno.com/introduction/agents.md")
    )

    asyncio.run(
        agent.aprint_response("What is the purpose of an Agno Agent?", markdown=True)
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U psycopg2-binary pgvector pypdf openai agno
    ```
  </Step>

  <Snippet file="run-pgvector-docker.mdx" />

  <Step title="Set environment variables">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/pgvector/async_pg_vector.py
    ```
  </Step>
</Steps>
