# Weaviate Async

**Source:** https://docs.agno.com/knowledge/vector-stores/weaviate/usage/async-weaviate-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Weaviate Async

## Code

```python cookbook/08_knowledge/vector_db/weaviate_db/async_weaviate_db.py theme={null}

import asyncio

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.search import SearchType
from agno.vectordb.weaviate import Distance, VectorIndex, Weaviate

vector_db = Weaviate(
    collection="recipes_async",
    search_type=SearchType.hybrid,
    vector_index=VectorIndex.HNSW,
    distance=Distance.COSINE,
    local=True,  # Set to False if using Weaviate Cloud and True if using local instance
)
# Create knowledge base
knowledge = Knowledge(
    vector_db=vector_db,
)

agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
)

if __name__ == "__main__":
    # Comment out after first run
    asyncio.run(
        knowledge.ainsert(
            name="Recipes",
            url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
        )
    )

    # Create and use the agent
    asyncio.run(agent.aprint_response("How to make Tom Kha Gai", markdown=True))
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U weaviate-client pypdf openai agno
    ```
  </Step>

  <Step title="Set environment variables">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Setup Weaviate">
    <CodeGroup>
      ```bash Weaviate Cloud theme={null}
      # 1. Create account at https://console.weaviate.cloud/
      # 2. Create a cluster and copy the "REST endpoint" and "Admin" API Key
      # 3. Set environment variables:
      export WCD_URL="your-cluster-url"
      export WCD_API_KEY="your-api-key"
      # 4. Set local=False in the code
      ```

      ```bash Local Development theme={null}
      # 1. Install Docker from https://docs.docker.com/get-docker/
      # 2. Run Weaviate locally:
      docker run -d \
          -p 8080:8080 \
          -p 50051:50051 \
          --name weaviate \
          cr.weaviate.io/semitechnologies/weaviate:1.28.4
      # 3. Set local=True in the code
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/weaviate_db/async_weaviate_db.py
    ```
  </Step>
</Steps>
