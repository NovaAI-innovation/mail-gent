# PgVector

**Source:** https://docs.agno.com/knowledge/vector-stores/pgvector/usage/pgvector-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# PgVector

## Code

```python cookbook/08_knowledge/vector_db/pgvector/pgvector_db.py theme={null}
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

vector_db = PgVector(table_name="vectors", db_url=db_url)

knowledge = Knowledge(
    name="My PG Vector Knowledge Base",
    description="This is a knowledge base that uses a PG Vector DB",
    vector_db=vector_db,
)
knowledge.insert(
    name="Recipes",
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
    metadata={"doc_type": "recipe_book"},
)

agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    read_chat_history=True,
)

agent.print_response("How do I make pad thai?", markdown=True)

vector_db.delete_by_name("Recipes")

vector_db.delete_by_metadata({"doc_type": "recipe_book"})
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
    python cookbook/08_knowledge/vector_db/pgvector/pgvector_db.py
    ```
  </Step>
</Steps>
