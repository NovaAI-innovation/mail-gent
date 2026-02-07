# Agent with Tools Stream

**Source:** https://docs.agno.com/models/providers/local/llama-cpp/usage/tool-use-stream.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Tools Stream

## Code

```python cookbook/11_models/llama_cpp/tool_use_stream.py theme={null}
"""Run `uv pip install` to install dependencies."""

from agno.agent import Agent
from agno.models.llama_cpp import LlamaCpp
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=LlamaCpp(id="ggml-org/gpt-oss-20b-GGUF"),
    tools=[HackerNewsTools()],
    markdown=True,
)
agent.print_response("Whats happening in France?", stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install LlamaCpp">
    Follow the [LlamaCpp installation guide](https://github.com/ggerganov/llama.cpp) and start the server:

    ```bash  theme={null}
    llama-server -hf ggml-org/gpt-oss-20b-GGUF --ctx-size 0 --jinja -ub 2048 -b 2048
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/llama_cpp/tool_use_stream.py
    ```
  </Step>
</Steps>
