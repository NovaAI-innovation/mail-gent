# Streaming Basic Agent

**Source:** https://docs.agno.com/models/providers/cloud/ibm-watsonx/usage/basic-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Streaming Basic Agent

## Code

```python cookbook/11_models/ibm/watsonx/basic_stream.py theme={null}
from typing import Iterator
from agno.agent import Agent, RunOutput
from agno.models.ibm import WatsonX

agent = Agent(model=WatsonX(id="ibm/granite-20b-code-instruct"), markdown=True)

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
    export IBM_WATSONX_API_KEY=xxx
    export IBM_WATSONX_PROJECT_ID=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ibm-watsonx-ai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ibm/watsonx/basic_stream.py
    ```
  </Step>
</Steps>

This example shows how to use streaming with IBM WatsonX. Setting `stream=True` when calling `print_response()` or `run()` enables token-by-token streaming, which can provide a more interactive user experience.
