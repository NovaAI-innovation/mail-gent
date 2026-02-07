# Agent with Tools

**Source:** https://docs.agno.com/models/providers/native/vercel/usage/tool-use.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Tools

## Code

```python cookbook/11_models/vercel/tool_use.py theme={null}
from agno.agent import Agent
from agno.models.vercel import V0
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=V0(id="v0-1.0-md"),
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
    export V0_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/vercel/tool_use.py
    ```
  </Step>
</Steps>
