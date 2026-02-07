# Agent with External URL Input

**Source:** https://docs.agno.com/models/providers/native/google/usage/external-url-input.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with External URL Input

## Code

```python cookbook/11_models/google/gemini/external_url_input.py theme={null}
"""External URL input with Gemini.

Pass files from public HTTPS URLs directly without downloading.
Supports files up to 100MB. Requires Gemini 3.x models.
"""

from agno.agent import Agent
from agno.media import File
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-3-flash-preview"),
    markdown=True,
)

agent.print_response(
    "Summarize this document.",
    files=[
        File(
            url="https://agno-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf",
            mime_type="application/pdf",
        )
    ],
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GOOGLE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    pip install -U google-genai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/external_url_input.py
    ```
  </Step>
</Steps>
