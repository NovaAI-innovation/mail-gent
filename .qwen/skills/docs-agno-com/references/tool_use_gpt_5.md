# Tool Use Gpt 5

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/tool-use-gpt-5.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Tool Use Gpt 5

## Code

```python cookbook/11_models/openai/responses/tool_use_gpt_5.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.yfinance import YFinanceTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5"),
    tools=[YFinanceTools(cache_results=True)],
    markdown=True,
    telemetry=False,
)

agent.print_response("What is the current price of TSLA?", stream=True)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/openai/responses/tool_use_gpt_5.py
    ```
  </Step>
</Steps>
