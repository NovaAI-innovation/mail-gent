# Cassandra Async

**Source:** https://docs.agno.com/knowledge/vector-stores/cassandra/usage/async-cassandra-db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Cassandra Async

## Code

```python cookbook/08_knowledge/vector_db/cassandra_db/async_cassandra_db.py theme={null}
import asyncio

from agno.agent import Agent
from agno.knowledge.embedder.mistral import MistralEmbedder
from agno.knowledge.knowledge import Knowledge
from agno.models.mistral import MistralChat
from agno.vectordb.cassandra import Cassandra

try:
    from cassandra.cluster import Cluster  # type: ignore
except (ImportError, ModuleNotFoundError):
    raise ImportError(
        "Could not import cassandra-driver python package.Please install it with pip install cassandra-driver."
    )

cluster = Cluster()

session = cluster.connect()
session.execute(
    """
    CREATE KEYSPACE IF NOT EXISTS testkeyspace
    WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1 }
    """
)

knowledge = Knowledge(
    vector_db=Cassandra(
        table_name="recipes",
        keyspace="testkeyspace",
        session=session,
        embedder=MistralEmbedder(),
    ),
)

agent = Agent(
    model=MistralChat(),
    knowledge=knowledge,
)

if __name__ == "__main__":
    asyncio.run(
        knowledge.insert(url="https://docs.agno.com/introduction/agents.md")
    )

    asyncio.run(
        agent.aprint_response(
            "What is the purpose of an Agno Agent?",
            markdown=True,
        )
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U cassandra-driver pypdf mistralai agno
    ```
  </Step>

  <Step title="Run Cassandra">
    ```bash  theme={null}
    docker run -d \
    --name cassandra-db \
    -p 9042:9042 \
    cassandra:latest
    ```
  </Step>

  <Step title="Set environment variables">
    ```bash  theme={null}
    export CASSANDRA_HOST="localhost"
    export CASSANDRA_PORT="9042"
    export CASSANDRA_USER="cassandra"
    export CASSANDRA_PASSWORD="cassandra"
    export MISTRAL_API_KEY="your-mistral-api-key"
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/08_knowledge/vector_db/cassandra_db/async_cassandra_db.py
    ```
  </Step>
</Steps>
