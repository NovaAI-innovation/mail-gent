# Set Client

**Source:** https://docs.agno.com/models/providers/local/ollama/usage/set-client.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Set Client

## Code

```python cookbook/11_models/ollama/set_client.py theme={null}
from agno.agent import Agent, RunOutput  # noqa
from agno.models.ollama import Ollama
from ollama import Client as OllamaClient

agent = Agent(
    model=Ollama(id="llama3.1:8b", client=OllamaClient()),
    markdown=True,
)

# Print the response in the terminal
agent.print_response("Share a 2 sentence horror story")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install Ollama">
    Follow the [Ollama installation guide](https://github.com/ollama/ollama?tab=readme-ov-file#macos) and run:

    ```bash  theme={null}
    ollama pull llama3.1:8b
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ollama agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ollama/set_client.py
    ```
  </Step>
</Steps>
