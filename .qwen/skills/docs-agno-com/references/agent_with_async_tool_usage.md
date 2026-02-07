# Agent with Async Tool Usage

**Source:** https://docs.agno.com/models/providers/native/meta/usage/async-tool-use.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Async Tool Usage

## Code

```python cookbook/11_models/meta/llama/async_tool_use.py theme={null}
"""Run `uv pip install agno llama-api-client` to install dependencies."""

import asyncio

from agno.agent import Agent
from agno.models.meta import Llama
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=Llama(id="Llama-4-Maverick-17B-128E-Instruct-FP8"),
    tools=[HackerNewsTools()],
    debug_mode=True,
)
asyncio.run(agent.aprint_response("Whats happening in UK and in USA?"))
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your LLAMA API key">
    ```bash  theme={null}
    export LLAMA_API_KEY=YOUR_API_KEY
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install llama-api-client agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/meta/async_tool_use.py
    ```
  </Step>
</Steps>
