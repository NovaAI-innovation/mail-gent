# Verbosity Control

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/verbosity-control.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Verbosity Control

## Code

```python cookbook/11_models/openai/responses/verbosity_control.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.yfinance import YFinanceTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2", verbosity="high"),
    tools=[
        YFinanceTools(
            stock_price=True,
            analyst_recommendations=True,
            company_info=True,
            company_news=True,
        )
    ],
    instructions="Use tables to display data.",
    markdown=True,
)
agent.print_response("Write a report comparing NVDA to TSLA", stream=True)

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
    python cookbook/11_models/openai/responses/verbosity_control.py
    ```
  </Step>
</Steps>
