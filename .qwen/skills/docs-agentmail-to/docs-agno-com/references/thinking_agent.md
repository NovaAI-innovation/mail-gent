# Thinking Agent

**Source:** https://docs.agno.com/models/providers/native/dashscope/usage/thinking-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Thinking Agent

## Code

```python cookbook/11_models/dashscope/thinking_agent.py theme={null}
from agno.agent import Agent
from agno.media import Image
from agno.models.dashscope import DashScope

agent = Agent(
    model=DashScope(id="qvq-max", enable_thinking=True),
)

image_url = "https://img.alicdn.com/imgextra/i1/O1CN01gDEY8M1W114Hi3XcN_!!6000000002727-0-tps-1024-406.jpg"

agent.print_response(
    "How do I solve this problem? Please think through each step carefully.",
    images=[Image(url=image_url)],
    stream=True,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export DASHSCOPE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/dashscope/thinking_agent.py
    ```
  </Step>
</Steps>
