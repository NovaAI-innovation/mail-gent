# Milvus

**Source:** https://docs.agno.com/knowledge/vector-stores/milvus/usage/milvus-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Milvus

## Code

```python cookbook/08_knowledge/vector_db/milvus_db/milvus_db.py theme={null}
import asyncio

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.milvus import Milvus

vector_db = Milvus(
    collection="recipes",
    uri="tmp/milvus.db",
)

knowledge = Knowledge(
    name="My Milvus Knowledge Base",
    description="This is a knowledge base that uses a Milvus DB",
    vector_db=vector_db,
)

asyncio.run(
    knowledge.ainsert(
        name="Recipes",
        url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
        metadata={"doc_type": "recipe_book"},
    )
)

agent = Agent(knowledge=knowledge)
agent.print_response("How to make Tom Kha Gai", markdown=True)

vector_db.delete_by_name("Recipes")

vector_db.delete_by_metadata({"doc_type": "recipe_book"})
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U pymilvus pypdf openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/milvus_db/milvus_db.py
    ```
  </Step>
</Steps>
