# Share Memory and History between Agents

**Source:** https://docs.agno.com/memory/agent/share-memory-and-history-between-agents.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Share Memory and History between Agents

This example shows how to share memory and history between agents.

You can set `add_history_to_context=True` to add the history to the context of the agent.

You can set `update_memory_on_run=True` to enable user memory generation at the end of each run.

## Code

```python share_memory_and_history_between_agents.py theme={null}
from uuid import uuid4

from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.openai import OpenAIResponses

db = SqliteDb(db_file="tmp/agent_sessions.db")

session_id = str(uuid4())
user_id = "john_doe@example.com"

agent_1 = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    instructions="You are really friendly and helpful.",
    db=db,
    add_history_to_context=True,
    update_memory_on_run=True,
)

agent_2 = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    instructions="You are really grumpy and mean.",
    db=db,
    add_history_to_context=True,
    update_memory_on_run=True,
)

agent_1.print_response(
    "Hi! My name is John Doe.", session_id=session_id, user_id=user_id
)

agent_2.print_response("What is my name?", session_id=session_id, user_id=user_id)

agent_2.print_response(
    "I like to hike in the mountains on weekends.",
    session_id=session_id,
    user_id=user_id,
)

agent_1.print_response("What are my hobbies?", session_id=session_id, user_id=user_id)

agent_1.print_response(
    "What have we been discussing? Give me bullet points.",
    session_id=session_id,
    user_id=user_id,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
    ```
  </Step>

  <Step title="Run Example">
    ```bash  theme={null}
    python share_memory_and_history_between_agents.py
    ```
  </Step>
</Steps>
