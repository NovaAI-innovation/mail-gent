# Db

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/db.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Db

## Code

```python cookbook/11_models/openai/responses/db.py theme={null}
"""Run `uv pip install sqlalchemy openai` to install dependencies."""

from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools

# Setup the database
db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
db = PostgresDb(db_url=db_url)

agent = Agent(
    model=OpenAIResponses(id="gpt-5-mini"),
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
)
agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    <CodeGroup>
      ```bash Mac theme={null}
      python cookbook/11_models/openai/responses/db.py
      ```

      ```bash Windows theme={null}
      python cookbook\models\openai\responses\db.py
      ```
    </CodeGroup>
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/openai/responses/db.py
    ```
  </Step>
</Steps>
