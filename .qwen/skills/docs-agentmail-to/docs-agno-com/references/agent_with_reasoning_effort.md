# Agent with Reasoning Effort

**Source:** https://docs.agno.com/models/providers/native/openai/completion/usage/reasoning-effort.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Reasoning Effort

## Code

```python cookbook/10_reasoning/models/openai/reasoning_effort.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2", reasoning_effort="high"),
    tools=[HackerNewsTools()],
        markdown=True,
)

agent.print_response("Write a report on the latest news on AI?", stream=True)
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
    python cookbook/10_reasoning/models/openai/reasoning_effort.py
    ```
  </Step>
</Steps>
