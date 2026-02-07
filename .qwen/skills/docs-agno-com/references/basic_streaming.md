# Basic Streaming

**Source:** https://docs.agno.com/models/providers/cloud/azure-openai/usage/basic-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Basic Streaming

## Code

```python cookbook/11_models/azure/openai/basic_stream.py theme={null}
from typing import Iterator  # noqa

from agno.agent import Agent, RunOutputEvent  # noqa
from agno.models.azure import AzureOpenAI

agent = Agent(model=AzureOpenAI(id="gpt-5-mini"), markdown=True)

# Get the response in a variable
# run_response: Iterator[RunOutputEvent] = agent.run("Share a 2 sentence horror story", stream=True)
# for chunk in run_response:
#     print(chunk.content)

# Print the response on the terminal
agent.print_response("Share a 2 sentence horror story", stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export AZURE_OPENAI_API_KEY=xxx
    export AZURE_OPENAI_ENDPOINT=xxx
    export AZURE_DEPLOYMENT=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/azure/openai/basic_stream.py
    ```
  </Step>
</Steps>
