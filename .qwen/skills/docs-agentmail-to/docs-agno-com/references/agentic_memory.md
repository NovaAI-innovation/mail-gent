# Agentic Memory

**Source:** https://docs.agno.com/memory/agent/agentic-memory.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agentic Memory

This example shows you how to use persistent memory with an Agent.

During each run the Agent can create/update/delete user memories.

To enable this, set `enable_agentic_memory=True` in the Agent config.

## Code

```python agentic_memory.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.models.openai import OpenAIResponses
from rich.pretty import pprint

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"

db = PostgresDb(db_url=db_url)


john_doe_id = "john_doe@example.com"

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    db=db,
    enable_agentic_memory=True,
)

agent.print_response(
    "My name is John Doe and I like to hike in the mountains on weekends.",
    stream=True,
    user_id=john_doe_id,
)

agent.print_response("What are my hobbies?", stream=True, user_id=john_doe_id)

memories = agent.get_user_memories(user_id=john_doe_id)
print("Memories about John Doe:")
pprint(memories)


agent.print_response(
    "Remove all existing memories of me.",
    stream=True,
    user_id=john_doe_id,
)

memories = agent.get_user_memories(user_id=john_doe_id)
print("Memories about John Doe:")
pprint(memories)

agent.print_response(
    "My name is John Doe and I like to paint.", stream=True, user_id=john_doe_id
)

memories = agent.get_user_memories(user_id=john_doe_id)
print("Memories about John Doe:")
pprint(memories)


agent.print_response(
    "I don't paint anymore, i draw instead.", stream=True, user_id=john_doe_id
)

memories = agent.get_user_memories(user_id=john_doe_id)

print("Memories about John Doe:")
pprint(memories)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Example">
    ```bash  theme={null}
    python agentic_memory.py
    ```
  </Step>
</Steps>
