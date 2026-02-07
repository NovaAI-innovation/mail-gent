# Agent with Knowledge

**Source:** https://docs.agno.com/models/providers/native/vercel/usage/knowledge.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Knowledge

## Code

```python cookbook/11_models/vercel/knowledge.py theme={null}
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.models.vercel import V0
from agno.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge = Knowledge(
    vector_db=PgVector(table_name="recipes", db_url=db_url),
)
# Add content to the knowledge
knowledge.insert(
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"
)

agent = Agent(model=V0(id="v0-1.0-md"), knowledge=knowledge)
agent.print_response("How to make Thai curry?", markdown=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export V0_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U sqlalchemy pgvector pypdf openai agno
    ```
  </Step>

  <Step title="Run PgVector">
    ```bash  theme={null}
    docker run -d \
      -e POSTGRES_DB=ai \
      -e POSTGRES_USER=ai \
      -e POSTGRES_PASSWORD=ai \
      -e PGDATA=/var/lib/postgresql/data/pgdata \
      -v pgvolume:/var/lib/postgresql/data \
      -p 5532:5432 \
      --name pgvector \
      agnohq/pgvector:16
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/vercel/knowledge.py
    ```
  </Step>
</Steps>
