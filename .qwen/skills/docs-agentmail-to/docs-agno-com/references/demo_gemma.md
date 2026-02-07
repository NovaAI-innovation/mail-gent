# Demo Gemma

**Source:** https://docs.agno.com/models/providers/local/ollama/usage/demo-gemma.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Demo Gemma

## Code

```python cookbook/11_models/ollama/demo_gemma.py theme={null}
from pathlib import Path

from agno.agent import Agent
from agno.media import Image
from agno.models.ollama import Ollama

agent = Agent(model=Ollama(id="gemma3:12b"), markdown=True)

image_path = Path(__file__).parent.joinpath("super-agents.png")
agent.print_response(
    "Write a 3 sentence fiction story about the image",
    images=[Image(filepath=image_path)],
    stream=True,
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install Ollama">
    Follow the [Ollama installation guide](https://github.com/ollama/ollama?tab=readme-ov-file#macos) and run:

    ```bash  theme={null}
    ollama pull gemma3:12b
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ollama agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ollama/demo_gemma.py
    ```
  </Step>
</Steps>
