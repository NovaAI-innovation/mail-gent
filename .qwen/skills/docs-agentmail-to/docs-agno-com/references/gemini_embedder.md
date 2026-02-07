# Gemini Embedder

**Source:** https://docs.agno.com/knowledge/concepts/embedder/gemini/gemini-embedder.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Gemini Embedder

## Code

```python  theme={null}
from agno.knowledge.embedder.google import GeminiEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector

embeddings = GeminiEmbedder().get_embedding(
    "The quick brown fox jumps over the lazy dog."
)

# Print the embeddings and their dimensions
print(f"Embeddings: {embeddings[:5]}")
print(f"Dimensions: {len(embeddings)}")

# Example usage:
knowledge = Knowledge(
    vector_db=PgVector(
        db_url="postgresql+psycopg://ai:ai@localhost:5532/ai",
        table_name="gemini_embeddings",
        embedder=GeminiEmbedder(),
    ),
    max_results=2,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GOOGLE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U sqlalchemy psycopg pgvector google-generativeai agno
    ```
  </Step>

  <Snippet file="run-pgvector-step.mdx" />

  <Step title="Run Agent">
    <CodeGroup>
      ```bash Mac theme={null}
      python cookbook/08_knowledge/embedders/gemini_embedder.py
      ```

      ```bash Windows theme={null}
      python cookbook/08_knowledge/embedders/gemini_embedder.py
      ```
    </CodeGroup>
  </Step>
</Steps>
