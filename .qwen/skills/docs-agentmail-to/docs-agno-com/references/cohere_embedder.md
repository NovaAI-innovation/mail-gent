# Cohere Embedder

**Source:** https://docs.agno.com/knowledge/concepts/embedder/cohere/cohere-embedder.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Cohere Embedder

## Code

```python  theme={null}
import asyncio
from agno.knowledge.embedder.cohere import CohereEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector

embeddings = CohereEmbedder().get_embedding(
    "The quick brown fox jumps over the lazy dog."
)
# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge = Knowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="cohere_embeddings",
        embedder=CohereEmbedder(
            dimensions=1024,
        ),
    ),
    max_results=2,
)

asyncio.run(
    knowledge.ainsert(
        path="cookbook/08_knowledge/testing_resources/cv_1.pdf",
    )
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export COHERE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U sqlalchemy psycopg pgvector cohere agno
    ```
  </Step>

  <Snippet file="run-pgvector-step.mdx" />

  <Step title="Run Agent">
    <CodeGroup>
      ```bash Mac theme={null}
      python cookbook/08_knowledge/embedders/cohere_embedder.py
      ```

      ```bash Windows theme={null}
      python cookbook/08_knowledge/embedders/cohere_embedder.py
      ```
    </CodeGroup>
  </Step>
</Steps>
