# Neo4j

**Source:** https://docs.agno.com/tools/toolkits/database/neo4j.md
**Section:** Docs

**Description:** The Neo4jTools toolkit enables agents to interact with Neo4j graph databases for querying and managing graph data.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Neo4j

> The Neo4jTools toolkit enables agents to interact with Neo4j graph databases for querying and managing graph data.

**Neo4jTools** enables agents to interact with Neo4j graph databases for querying and managing graph data.

## Prerequisites

The following example requires the `neo4j` library.

```shell  theme={null}
uv pip install -U neo4j
```

You will also need a Neo4j database. The following example uses a Neo4j database running in a Docker container.

```shell  theme={null}
docker run -d -p 7474:7474 -p 7687:7687 --name neo4j -e NEO4J_AUTH=neo4j/password neo4j
```

Make sure to set the `NEO4J_URI` environment variable to the URI of the Neo4j database.

```shell  theme={null}
    export NEO4J_URI=bolt://localhost:7687
    export NEO4J_USERNAME=neo4j
    export NEO4J_PASSWORD=your-password
    export OPENAI_API_KEY=xxx
```

Install dependencies

```shell  theme={null}
uv pip install -U neo4j openai agno
```

Run the agent

```shell  theme={null}
python cookbook/14_tools/neo4j_tools.py
```

## Example

The following agent can interact with Neo4j graph databases:

```python  theme={null}
from agno.agent import Agent
from agno.tools.neo4j import Neo4jTools

agent = Agent(
    instructions=[
        "You are a graph database assistant that helps with Neo4j operations",
        "Execute Cypher queries to analyze graph data and relationships",
        "Provide insights about graph structure and patterns",
        "Help with graph data modeling and optimization",
    ],
    tools=[Neo4jTools()],
)

agent.print_response("Show me the schema of the graph database", stream=True)
```

## Toolkit Params

| Parameter                   | Type            | Default | Description                                       |
| --------------------------- | --------------- | ------- | ------------------------------------------------- |
| `uri`                       | `Optional[str]` | `None`  | Neo4j connection URI. Uses NEO4J\_URI if not set. |
| `user`                      | `Optional[str]` | `None`  | Neo4j username. Uses NEO4J\_USERNAME if not set.  |
| `password`                  | `Optional[str]` | `None`  | Neo4j password. Uses NEO4J\_PASSWORD if not set.  |
| `database`                  | `Optional[str]` | `None`  | Specific database name to connect to.             |
| `enable_list_labels`        | `bool`          | `True`  | Enable listing node labels.                       |
| `enable_list_relationships` | `bool`          | `True`  | Enable listing relationship types.                |
| `enable_get_schema`         | `bool`          | `True`  | Enable schema information retrieval.              |
| `enable_run_cypher`         | `bool`          | `True`  | Enable Cypher query execution.                    |

## Toolkit Functions

| Function             | Description                                           |
| -------------------- | ----------------------------------------------------- |
| `list_labels`        | List all node labels in the graph database.           |
| `list_relationships` | List all relationship types in the graph database.    |
| `get_schema`         | Get comprehensive schema information about the graph. |
| `run_cypher`         | Execute Cypher queries on the graph database.         |

## Developer Resources

* View [Tools Source](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/neo4j.py)
* [Neo4j Documentation](https://neo4j.com/docs/)
* [Cypher Query Language](https://neo4j.com/docs/cypher-manual/current/)
