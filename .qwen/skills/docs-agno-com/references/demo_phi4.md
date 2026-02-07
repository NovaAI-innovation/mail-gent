# Demo Phi4

**Source:** https://docs.agno.com/models/providers/local/ollama/usage/demo-phi4.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Demo Phi4

## Code

```python cookbook/11_models/ollama/demo_phi4.py theme={null}
from agno.agent import Agent, RunOutput  # noqa
from agno.models.ollama import Ollama

agent = Agent(model=Ollama(id="phi4"), markdown=True)

# Print the response in the terminal
agent.print_response("Tell me a scary story in exactly 10 words.")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install Ollama">
    Follow the [Ollama installation guide](https://github.com/ollama/ollama?tab=readme-ov-file#macos) and run:

    ```bash  theme={null}
    ollama pull phi4
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ollama agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ollama/demo_phi4.py
    ```
  </Step>
</Steps>
