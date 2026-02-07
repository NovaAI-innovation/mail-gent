# Live Search Agent

**Source:** https://docs.agno.com/models/providers/native/xai/usage/live-search-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Live Search Agent

## Code

```python cookbook/11_models/xai/live_search_agent.py theme={null}
from agno.agent import Agent
from agno.models.xai.xai import xAI

agent = Agent(
    model=xAI(
        id="grok-3",
        search_parameters={
            "mode": "on",
            "max_search_results": 20,
            "return_citations": True,
        },
    ),
    markdown=True,
)
agent.print_response("Provide me a digest of world news in the last 24 hours.")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export XAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U xai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/xai/live_search_agent.py
    ```
  </Step>
</Steps>
