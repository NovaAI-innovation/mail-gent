# Share Memory between Agents

**Source:** https://docs.agno.com/memory/agent/agents-share-memory.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Share Memory between Agents

This example demonstrates how to share memory between Agents.

This means that memories created by one Agent, will be available to the other Agents.

## Code

```python agents_share_memory.py theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools
from rich.pretty import pprint

db = SqliteDb(db_file="agents.db")

john_doe_id = "john_doe@example.com"

chat_agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    description="You are a helpful assistant that can chat with users",
    db=db,
    update_memory_on_run=True,
)

chat_agent.print_response(
    "My name is John Doe and I like to hike in the mountains on weekends.",
    stream=True,
    user_id=john_doe_id,
)

chat_agent.print_response("What are my hobbies?", stream=True, user_id=john_doe_id)


research_agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    description="You are a research assistant that can help users with their research questions",
    tools=[HackerNewsTools()],
    db=db,
    update_memory_on_run=True,
)

research_agent.print_response(
    "I love reading about AI. What are the top stories on Hacker News about AI?",
    stream=True,
    user_id=john_doe_id,
)

memories = research_agent.get_user_memories(user_id=john_doe_id)
print("Memories about John Doe:")
pprint(memories)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai rich
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=your_openai_api_key_here
    ```
  </Step>

  <Step title="Run Example">
    ```bash  theme={null}
    python agents_share_memory.py
    ```
  </Step>
</Steps>
