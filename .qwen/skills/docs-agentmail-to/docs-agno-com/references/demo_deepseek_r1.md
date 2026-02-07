# Demo Deepseek R1

**Source:** https://docs.agno.com/models/providers/local/ollama/usage/demo-deepseek-r1.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Demo Deepseek R1

## Code

```python cookbook/11_models/ollama/demo_deepseek_r1.py theme={null}
from agno.agent import Agent, RunOutput  # noqa
from agno.models.ollama import Ollama

agent = Agent(model=Ollama(id="deepseek-r1:14b"), markdown=True)

# Print the response in the terminal
agent.print_response(
    "Write me python code to solve quadratic equations. Explain your reasoning."
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install Ollama">
    Follow the [Ollama installation guide](https://github.com/ollama/ollama?tab=readme-ov-file#macos) and run:

    ```bash  theme={null}
    ollama pull deepseek-r1:14b
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ollama agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ollama/demo_deepseek_r1.py
    ```
  </Step>
</Steps>
