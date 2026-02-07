# Agent Flex Tier

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/agent-flex-tier.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent Flex Tier

## Code

```python cookbook/11_models/openai/responses/agent_flex_tier.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses

agent = Agent(
    model=OpenAIResponses(id="o4-mini", service_tier="flex"),
    markdown=True,
)

agent.print_response("Share a 2 sentence horror story")
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
    python cookbook/11_models/openai/responses/agent_flex_tier.py
    ```
  </Step>
</Steps>
