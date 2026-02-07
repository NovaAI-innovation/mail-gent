# JSON for Team

**Source:** https://docs.agno.com/database/providers/json/usage/json-for-team.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# JSON for Team

Agno supports using local JSON files as a storage backend for Teams using the `JsonDb` class.

## Usage

```python json_for_team.py theme={null}
"""
Run: `uv pip install openai newspaper4k lxml_html_clean agno` to install the dependencies
"""

from typing import List

from agno.agent import Agent
from agno.db.json import JsonDb
from agno.models.openai import OpenAIResponses
from agno.team import Team
from agno.tools.hackernews import HackerNewsTools
from agno.tools.hackernews import HackerNewsTools
from pydantic import BaseModel

# Setup the JSON database
db = JsonDb(db_path="tmp/json_db")

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

hn_team.print_response("Write an article about the top 2 stories on hackernews")
```

## Params

<Snippet file="db-json-params.mdx" />
