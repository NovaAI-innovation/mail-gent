# Async Basic Agent

**Source:** https://docs.agno.com/models/providers/native/xai/usage/basic-async.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Basic Agent

## Code

```python cookbook/11_models/xai/basic_async.py theme={null}
import asyncio

from agno.agent import Agent, RunOutput
from agno.models.xai import xAI

agent = Agent(model=xAI(id="grok-3"), markdown=True)

# Get the response in a variable
# run: RunOutput = agent.run("Share a 2 sentence horror story")
# print(run.content)

# Print the response in the terminal
asyncio.run(agent.aprint_response("Share a 2 sentence horror story"))
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
    python cookbook/11_models/xai/basic_async.py
    ```
  </Step>
</Steps>
