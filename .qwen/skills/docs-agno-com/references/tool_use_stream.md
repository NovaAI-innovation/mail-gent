# Tool Use Stream

**Source:** https://docs.agno.com/models/providers/native/xai/usage/tool-use-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Tool Use Stream

## Code

```python cookbook/11_models/xai/tool_use_stream.py theme={null}
"""Build a Web Search Agent using xAI."""

from agno.agent import Agent
from agno.models.xai import xAI
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=xAI(id="grok-2"),
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
    python cookbook/11_models/xai/tool_use_stream.py
    ```
  </Step>
</Steps>
