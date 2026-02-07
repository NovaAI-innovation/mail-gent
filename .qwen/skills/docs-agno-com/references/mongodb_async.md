# MongoDB Async

**Source:** https://docs.agno.com/knowledge/vector-stores/mongodb/usage/async-mongo-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# MongoDB Async

## Code

```python cookbook/08_knowledge/vector_db/mongo_db/async_mongo_db.py theme={null}

import asyncio

from agno.agent import Agent
from agno.knowledge.knowledge import Knowledge
from agno.vectordb.mongodb import MongoVectorDb

mdb_connection_string = "mongodb://localhost:27017"

knowledge = Knowledge(
    vector_db=MongoVectorDb(
        collection_name="recipes",
        db_url=mdb_connection_string,
    ),
)

agent = Agent(knowledge=knowledge)

if __name__ == "__main__":
    asyncio.run(
        knowledge.ainsert(
            url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"
        )
    )

    asyncio.run(agent.aprint_response("How to make Thai curry?", markdown=True))
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U pymongo pypdf openai agno
    ```
  </Step>

  <Step title="Run MongoDB">
    ```bash  theme={null}
    docker run -d \
    --name local-mongo \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
    -e MONGO_INITDB_ROOT_PASSWORD=secret \
    mongo
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/mongo_db/async_mongo_db.py
    ```
  </Step>
</Steps>
