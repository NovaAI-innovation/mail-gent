# Qdrant Hybrid Search

**Source:** https://docs.agno.com/knowledge/vector-stores/qdrant/usage/qdrant-db-hybrid-search.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Qdrant Hybrid Search

## Code

```python cookbook/08_knowledge/vector_db/qdrant_db/qdrant_db_hybrid_search.py theme={null}
import typer
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.qdrant import Qdrant
from agno.vectordb.search import SearchType
from rich.prompt import Prompt

COLLECTION_NAME = "thai-recipes"

vector_db = Qdrant(
    collection=COLLECTION_NAME,
    url="http://localhost:6333",
    search_type=SearchType.hybrid,
)

knowledge = Knowledge(
    name="My Qdrant Vector Knowledge Base",
    vector_db=vector_db,
)

knowledge.insert(
    name="Recipes",
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
    metadata={"doc_type": "recipe_book"},
)

def qdrantdb_agent(user: str = "user"):
    agent = Agent(
        user_id=user,
        knowledge=knowledge,
        search_knowledge=True,
    )

    while True:
        message = Prompt.ask(f"[bold] :sunglasses: {user} [/bold]")
        if message in ("exit", "bye"):
            break
        agent.print_response(message)

if __name__ == "__main__":
    typer.run(qdrantdb_agent)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U qdrant-client typer rich pypdf openai agno
    ```
  </Step>

  <Step title="Run Qdrant">
    ```bash  theme={null}
    docker run -d --name qdrant -p 6333:6333 qdrant/qdrant:latest
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/qdrant_db/qdrant_db_hybrid_search.py
    ```
  </Step>
</Steps>
