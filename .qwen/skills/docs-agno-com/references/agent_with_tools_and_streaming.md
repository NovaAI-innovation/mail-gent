# Agent with Tools and Streaming

**Source:** https://docs.agno.com/models/providers/gateways/portkey/usage/tool-use-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Tools and Streaming

## Code

```python cookbook/11_models/portkey/tool_use_stream.py theme={null}
from agno.agent import Agent
from agno.models.portkey import Portkey
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=Portkey(id="@first-integrati-707071/gpt-5-nano"),
    tools=[HackerNewsTools()],
    markdown=True,
)

# Print the response in the terminal
agent.print_response("What are the latest developments in AI gateways?", stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API keys">
    ```bash  theme={null}
    export PORTKEY_API_KEY=***
    export PORTKEY_VIRTUAL_KEY=***
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/portkey/tool_use_stream.py
    ```
  </Step>
</Steps>
