# Filtering

**Source:** https://docs.agno.com/knowledge/concepts/filters/overview.md
**Section:** Docs

**Description:** Filter knowledge searches by metadata for precise retrieval.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Filtering

> Filter knowledge searches by metadata for precise retrieval.

Filters restrict knowledge searches to documents matching specific criteria. Attach metadata when adding content, then filter by that metadata when searching.

```python  theme={null}
from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge

# Add content with metadata
knowledge.insert(
    path="resumes/",
    metadata={"user_id": "jordan_mitchell", "document_type": "cv", "year": 2025}
)

# Search with filters
agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    knowledge_filters={"user_id": "jordan_mitchell"},
)
```

## Why Use Filters

* **Personalization**: Retrieve documents for a specific user or group
* **Access control**: Restrict searches to authorized content
* **Precision**: Reduce noise by narrowing results to relevant documents

## Manual Filtering

Pass filters explicitly when creating the agent or searching:

```python  theme={null}
# Filter at agent level
agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    knowledge_filters={"user_id": "jordan_mitchell"},
)

# Filter at query time
agent.print_response(
    "What are Jordan's skills?",
    knowledge_filters={"document_type": "cv"}
)

# Direct search with filters
results = knowledge.search(
    query="programming experience",
    filters={"user_id": "jordan_mitchell", "year": 2025}
)
```

Multiple filters are combined with AND logic.

## Agentic Filtering

Let the agent extract filters automatically from the query. The agent analyzes the user's question and determines which filters to apply.

```python  theme={null}
agent = Agent(
    knowledge=knowledge,
    search_knowledge=True,
    enable_agentic_knowledge_filters=True,  # Agent infers filters from query
)

# Agent extracts "jordan_mitchell" as user filter from the query
agent.print_response("What skills does Jordan Mitchell have?")
```

This requires a [Contents DB](/knowledge/concepts/contents-db) to track available filter keys.

## Manual vs Agentic Filtering

| Approach | When to Use                                   |
| -------- | --------------------------------------------- |
| Manual   | Automation, predictable filters, full control |
| Agentic  | User-facing apps, natural language queries    |

## Traditional vs Agentic RAG

Filters work with both RAG approaches:

<Tabs>
  <Tab title="Agentic RAG">
    ```python  theme={null}
    # Agent decides when to search (default)
    agent = Agent(
        knowledge=knowledge,
        search_knowledge=True,
        knowledge_filters={"user_id": "jordan_mitchell"},
    )
    ```
  </Tab>

  <Tab title="Traditional RAG">
    ```python  theme={null}
    # Always inject context into prompt
    agent = Agent(
        knowledge=knowledge,
        search_knowledge=False,
        add_knowledge_to_context=True,
        knowledge_filters={"user_id": "jordan_mitchell"},
    )
    ```
  </Tab>
</Tabs>

Use one approach at a time. Agentic RAG (`search_knowledge=True`) is recommended for most use cases.

## Metadata Design

Good metadata enables effective filtering:

```python  theme={null}
# Rich, filterable metadata
metadata = {
    "user_id": "jordan_mitchell",
    "document_type": "cv",
    "department": "engineering",
    "year": 2025,
    "access_level": "internal",
}

# Add with content
knowledge.insert(path="resume.pdf", metadata=metadata)
```

**Tips:**

* Use consistent values (always `"engineering"`, not sometimes `"eng"`)
* Include temporal data for time-based filtering
* Add access levels for permission-based filtering

## Supported Vector Databases

Filtering is supported on:

* ChromaDB
* LanceDB
* Milvus
* MongoDB
* PgVector
* Pinecone
* Qdrant
* Weaviate

## Next Steps

<CardGroup cols={2}>
  <Card title="Advanced Filtering" icon="filter" href="/knowledge/concepts/filters/advanced-filtering">
    Complex filters with OR, NOT, and comparisons
  </Card>

  <Card title="Content DB" icon="database" href="/knowledge/concepts/contents-db">
    Required for agentic filtering
  </Card>

  <Card title="Search & Retrieval" icon="magnifying-glass" href="/knowledge/concepts/search-and-retrieval/overview">
    How filtering affects search
  </Card>
</CardGroup>
