# Data Analyst Agent

**Source:** https://docs.agno.com/models/providers/gateways/langdb/usage/data-analyst.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Data Analyst Agent

## Code

```python cookbook/11_models/langdb/data_analyst.py theme={null}
from textwrap import dedent

from agno.agent import Agent
from agno.models.langdb import LangDB
from agno.tools.duckdb import DuckDbTools

duckdb_tools = DuckDbTools(
    create_tables=False, export_tables=False, summarize_tables=False
)
duckdb_tools.create_table_from_path(
    path="https://phidata-public.s3.amazonaws.com/demo_data/IMDB-Movie-Data.csv",
    table="movies",
)

agent = Agent(
    model=LangDB(id="llama3-1-70b-instruct-v1.0"),
    tools=[duckdb_tools],
    markdown=True,
    additional_context=dedent("""\
    You have access to the following tables:
    - movies: contains information about movies from IMDB.
    """),
)
agent.print_response("What is the average rating of movies?", stream=False)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export LANGDB_API_KEY=xxx
    export LANGDB_PROJECT_ID=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno duckdb
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/langdb/data_analyst.py
    ```
  </Step>
</Steps>
