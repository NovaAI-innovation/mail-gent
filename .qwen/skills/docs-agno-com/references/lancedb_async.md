# LanceDB Async

**Source:** https://docs.agno.com/knowledge/vector-stores/lancedb/usage/async-lance-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# LanceDB Async

## Code

```python cookbook/08_knowledge/vector_db/lance_db/lance_db.py theme={null}
import asyncio

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.lancedb import LanceDb

vector_db = LanceDb(
    table_name="vectors",
    uri="tmp/lancedb",
)

knowledge = Knowledge(
    name="Basic SDK Knowledge Base",
    description="Agno 2.0 Knowledge Implementation with LanceDB",
    vector_db=vector_db,
)

agent = Agent(knowledge=knowledge)

if __name__ == "__main__":
    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
            metadata={"doc_type": "recipe_book"},
        )
    )

    asyncio.run(
        agent.aprint_response("List down the ingredients to make Massaman Gai", markdown=True)
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U lancedb pypdf openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/lance_db/lance_db.py
    ```
  </Step>
</Steps>
