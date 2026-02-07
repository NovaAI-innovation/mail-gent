# Mistral Small

**Source:** https://docs.agno.com/models/providers/native/mistral/usage/mistral-small.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Mistral Small

## Code

```python cookbook/11_models/mistral/mistral_small.py theme={null}
from agno.agent import Agent
from agno.models.mistral import MistralChat
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=MistralChat(id="mistral-small-latest"),
    tools=[HackerNewsTools()],
    markdown=True,
)
agent.print_response("Tell me about mistrall small, any news", stream=True)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export MISTRAL_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U mistralai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/mistral/mistral_small.py
    ```
  </Step>
</Steps>
