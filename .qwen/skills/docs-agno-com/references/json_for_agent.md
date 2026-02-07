# JSON for Agent

**Source:** https://docs.agno.com/database/providers/json/usage/json-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# JSON for Agent

Agno supports using local JSON files as a storage backend for Agents using the `JsonDb` class.

## Usage

```python json_for_agent.py theme={null}
"""Run `uv pip install openai` to install dependencies."""

from agno.agent import Agent
from agno.db.json import JsonDb
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools

# Setup the JSON database
db = JsonDb(db_path="tmp/json_db")

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
)
agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")
```

## Params

<Snippet file="db-json-params.mdx" />
