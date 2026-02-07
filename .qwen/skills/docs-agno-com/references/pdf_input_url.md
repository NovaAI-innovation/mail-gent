# Pdf Input Url

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/pdf-input-url.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Pdf Input Url

## Code

```python cookbook/11_models/openai/responses/pdf_input_url.py theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.media import File
from agno.models.openai.responses import OpenAIResponses

# Setup the database for the Agent Session to be stored
db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
db = PostgresDb(db_url=db_url)

agent = Agent(
    model=OpenAIResponses(id="gpt-5-mini"),
    db=db,
    tools=[{"type": "file_search"}, {"type": "web_search_preview"}],
    markdown=True,
)

agent.print_response(
    "Summarize the contents of the attached file and search the web for more information.",
    files=[File(url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf")],
)

# Get the stored Agent session, to check the response citations
session = agent.get_session()
if session and session.runs and session.runs[-1].citations:
    print("Citations:")
    print(session.runs[-1].citations)

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
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/openai/responses/pdf_input_url.py
    ```
  </Step>
</Steps>
