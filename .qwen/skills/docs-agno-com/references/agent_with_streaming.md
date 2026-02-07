# Agent with Streaming

**Source:** https://docs.agno.com/models/providers/local/vllm/usage/basic-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Streaming

## Code

```python cookbook/11_models/vllm/basic_stream.py theme={null}
from agno.agent import Agent
from agno.models.vllm import VLLM

agent = Agent(
    model=VLLM(id="Qwen/Qwen2.5-7B-Instruct", top_k=20, enable_thinking=False),
    markdown=True,
)
agent.print_response("Share a 2 sentence horror story", stream=True)
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
    vllm serve Qwen/Qwen2.5-7B-Instruct \
        --enable-auto-tool-choice \
        --tool-call-parser hermes \
        --dtype float16 \
        --max-model-len 8192 \
        --gpu-memory-utilization 0.9
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/vllm/basic_stream.py
    ```
  </Step>
</Steps>
