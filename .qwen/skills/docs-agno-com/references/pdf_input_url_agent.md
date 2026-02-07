# PDF Input URL Agent

**Source:** https://docs.agno.com/models/providers/native/anthropic/usage/pdf-input-url.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# PDF Input URL Agent

## Code

```python cookbook/11_models/anthropic/pdf_input_url.py theme={null}
from agno.agent import Agent
from agno.media import File
from agno.models.anthropic import Claude

agent = Agent(
    model=Claude(id="claude-sonnet-4-20250514"),
    markdown=True,
)

agent.print_response(
    "Summarize the contents of the attached file.",
    files=[
        File(url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"),
    ],
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
    python cookbook/11_models/anthropic/pdf_input_url.py
    ```
  </Step>
</Steps>
