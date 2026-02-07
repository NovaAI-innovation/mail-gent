# Flash Thinking Agent

**Source:** https://docs.agno.com/models/providers/native/google/usage/flash-thinking.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Flash Thinking Agent

## Code

```python cookbook/11_models/google/gemini/flash_thinking_agent.py theme={null}
from agno.agent import Agent
from agno.models.google import Gemini

task = (
    "Three missionaries and three cannibals need to cross a river. "
    "They have a boat that can carry up to two people at a time. "
    "If, at any time, the cannibals outnumber the missionaries on either side of the river, the cannibals will eat the missionaries. "
    "How can all six people get across the river safely? Provide a step-by-step solution and show the solutions as an ascii diagram"
)

agent = Agent(model=Gemini(id="gemini-2.0-flash-thinking-exp-1219"), markdown=True)
agent.print_response(task, stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GOOGLE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U google-genai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/flash_thinking_agent.py
    ```
  </Step>
</Steps>
