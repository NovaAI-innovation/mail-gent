# Agent with Memory

**Source:** https://docs.agno.com/models/providers/native/perplexity/usage/memory.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Memory

## Code

```python cookbook/11_models/perplexity/memory.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.models.perplexity import Perplexity
from rich.pretty import pprint

db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
agent = Agent(
    model=Perplexity(id="sonar-pro"),
    # Store the memories and summary in a database
    db=PostgresDb(db_url=db_url),
    update_memory_on_run=True,
    enable_session_summaries=True,
)

# -*- Share personal information
agent.print_response("My name is john billings?", stream=True)
# -*- Print memories and summary
if agent.db:
    pprint(agent.get_user_memories(user_id="test_user"))
    pprint(
        agent.get_session(session_id="test_session").summary  # type: ignore
    )

# -*- Share personal information
agent.print_response("I live in nyc?", stream=True)
# -*- Print memories and summary
if agent.db:
    pprint(agent.get_user_memories(user_id="test_user"))
    pprint(
        agent.get_session(session_id="test_session").summary  # type: ignore
    )

# -*- Share personal information
agent.print_response("I'm going to a concert tomorrow?", stream=True)
# -*- Print memories and summary
if agent.db:
    pprint(agent.get_user_memories(user_id="test_user"))
    pprint(
        agent.get_session(session_id="test_session").summary  # type: ignore
    )

# Ask about the conversation
agent.print_response(
    "What have we been talking about, do you know my name?", stream=True
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export PERPLEXITY_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai sqlalchemy psycopg pgvector
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/perplexity/memory.py
    ```
  </Step>
</Steps>
