# Browser Search Agent

**Source:** https://docs.agno.com/models/providers/gateways/groq/usage/browser-search.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Browser Search Agent

## Code

```python cookbook/11_models/groq/browser_search.py theme={null}
from agno.agent import Agent
from agno.models.groq import Groq

agent = Agent(
    model=Groq(id="openai/gpt-oss-20b"),
    tools=[{"type": "browser_search"}],
)
agent.print_response("Is the Going-to-the-sun road open for public?")
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GROQ_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U groq agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/groq/browser_search.py
    ```
  </Step>
</Steps>
