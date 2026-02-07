# LightRAG Async

**Source:** https://docs.agno.com/knowledge/vector-stores/lightrag/usage/async-lightrag-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# LightRAG Async

## Code

```python cookbook/08_knowledge/vector_db/lightrag/lightrag.py theme={null}
import asyncio
from os import getenv

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.knowledge.reader.wikipedia_reader import WikipediaReader
from agno.vectordb.lightrag import LightRag

vector_db = LightRag(
    api_key=getenv("LIGHTRAG_API_KEY"),
)

knowledge = Knowledge(
    name="My LightRag Knowledge Base",
    description="This is a knowledge base that uses a LightRag Vector DB",
    vector_db=vector_db,
)

agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    read_chat_history=False,
)

if __name__ == "__main__":
    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            path="cookbook/08_knowledge/testing_resources/cv_1.pdf",
            metadata={"doc_type": "recipe_book"},
        )
    )

    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            topics=["Manchester United"],
            reader=WikipediaReader(),
        )
    )

    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            url="https://en.wikipedia.org/wiki/Manchester_United_F.C.",
        )
    )

    asyncio.run(
        agent.aprint_response("What skills does Jordan Mitchell have?", markdown=True)
    )

    asyncio.run(
        agent.aprint_response(
            "In what year did Manchester United change their name?", markdown=True
        )
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U lightrag pypdf openai agno
    ```
  </Step>

  <Step title="Set environment variables">
    ```bash  theme={null}
    export LIGHTRAG_API_KEY="your-lightrag-api-key"
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/lightrag/lightrag.py
    ```
  </Step>
</Steps>
