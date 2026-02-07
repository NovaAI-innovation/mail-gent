# Web Fetch

**Source:** https://docs.agno.com/models/providers/native/anthropic/usage/web-fetch.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Web Fetch

## Code

```python cookbook/11_models/anthropic/web_fetch.py theme={null}
from agno.agent import Agent
from agno.models.anthropic import Claude

agent = Agent(
    model=Claude(
        id="claude-opus-4-1-20250805",
        betas=["web-fetch-2025-09-10"],
    ),
    tools=[
        {
            "type": "web_fetch_20250910",
            "name": "web_fetch",
            "max_uses": 5,
        }
    ],
    markdown=True,
)

agent.print_response(
    "Tell me more about https://en.wikipedia.org/wiki/Glacier_National_Park_(U.S.)",
    stream=True,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export ANTHROPIC_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U anthropic agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/anthropic/web_fetch.py
    ```
  </Step>
</Steps>
