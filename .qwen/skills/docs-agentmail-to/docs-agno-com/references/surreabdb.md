# SurreabDB

**Source:** https://docs.agno.com/database/providers/surrealdb/overview.md
**Section:** Docs

**Description:** Use SurrealDB for agent session storage.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# SurreabDB

> Use SurrealDB for agent session storage.

Agno supports using [SurreabDB](https://surrealdb.com/) as a database with the `SurrealDb` class.

You can get started with SurreabDB following their [documentation](https://surrealdb.com/docs).

Run SurreabDB locally with the following command:

```bash  theme={null}
docker run --rm --pull always -p 8000:8000 surrealdb/surrealdb:latest start --user root --pass root
```

## Usage

```python surrealdb_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.surrealdb import SurrealDb

# SurrealDB connection parameters
SURREALDB_URL = "ws://localhost:8000"
SURREALDB_USER = "root"
SURREALDB_PASSWORD = "root"
SURREALDB_NAMESPACE = "agno"
SURREALDB_DATABASE = "surrealdb_for_agent"

creds = {"username": SURREALDB_USER, "password": SURREALDB_PASSWORD}
db = SurrealDb(None, SURREALDB_URL, creds, SURREALDB_NAMESPACE, SURREALDB_DATABASE)

agent = Agent(db=db)
```

## Params

<Snippet file="db-surrealdb-params.mdx" />
