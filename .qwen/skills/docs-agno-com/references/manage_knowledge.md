# Manage Knowledge

**Source:** https://docs.agno.com/agent-os/knowledge/manage-knowledge.md
**Section:** Docs

**Description:** Attach Knowledge to your AgentOS instance

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Manage Knowledge

> Attach Knowledge to your AgentOS instance

The AgentOS control plane provides a simple way to [manage](/agent-os/features/knowledge-management#adding-content) your Knowledge bases.
You can add, edit, and delete content from your Knowledge bases directly through the control plane.

You can specify multiple Knowledge bases and reuse the same Knowledge instance
across different Agents or Teams as needed.

## Prerequisites

Before setting up Knowledge management in AgentOS, ensure you have:

* PostgreSQL database running and accessible - used for this example
* Required dependencies installed: `uv pip install agno`
* OpenAI API key configured (for embeddings)
* Basic understanding of [Knowledge concepts](/knowledge/quickstart)

## Example

This example demonstrates how to attach multiple Knowledge bases to AgentOS
and populate them with content from different sources.

```python agentos_knowledge.py theme={null}
from textwrap import dedent

from agno.db.postgres import PostgresDb
from agno.knowledge.embedder.openai import OpenAIEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.os import AgentOS
from agno.vectordb.pgvector import PgVector, SearchType

# ************* Setup Knowledge Databases *************
db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
documents_db = PostgresDb(
    db_url,
    id="agno_knowledge_db",
    knowledge_table="agno_knowledge_contents",
)
faq_db = PostgresDb(
    db_url,
    id="agno_faq_db",
    knowledge_table="agno_faq_contents",
)
# *******************************

documents_knowledge = Knowledge(
    vector_db=PgVector(
        db_url=db_url,
        table_name="agno_knowledge_vectors",
        search_type=SearchType.hybrid,
        embedder=OpenAIEmbedder(id="text-embedding-3-small"),
    ),
    contents_db=documents_db,
)

faq_knowledge = Knowledge(
    vector_db=PgVector(
        db_url=db_url,
        table_name="agno_faq_vectors",
        search_type=SearchType.hybrid,
        embedder=OpenAIEmbedder(id="text-embedding-3-small"),
    ),
    contents_db=faq_db,
)

agent_os = AgentOS(
    description="Example app with AgentOS Knowledge",
    # Add the knowledge bases to AgentOS
    knowledge=[documents_knowledge, faq_knowledge],
)


app = agent_os.get_app()

if __name__ == "__main__":
    documents_knowledge.insert(
        name="Agno Docs", url="https://docs.agno.com/llms-full.txt", skip_if_exists=True
    )
    faq_knowledge.insert(
        name="Agno FAQ",
        text_content=dedent("""
            What is Agno?
            Agno is a framework for building agents.
            Use it to build multi-agent systems with memory, knowledge,
            human in the loop and MCP support.
        """),
        skip_if_exists=True,
    )
    # Run your AgentOS
    # You can test your AgentOS at: http://localhost:7777/

    agent_os.serve(app="agentos_knowledge:app")
```

### Screenshots

The screenshots below show how you can access and manage your different Knowledge bases through the AgentOS interface:

<img src="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=b7def1bd459cf44ad505591fedb7d93c" alt="llm-app-aidev-run" data-og-width="3410" width="3410" data-og-height="750" height="750" data-path="images/agno_knowledge_db.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=280&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=b02fe247caf52bf3310f81e19105931b 280w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=560&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=df11d1e81ef31de6d46b3de5c334f034 560w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=840&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=f7021b623fbd594644013584a2b5ea56 840w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=1100&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=0be43fd4bb82c7e7b75eee78e4ebd368 1100w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=1650&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=11a7b25ddec1e72e4067f77e7680f560 1650w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_knowledge_db.png?w=2500&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=81db8b378f9fd4199322ac18b4a77316 2500w" />

<img src="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=e0b00d9eaa45fa729acfea31f4c999e3" alt="llm-app-aidev-run" data-og-width="3410" width="3410" data-og-height="750" height="750" data-path="images/agno_faq_db.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=280&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=033bd66a43bdb037f81a8d4a4c545f23 280w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=560&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=0359a858a41e5a6adce873d020b9052c 560w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=840&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=1a448a117b5799486749736564ee7ec5 840w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=1100&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=3553a6cee69b421fbb876ba5298d30c0 1100w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=1650&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=b52a97309c4de3ed6ccf273fca09a4d5 1650w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agno_faq_db.png?w=2500&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=b026a900809300e55ce4f64e28d688d2 2500w" />

## Best Practices

* **Separate Knowledge by Domain**: Create separate Knowledge bases for different topics (e.g., technical docs, FAQs, policies)
* **Consistent Naming**: Use descriptive names for your Knowledge bases that reflect their content
* **Regular Updates**: Keep your Knowledge bases current by regularly adding new content and removing outdated information
* **Monitor Performance**: Use different table names for vector storage to avoid conflicts
* **Content Organization**: Use the `name` parameter when adding content to make it easily identifiable
* **Use metadata for filtering and searching**: Add metadata to your content to make it easier to find and filter

## Troubleshooting

<AccordionGroup>
  <Accordion title="Knowledge base not appearing in AgentOS interface">
    Ensure your knowledge base is properly added to the `knowledge` parameter when creating your AgentOS instance.
    Also make sure to attach a `contents_db` to your Knowledge instance.
  </Accordion>

  <Accordion title="Database connection errors">
    Verify your PostgreSQL connection string and ensure the database is running and accessible.
  </Accordion>

  <Accordion title="Content not being found in searches">
    Check that your content has been properly embedded by verifying entries in your vector database table.
  </Accordion>
</AccordionGroup>
