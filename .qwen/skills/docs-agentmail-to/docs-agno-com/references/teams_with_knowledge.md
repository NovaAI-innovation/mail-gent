# Teams with Knowledge

**Source:** https://docs.agno.com/knowledge/teams/overview.md
**Section:** Docs

**Description:** Use knowledge bases with teams.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Teams with Knowledge

> Use knowledge bases with teams.

Teams can use a knowledge base to store and retrieve information, just like agents:

```python  theme={null}
from pathlib import Path

from agno.agent import Agent
from agno.knowledge.embedder.openai import OpenAIEmbedder
from agno.knowledge import Knowledge
from agno.models.openai import OpenAIResponses
from agno.team import Team
from agno.tools.hackernews import HackerNewsTools
from agno.vectordb.lancedb import LanceDb

# Setup paths
cwd = Path(__file__).parent
tmp_dir = cwd.joinpath("tmp")
tmp_dir.mkdir(parents=True, exist_ok=True)

# Initialize knowledge base
agno_docs_knowledge = Knowledge(
    vector_db=LanceDb(
        uri=str(tmp_dir.joinpath("lancedb")),
        table_name="agno_docs",
        embedder=OpenAIEmbedder(id="text-embedding-3-small"),
    ),
)

agno_docs_knowledge.insert(url="https://docs.agno.com/llms-full.txt")

hackernews_agent = Agent(
    name="HackerNews Agent",
    role="Search HackerNews for tech news",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[HackerNewsTools()],
    instructions=["Always include sources"],
)

team_with_knowledge = Team(
    name="Team with Knowledge",
    members=[hackernews_agent],
    model=OpenAIResponses(id="gpt-5.2"),
    knowledge=agno_docs_knowledge,
    show_members_responses=True,
    markdown=True,
)

if __name__ == "__main__":
    team_with_knowledge.print_response("Tell me about the Agno framework", stream=True)
```

See more in the [Knowledge](/knowledge/overview) section.
