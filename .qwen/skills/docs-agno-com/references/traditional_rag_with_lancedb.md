# Traditional RAG with LanceDB

**Source:** https://docs.agno.com/knowledge/agents/traditional-rag-lancedb.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Traditional RAG with LanceDB

This example demonstrates how to implement traditional RAG using LanceDB vector database, where knowledge is added to context rather than searched dynamically by the agent.

## Code

```python traditional_rag_lancedb.py theme={null}
"""
1. Run: `pip install openai lancedb tantivy pypdf sqlalchemy agno` to install the dependencies
2. Run: `python cookbook/rag/03_traditional_rag_lancedb.py` to run the agent
"""

from agno.agent import Agent
from agno.knowledge.embedder.openai import OpenAIEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.models.openai import OpenAIResponses
from agno.vectordb.lancedb import LanceDb, SearchType

knowledge = Knowledge(
    # Use LanceDB as the vector database and store embeddings in the `recipes` table
    vector_db=LanceDb(
        table_name="recipes",
        uri="tmp/lancedb",
        search_type=SearchType.vector,
        embedder=OpenAIEmbedder(id="text-embedding-3-small"),
    ),
)

knowledge.insert(
    name="Recipes",
    url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
)

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    knowledge=knowledge,
    # Enable RAG by adding references from Knowledge to the user prompt.
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
    uv pip install -U agno openai lancedb tantivy pypdf sqlalchemy
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=your_openai_api_key_here
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python traditional_rag_lancedb.py
    ```
  </Step>
</Steps>
