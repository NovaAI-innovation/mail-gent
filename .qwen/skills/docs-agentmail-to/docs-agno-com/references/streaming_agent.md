# Streaming Agent

**Source:** https://docs.agno.com/models/providers/native/vercel/usage/basic-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Streaming Agent

## Code

```python cookbook/11_models/vercel/basic_stream.py theme={null}
from typing import Iterator  # noqa
from agno.agent import Agent, RunOutput  # noqa
from agno.models.vercel import V0

agent = Agent(model=V0(id="v0-1.0-md"), markdown=True)

# Get the response in a variable
# run_response: Iterator[RunOutputEvent] = agent.run("Share a 2 sentence horror story", stream=True)
# for chunk in run_response:
#     print(chunk.content)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story", stream=True)
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
    python cookbook/11_models/vercel/basic_stream.py
    ```
  </Step>
</Steps>
