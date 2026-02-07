# VoyageAI Embedder

**Source:** https://docs.agno.com/knowledge/concepts/embedder/voyageai/voyageai-embedder.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# VoyageAI Embedder

## Code

```python  theme={null}
from agno.knowledge.embedder.voyageai import VoyageAIEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector

embeddings = VoyageAIEmbedder().get_embedding(
    "The quick brown fox jumps over the lazy dog."
)

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge = Knowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="voyageai_embeddings",
        embedder=VoyageAIEmbedder(),
    ),
    max_results=2,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U sqlalchemy psycopg pgvector voyageai agno
    ```
  </Step>

  <Step title="Run PgVector">
    ```bash  theme={null}
    docker run -d \
      -e POSTGRES_DB=ai \
      -e POSTGRES_USER=ai \
      -e POSTGRES_PASSWORD=ai \
      -e PGDATA=/var/lib/postgresql/data/pgdata \
      -v pgvolume:/var/lib/postgresql/data \
      -p 5532:5432 \
      --name pgvector \
      agnohq/pgvector:16
    ```
  </Step>

  <Step title="Run Agent">
    <CodeGroup>
      ```bash Mac theme={null}
      python cookbook/08_knowledge/embedders/voyageai_embedder.py
      ```

      ```bash Windows theme={null}
      python cookbook/08_knowledge/embedders/voyageai_embedder.py
      ```
    </CodeGroup>
  </Step>
</Steps>
