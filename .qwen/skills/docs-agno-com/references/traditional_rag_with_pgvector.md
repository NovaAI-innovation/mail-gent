# Traditional RAG with PgVector

**Source:** https://docs.agno.com/knowledge/agents/traditional-rag-pgvector.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Traditional RAG with PgVector

This example demonstrates traditional RAG implementation using PgVector database with OpenAI embeddings, where knowledge context is automatically added to prompts without search functionality.

## Code

```python traditional_rag_pgvector.py theme={null}
from agno.agent import Agent
from agno.knowledge.embedder.openai import OpenAIEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.models.openai import OpenAIResponses
from agno.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge = Knowledge(
    # Use PgVector as the vector database and store embeddings in the `ai.recipes` table
    vector_db=PgVector(
        table_name="recipes",
        db_url=db_url,
        search_type=SearchType.hybrid,
        embedder=OpenAIEmbedder(id="text-embedding-3-small"),
    ),
)

knowledge.insert(
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"
)

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    knowledge=knowledge,
    # Enable RAG by adding context from the `knowledge` to the user prompt.
    add_knowledge_to_context=True,
    # Set as False because Agents default to `search_knowledge=True`
    search_knowledge=False,
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
    uv pip install -U agno openai sqlalchemy psycopg pgvector
    ```
  </Step>

  <Step title="Setup PgVector">
    Start PostgreSQL with pgvector extension and update the connection string in the code as needed.
  </Step>

  <Step title="Export your OpenAI API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=your_openai_api_key_here
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python traditional_rag_pgvector.py
    ```
  </Step>
</Steps>
