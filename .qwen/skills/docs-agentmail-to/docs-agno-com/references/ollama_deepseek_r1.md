# Ollama DeepSeek R1

**Source:** https://docs.agno.com/reasoning/usage/models/ollama/ollama.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Ollama DeepSeek R1

<Steps>
  <Step title="Add the following code to your Python file">
    ```python ollama.py theme={null}
    from agno.agent import Agent
    from agno.models.ollama.chat import Ollama

    agent = Agent(
        model=Ollama(id="llama3.2:latest"),
        reasoning_model=Ollama(id="deepseek-r1:14b", max_tokens=4096),
    )
    agent.print_response(
        "Solve the trolley problem. Evaluate multiple ethical frameworks. "
        "Include an ASCII diagram of your solution.",
        stream=True,
    )
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno ollama
    ```
  </Step>

  <Step title="Install Ollama">
    Follow the [installation guide](https://github.com/ollama/ollama?tab=readme-ov-file#macos) and run:

    ```bash  theme={null}
    ollama pull llama3.2:latest
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python ollama.py
    ```
  </Step>
</Steps>
