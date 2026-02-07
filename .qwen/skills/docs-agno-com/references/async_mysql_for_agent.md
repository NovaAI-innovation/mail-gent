# Async MySQL for Agent

**Source:** https://docs.agno.com/database/providers/async-mysql/usage/async-mysql-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async MySQL for Agent

Agno supports using [MySQL](https://www.mysql.com/) asynchronously, with the `AsyncMySQLDb` class.

## Usage

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

```python async_mysql_for_agent.py theme={null}
import asyncio
import uuid

from agno.agent import Agent
from agno.db.base import SessionType
from agno.db.mysql import AsyncMySQLDb
from agno.tools.hackernews import HackerNewsTools

db_url = "mysql+asyncmy://ai:ai@localhost:3306/ai"
db = AsyncMySQLDb(db_url=db_url)

agent = Agent(
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
    add_datetime_to_context=True,
)

async def main():
    """Run the agent queries in the same event loop"""
    session_id = str(uuid.uuid4())
    await agent.aprint_response(
        "How many people live in Canada?", session_id=session_id
    )
    await agent.aprint_response(
        "What is their national anthem called?", session_id=session_id
    )
    session_data = await db.get_session(
        session_id=session_id, session_type=SessionType.AGENT
    )
    print("\n=== SESSION DATA ===")
    print(session_data.to_dict())

if __name__ == "__main__":
    asyncio.run(main())
```

## Params

<Snippet file="db-async-mysql-params.mdx" />
