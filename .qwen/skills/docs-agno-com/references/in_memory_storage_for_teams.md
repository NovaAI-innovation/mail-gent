# In-Memory Storage for Teams

**Source:** https://docs.agno.com/database/providers/in-memory/usage/in-memory-for-team.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# In-Memory Storage for Teams

Example using `InMemoryDb` with teams for multi-agent coordination.

## Usage

```python  theme={null}
from agno.agent import Agent
from agno.db.in_memory import InMemoryDb
from agno.models.openai import OpenAIResponses
from agno.team import Team
from agno.tools.hackernews import HackerNewsTools
from agno.tools.hackernews import HackerNewsTools

# Create team members
hn_researcher = Agent(
    name="HackerNews Researcher",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[HackerNewsTools()],
)

web_searcher = Agent(
    name="Web Searcher",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[HackerNewsTools()],
)

# Setup team with in-memory database
db = InMemoryDb()
team = Team(
    name="Research Team",
    members=[hn_researcher, web_searcher],
    db=db,
)

team.print_response("Find top AI news")
```
