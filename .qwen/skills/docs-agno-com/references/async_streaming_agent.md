# Async Streaming Agent

**Source:** https://docs.agno.com/models/providers/native/xai/usage/basic-async-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Streaming Agent

## Code

```python cookbook/11_models/xai/basic_async_stream.py theme={null}
import asyncio
from typing import Iterator

from agno.agent import Agent, RunOutputEvent
from agno.models.xai import xAI

agent = Agent(model=xAI(id="grok-3"), markdown=True)

# Get the response in a variable
# run_response: Iterator[RunOutputEvent] = agent.run("Share a 2 sentence horror story", stream=True)
# for chunk in run_response:
#     print(chunk.content)

# Print the response in the terminal
asyncio.run(agent.aprint_response("Share a 2 sentence horror story", stream=True))
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
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/xai/basic_async_stream.py
    ```
  </Step>
</Steps>
