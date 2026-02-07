# ZDR Reasoning Agent

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/zdr-reasoning-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# ZDR Reasoning Agent

## Code

```python cookbook/11_models/openai/responses/zdr_reasoning_agent.py theme={null}
"""
An example of using OpenAI Responses with reasoning features and ZDR mode enabled.

Read more about ZDR mode here: https://openai.com/enterprise-privacy/.
"""

from agno.agent import Agent
from agno.db.in_memory import InMemoryDb
from agno.models.openai import OpenAIResponses

agent = Agent(
    name="ZDR Compliant Agent",
    session_id="zdr_demo_session",
    model=OpenAIResponses(
        id="o4-mini",
        store=False,
        reasoning_summary="auto",  # Requesting a reasoning summary
    ),
    instructions="You are a helpful AI assistant operating in Zero Data Retention mode for maximum privacy and compliance.",
    db=InMemoryDb(),
    add_history_to_context=True,
    stream=True,
)

agent.print_response("What's the largest country in Europe by area?")
agent.print_response("What's the population of that country?")
agent.print_response("What's the population density per square kilometer?")
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
    python cookbook/11_models/openai/responses/zdr_reasoning_agent.py
    ```
  </Step>
</Steps>
