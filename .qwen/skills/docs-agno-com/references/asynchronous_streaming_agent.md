# Asynchronous Streaming Agent

**Source:** https://docs.agno.com/models/providers/native/meta/usage/async-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Asynchronous Streaming Agent

## Code

```python cookbook/11_models/meta/llama/async_basic_stream.py theme={null}
import asyncio
from typing import Iterator  # noqa

from agno.agent import Agent, RunOutput  # noqa
from agno.models.meta import Llama

agent = Agent(model=Llama(id="Llama-4-Maverick-17B-128E-Instruct-FP8"), markdown=True)

# Get the response in a variable
# run_response: Iterator[RunOutputEvent] = asyncio.run(agent.arun("Share a 2 sentence horror story", stream=True))
# for chunk in run_response:
#     print(chunk.content)

# Print the response in the terminal
asyncio.run(agent.aprint_response("Share a 2 sentence horror story", stream=True))
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
    python cookbook/11_models/meta/async_stream.py
    ```
  </Step>
</Steps>
