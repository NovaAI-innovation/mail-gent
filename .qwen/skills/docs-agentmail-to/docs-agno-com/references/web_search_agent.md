# Web Search Agent

**Source:** https://docs.agno.com/models/providers/gateways/langdb/usage/tool-use.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Web Search Agent

## Code

```python cookbook/11_models/langdb/web_search.py theme={null}
from agno.agent import Agent
from agno.models.langdb import LangDB
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=LangDB(id="llama3-1-70b-instruct-v1.0"),
    tools=[HackerNewsTools()],
    markdown=True,
)
agent.print_response("Whats happening in France?", stream=True)

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
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/langdb/web_search.py
    ```
  </Step>
</Steps>
