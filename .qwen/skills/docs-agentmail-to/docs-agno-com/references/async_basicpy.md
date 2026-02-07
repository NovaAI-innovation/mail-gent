# Async Basic.Py

**Source:** https://docs.agno.com/models/providers/gateways/huggingface/usage/async-basic.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Basic.Py

## Code

```python cookbook/11_models/huggingface/async_basic.py theme={null}
import asyncio

from agno.agent import Agent
from agno.models.huggingface import HuggingFace

agent = Agent(
    model=HuggingFace(
        id="mistralai/Mistral-7B-Instruct-v0.2", max_tokens=4096, temperature=0
    ),
)
asyncio.run(
    agent.aprint_response(
        "What is meaning of life and then recommend 5 best books to read about it"
    )
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export HF_TOKEN=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U huggingface_hub agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/huggingface/async_basic.py
    ```
  </Step>
</Steps>
