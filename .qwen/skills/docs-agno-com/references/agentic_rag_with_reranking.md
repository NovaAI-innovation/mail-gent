# Agentic RAG with Reranking

**Source:** https://docs.agno.com/knowledge/concepts/search-and-retrieval/agentic-rag.md
**Section:** Docs

**Description:** Combine agentic search, hybrid retrieval, and reranking for high-quality responses.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agentic RAG with Reranking

> Combine agentic search, hybrid retrieval, and reranking for high-quality responses.

This example combines three techniques for optimal retrieval:

1. **Agentic RAG**: Agent decides when to search the knowledge base
2. **Hybrid search**: Combines vector similarity with keyword matching
3. **Reranking**: Reorders results using a dedicated ranking model

```python  theme={null}
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.knowledge.embedder.cohere import CohereEmbedder
from agno.knowledge.reranker.cohere import CohereReranker
from agno.models.anthropic import Claude
from agno.vectordb.lancedb import LanceDb, SearchType

knowledge = Knowledge(
    vector_db=LanceDb(
        uri="tmp/lancedb",
        table_name="docs",
        search_type=SearchType.hybrid,
        embedder=CohereEmbedder(id="embed-v4.0"),
        reranker=CohereReranker(model="rerank-v3.5"),
    ),
)

agent = Agent(
    model=Claude(id="claude-sonnet-4-5"),
    knowledge=knowledge,
    search_knowledge=True,
)
```

## Why Combine These Techniques

| Technique     | What It Does                                             |
| ------------- | -------------------------------------------------------- |
| Agentic RAG   | Agent searches only when needed, can reformulate queries |
| Hybrid search | Catches both semantic matches and exact terms            |
| Reranking     | Uses a dedicated model to reorder results by relevance   |

Together, these provide better retrieval accuracy than any single technique alone.

## How Reranking Works

After hybrid search returns initial results, the reranker:

1. Takes the query and candidate documents
2. Scores each document for relevance using a cross-encoder model
3. Reorders results so the most relevant appear first

Cohere's `rerank-v3.5` is trained specifically for this task and significantly improves result quality.

## Example

```python agentic_rag.py theme={null}
import asyncio

from agno.agent import Agent
from agno.knowledge.embedder.cohere import CohereEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.knowledge.reranker.cohere import CohereReranker
from agno.models.anthropic import Claude
from agno.vectordb.lancedb import LanceDb, SearchType

# Create knowledge base with hybrid search and reranking
knowledge = Knowledge(
    vector_db=LanceDb(
        uri="tmp/lancedb",
        table_name="agno_docs",
        search_type=SearchType.hybrid,
        embedder=CohereEmbedder(id="embed-v4.0"),
        reranker=CohereReranker(model="rerank-v3.5"),
    ),
)

# Load content
asyncio.run(
    knowledge.ainsert(url="https://docs.agno.com/introduction/agents.md")
)

# Create agent with knowledge
agent = Agent(
    model=Claude(id="claude-sonnet-4-20250514"),
    knowledge=knowledge,
    search_knowledge=True,
    instructions=[
        "Search your knowledge before answering.",
        "Include sources in your response.",
    ],
    markdown=True,
)

agent.print_response("What are Agents?", stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno anthropic cohere lancedb tantivy sqlalchemy
    ```
  </Step>

  <Step title="Export your API keys">
    ```bash  theme={null}
    export ANTHROPIC_API_KEY=your_anthropic_api_key_here
    export CO_API_KEY=your_cohere_api_key_here
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python agentic_rag.py
    ```
  </Step>
</Steps>

## Configuration Options

### Different Rerankers

```python  theme={null}
# Cohere
from agno.knowledge.reranker.cohere import CohereReranker
reranker = CohereReranker(model="rerank-v3.5")

# Add to vector database
vector_db = LanceDb(
    uri="tmp/lancedb",
    table_name="docs",
    search_type=SearchType.hybrid,
    reranker=reranker,
)
```

### Adjusting Results

```python  theme={null}
knowledge = Knowledge(
    vector_db=vector_db,
    max_results=10,  # Number of results to return after reranking
)
```

## Next Steps

<CardGroup cols={2}>
  <Card title="Hybrid Search" icon="magnifying-glass" href="/knowledge/concepts/search-and-retrieval/hybrid-search">
    Learn more about combining search types
  </Card>

  <Card title="Embedders" icon="code" href="/knowledge/concepts/embedder/overview">
    Choose the right embedding model
  </Card>
</CardGroup>
