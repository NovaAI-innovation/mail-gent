# Async Sqlite for Agent

**Source:** https://docs.agno.com/database/providers/async-sqlite/usage/async-sqlite-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Sqlite for Agent

Agno supports using Sqlite asynchronously as a storage backend for Agents, with the `AsyncSqliteDb` class.

## Usage

```python async_sqlite_for_agent.py theme={null}
"""
Run `uv pip install openai sqlalchemy aiosqlite` to install dependencies.
"""
import asyncio

from agno.agent import Agent
from agno.db.sqlite import AsyncSqliteDb
from agno.tools.hackernews import HackerNewsTools

# Initialize AsyncSqliteDb
db = AsyncSqliteDb(db_file="agent_storage.db")

agent = Agent(
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
    add_datetime_to_context=True,
)

asyncio.run(agent.aprint_response("How many people live in Canada?"))
asyncio.run(agent.aprint_response("What is their national anthem called?"))

```

## Params

<Snippet file="db-async-sqlite-params.mdx" />
