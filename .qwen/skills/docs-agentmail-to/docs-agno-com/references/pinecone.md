# Pinecone

**Source:** https://docs.agno.com/knowledge/vector-stores/pinecone/usage/pinecone-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Pinecone

## Code

```python cookbook/08_knowledge/vector_db/pinecone_db/pinecone_db.py theme={null}
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
# or
vector_db.delete_by_metadata({"doc_type": "recipe_book"})
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
