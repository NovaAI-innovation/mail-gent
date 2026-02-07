# Postgres for Agent

**Source:** https://docs.agno.com/database/providers/postgres/usage/postgres-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Postgres for Agent

Agno supports using PostgreSQL as a storage backend for Agents using the `PostgresDb` class.

## Usage

### Run PgVector

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **PgVector** on port **5532** using:

```bash  theme={null}
docker run -d \
  -e POSTGRES_DB=ai \
  -e POSTGRES_USER=ai \
  -e POSTGRES_PASSWORD=ai \
  -e PGDATA=/var/lib/postgresql/data/pgdata \
  -v pgvolume:/var/lib/postgresql/data \
  -p 5532:5432 \
  --name pgvector \
  agnohq/pgvector:16
```

```python postgres_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.tools.hackernews import HackerNewsTools

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

db = PostgresDb(db_url=db_url)

agent = Agent(
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
)
agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")

```

## Params

<Snippet file="db-postgres-params.mdx" />
