# Code Generation

**Source:** https://docs.agno.com/models/providers/local/vllm/usage/code-generation.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Code Generation

## Code

```python cookbook/11_models/vllm/code_generation.py theme={null}
from agno.agent import Agent
from agno.models.vllm import VLLM

agent = Agent(
    model=VLLM(id="deepseek-ai/deepseek-coder-6.7b-instruct"),
    description="You are an expert Python developer.",
    markdown=True,
)

agent.print_response(
    "Write a Python function that returns the nth Fibonacci number using dynamic programming."
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install Libraries">
    ```bash  theme={null}
    uv pip install -U agno openai vllm
    ```
  </Step>

  <Step title="Start vLLM server">
    ```bash  theme={null}
    vllm serve deepseek-ai/deepseek-coder-6.7b-instruct \
        --dtype float32 \
        --tool-call-parser pythonic
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/vllm/code_generation.py
    ```
  </Step>
</Steps>
