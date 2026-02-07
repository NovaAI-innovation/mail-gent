# Async MySQL

**Source:** https://docs.agno.com/database/providers/async-mysql/overview.md
**Section:** Docs

**Description:** Use MySQL asynchronously for agent session storage.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async MySQL

> Use MySQL asynchronously for agent session storage.

Agno supports using [MySQL](https://www.mysql.com/) asynchronously, with the `AsyncMySQLDb` class.

## Usage

```python async_mysql_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.postgres import AsyncPostgresDb

# Replace with your own connection string, and notice the `async_` prefix
db_url = "postgresql+psycopg_async://ai:ai@localhost:5532/ai"

# Setup your Database
db = AsyncPostgresDb(db_url=db_url)

# Setup your Agent with the Database
agent = Agent(db=db)
```

### Run MySQL

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **MySQL** on port **3306** using:

```bash  theme={null}
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=ai \
  -e MYSQL_DATABASE=ai \
  -e MYSQL_USER=ai \
  -e MYSQL_PASSWORD=ai \
  -p 3306:3306 \
  -d mysql:8
```

## Params

<Snippet file="db-async-postgres-params.mdx" />
