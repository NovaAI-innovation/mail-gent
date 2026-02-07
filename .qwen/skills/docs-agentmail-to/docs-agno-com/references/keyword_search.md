# Keyword Search

**Source:** https://docs.agno.com/knowledge/concepts/search-and-retrieval/keyword-search.md
**Section:** Docs

**Description:** Find content using exact word and phrase matching.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Keyword Search

> Find content using exact word and phrase matching.

Keyword search finds content by matching exact words and phrases. It uses your database's full-text search capabilities to find documents containing specific terms.

```python  theme={null}
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector, SearchType

knowledge = Knowledge(
    vector_db=PgVector(
        table_name="docs",
        db_url=db_url,
        search_type=SearchType.keyword,
    ),
)
```

## How It Works

1. **Text parsing**: Your query is broken into searchable terms
2. **Index lookup**: The system finds documents containing those terms
3. **Ranking**: Results are ordered by relevance (term frequency, document length, etc.)

When using PgVector, this leverages PostgreSQL's built-in full-text search. Other databases use their native text search capabilities.

## When to Use Keyword Search

| Scenario                     | Why Keyword Search Works                         |
| ---------------------------- | ------------------------------------------------ |
| Searching for specific terms | Exact match on product names, codes, IDs         |
| Error codes and identifiers  | Precise matching without semantic interpretation |
| Technical terminology        | Users know the exact terms to search             |
| Structured data queries      | Matching specific field values                   |

Use **vector search** if users phrase things differently than your docs.
Use **hybrid search** if you want both exact matching and semantic understanding.

## Configuration

### Basic Setup

```python  theme={null}
from agno.vectordb.pgvector import PgVector, SearchType

vector_db = PgVector(
    table_name="docs",
    db_url=db_url,
    search_type=SearchType.keyword,
)
```

### With Reranking

Add a reranker to improve result ordering:

```python  theme={null}
from agno.knowledge.reranker.cohere import CohereReranker

vector_db = PgVector(
    table_name="docs",
    db_url=db_url,
    search_type=SearchType.keyword,
    reranker=CohereReranker(),
)
```

## Example

```python keyword_search.py theme={null}
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.pgvector import PgVector, SearchType

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

knowledge = Knowledge(
    vector_db=PgVector(
        table_name="recipes",
        db_url=db_url,
        search_type=SearchType.keyword,
    ),
)

# Load content
knowledge.insert(
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
)

# Search by exact terms
results = knowledge.search("chicken coconut soup", max_results=5)
for doc in results:
    print(doc.content[:200])
```

## Next Steps

<CardGroup cols={2}>
  <Card title="Hybrid Search" icon="magnifying-glass" href="/knowledge/concepts/search-and-retrieval/hybrid-search">
    Combine keyword search with vector similarity
  </Card>

  <Card title="Vector Search" icon="brain" href="/knowledge/concepts/search-and-retrieval/vector-search">
    Search by semantic meaning
  </Card>
</CardGroup>
