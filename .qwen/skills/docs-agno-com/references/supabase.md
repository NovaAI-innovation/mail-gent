# Supabase

**Source:** https://docs.agno.com/database/providers/supabase/overview.md
**Section:** Docs

**Description:** Use Supabase PostgreSQL for agent session storage.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Supabase

> Use Supabase PostgreSQL for agent session storage.

Agno supports using [Supabase](https://supabase.com/) with the `PostgresDb` class.

You can get started with Supabase following their [Get Started guide](https://supabase.com/docs/guides/getting-started).

You can read more about the [`PostgresDb` class](/database/providers/postgres/overview) in its section.

## Usage

```python supabase_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from os import getenv

# Get your Supabase project and password
SUPABASE_PROJECT = getenv("SUPABASE_PROJECT")
SUPABASE_PASSWORD = getenv("SUPABASE_PASSWORD")

SUPABASE_DB_URL = (
    f"postgresql://postgres:{SUPABASE_PASSWORD}@db.{SUPABASE_PROJECT}:5432/postgres"
)

# Setup the Supabase database
db = PostgresDb(db_url=SUPABASE_DB_URL)

# Setup your Agent with the Database
agent = Agent(db=db)
```

## Params

<Snippet file="db-postgres-params.mdx" />
