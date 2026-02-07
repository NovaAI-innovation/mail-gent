# Agent with Grounding

**Source:** https://docs.agno.com/models/providers/native/google/usage/grounding.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Grounding

## Code

```python cookbook/11_models/google/gemini/grounding.py theme={null}
"""Grounding with Gemini.

Grounding enables Gemini to search the web and provide responses backed by
real-time information with citations. This is a legacy tool - for Gemini 2.0+
models, consider using the 'search' parameter instead.

"""

from agno.agent import Agent
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(
        id="gemini-2.0-flash",
        grounding=True,
        grounding_dynamic_threshold=0.7,  # Optional: set threshold for grounding
    ),
    add_datetime_to_context=True,
)

# Ask questions that benefit from real-time information
agent.print_response(
    "What are the current market trends in renewable energy?",
    stream=True,
    markdown=True,
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
    uv pip install -U google-genai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/grounding.py
    ```
  </Step>
</Steps>
