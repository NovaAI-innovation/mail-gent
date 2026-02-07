# Milvus Async Hybrid Search

**Source:** https://docs.agno.com/knowledge/vector-stores/milvus/usage/async-milvus-db-hybrid-search.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Milvus Async Hybrid Search

## Code

```python cookbook/08_knowledge/vector_db/milvus_db/async_milvus_db_hybrid_search.py theme={null}
import asyncio
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.milvus import Milvus, SearchType

vector_db = Milvus(
    collection="recipes", uri="tmp/milvus.db", search_type=SearchType.hybrid
)

knowledge = Knowledge(
    vector_db=vector_db,
)

asyncio.run(knowledge.ainsert(
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
))

agent = Agent(knowledge=knowledge)
if __name__ == "__main__":
    asyncio.run(agent.aprint_response("How to make Tom Kha Gai", markdown=True))
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
    python cookbook/08_knowledge/vector_db/milvus_db/async_milvus_db_hybrid_search.py
    ```
  </Step>
</Steps>
