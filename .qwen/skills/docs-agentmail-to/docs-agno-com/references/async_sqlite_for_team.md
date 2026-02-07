# Async Sqlite for Team

**Source:** https://docs.agno.com/database/providers/async-sqlite/usage/async-sqlite-for-team.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Sqlite for Team

Agno supports using Sqlite asynchronously as a storage backend for Teams, with the `AsyncSqliteDb` class.

## Usage

You need to provide either `db_url`, `db_file` or `db_engine`. The following example uses `db_file`.

```python async_sqlite_for_team.py theme={null}
"""
Run: `uv pip install openai newspaper4k lxml_html_clean agno sqlalchemy aiosqlite` to install the dependencies
"""
import asyncio
from typing import List

from agno.agent import Agent
from agno.db.sqlite import AsyncSqliteDb
from agno.models.openai import OpenAIResponses
from agno.team import Team
from agno.tools.hackernews import HackerNewsTools
from agno.tools.hackernews import HackerNewsTools
from pydantic import BaseModel

# Initialize AsyncSqliteDb with a database file
db = AsyncSqliteDb(db_file="team_storage.db")

class Article(BaseModel):
    title: str
    summary: str
    reference_links: List[str]

hn_researcher = Agent(
    name="HackerNews Researcher",
    model=OpenAIResponses(id="gpt-5.2"),
    role="Gets top stories from hackernews.",
    tools=[HackerNewsTools()],
)

web_searcher = Agent(
    name="Web Searcher",
    model=OpenAIResponses(id="gpt-5.2"),
    role="Searches the web for information on a topic",
    tools=[HackerNewsTools()],
    add_datetime_to_context=True,
)

hn_team = Team(
    name="HackerNews Team",
    model=OpenAIResponses(id="gpt-5.2"),
    members=[hn_researcher, web_searcher],
    db=db,
    instructions=[
        "First, search hackernews for what the user is asking about.",
        "Then, ask the web searcher to search for each story to get more information.",
        "Finally, provide a thoughtful and engaging summary.",
    ],
    output_schema=Article,
    markdown=True,
    show_members_responses=True,
)

asyncio.run(
    hn_team.aprint_response("Write an article about the top 2 stories on hackernews")
)
```

## Params

<Snippet file="db-async-sqlite-params.mdx" />
