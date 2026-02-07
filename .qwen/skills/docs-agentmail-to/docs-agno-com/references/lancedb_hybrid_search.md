# LanceDB Hybrid Search

**Source:** https://docs.agno.com/knowledge/vector-stores/lancedb/usage/lance-db-hybrid-search.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# LanceDB Hybrid Search

## Code

```python cookbook/08_knowledge/vector_db/lance_db/lance_db_hybrid_search.py theme={null}
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.models.openai import OpenAIResponses
from agno.vectordb.lancedb import LanceDb, SearchType

knowledge = Knowledge(
    name="My PG Vector Knowledge Base",
    description="This is a knowledge base that uses a PG Vector DB",
    vector_db=LanceDb(
        table_name="vectors",
        uri="tmp/lancedb",
        search_type=SearchType.hybrid,
    ),
)

knowledge.insert(
    name="Recipes",
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
    metadata={"doc_type": "recipe_book"},
)

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    knowledge=knowledge,
    search_knowledge=True,
    markdown=True,
)
agent.print_response(
    "How do I make chicken and galangal in coconut milk soup", stream=True
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

  <Step title="Set environment variables">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/lance_db/lance_db_hybrid_search.py
    ```
  </Step>
</Steps>
