# PostgreSQL

**Source:** https://docs.agno.com/database/providers/postgres/overview.md
**Section:** Docs

**Description:** Use PostgreSQL for agent session storage and persistence.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# PostgreSQL

> Use PostgreSQL for agent session storage and persistence.

Agno supports using [PostgreSQL](https://www.postgresql.org/) as a database with the `PostgresDb` class.

## Usage

```python postgres_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai" # Replace with your own connection string

# Setup your Database
db = PostgresDb(db_url=db_url)

# Setup your Agent with the Database
agent = Agent(db=db)
```

### Run Postgres (with PgVector)

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

## Params

<Snippet file="db-postgres-params.mdx" />
