# Pinecone Async

**Source:** https://docs.agno.com/knowledge/vector-stores/pinecone/usage/async-pinecone-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Pinecone Async

## Code

```python cookbook/08_knowledge/vector_db/pinecone_db/pinecone_db.py theme={null}
import asyncio
from os import getenv

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pineconedb import PineconeDb

api_key = getenv("PINECONE_API_KEY")
index_name = "thai-recipe-index"

vector_db = PineconeDb(
    name=index_name,
    dimension=1536,
    metric="cosine",
    spec={"serverless": {"cloud": "aws", "region": "us-east-1"}},
    api_key=api_key,
)

knowledge = Knowledge(
    name="My Pinecone Knowledge Base",
    description="This is a knowledge base that uses a Pinecone Vector DB",
    vector_db=vector_db,
)

agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    read_chat_history=True,
)

if __name__ == "__main__":
    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
            metadata={"doc_type": "recipe_book"},
        )
    )

    asyncio.run(
        agent.aprint_response("How do I make pad thai?", markdown=True)
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U pinecone-client pypdf openai agno
    ```
  </Step>

  <Step title="Set environment variables">
    ```bash  theme={null}
    export PINECONE_API_KEY="your-pinecone-api-key"
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/pinecone_db/pinecone_db.py
    ```
  </Step>
</Steps>
