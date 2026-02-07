# Async Agent with Tools

**Source:** https://docs.agno.com/models/providers/native/mistral/usage/async-tool-use.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Agent with Tools

## Code

```python cookbook/11_models/mistral/async_tool_use.py theme={null}
import asyncio

from agno.agent import Agent
from agno.models.mistral.mistral import MistralChat
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=MistralChat(id="mistral-large-latest"),
    tools=[HackerNewsTools()],
    markdown=True,
)

asyncio.run(agent.aprint_response("Whats happening in France?", stream=True))

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export MISTRAL_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U mistralai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/mistral/async_tool_use.py
    ```
  </Step>
</Steps>
