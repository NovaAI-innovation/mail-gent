# Ollama Cloud

**Source:** https://docs.agno.com/models/providers/local/ollama/usage/cloud.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Ollama Cloud

## Code

```python cookbook/11_models/ollama/ollama_cloud.py theme={null}
from agno.agent import Agent
from agno.models.ollama import Ollama

agent = Agent(
    model=Ollama(id="gpt-oss:120b-cloud", host="https://ollama.com"),
)

agent.print_response("How many r's in the word 'strawberry'?", stream=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set up Ollama Cloud API Key">
    Sign up at [ollama.com](https://ollama.com) and get your API key, then export it:

    ```bash  theme={null}
    export OLLAMA_API_KEY=your_api_key_here
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U ollama agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/ollama/ollama_cloud.py
    ```
  </Step>
</Steps>

## Key Features

* **No local setup required**: Access powerful models instantly without downloading or managing local installations
* **Production-ready**: Enterprise-grade infrastructure with reliable uptime and performance
* **Wide model selection**: Access to powerful models including GPT-OSS and other optimized cloud models
* **Automatic configuration**: When `api_key` is provided, the host automatically defaults to `https://ollama.com`
