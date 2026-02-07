# Structured Output Agent

**Source:** https://docs.agno.com/models/providers/native/dashscope/usage/structured-output.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Structured Output Agent

## Code

```python cookbook/11_models/dashscope/structured_output.py theme={null}
from typing import List

from agno.agent import Agent
from agno.models.dashscope import DashScope
from pydantic import BaseModel, Field

class MovieScript(BaseModel):
    name: str = Field(..., description="Give a name to this movie")
    setting: str = Field(
        ..., description="Provide a nice setting for a blockbuster movie."
    )
    ending: str = Field(
        ...,
        description="Ending of the movie. If not available, provide a happy ending.",
    )
    genre: str = Field(
        ...,
        description="Genre of the movie. If not available, select action, thriller or romantic comedy.",
    )
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(
        ..., description="3 sentence storyline for the movie. Make it exciting!"
    )

# Agent that returns a structured output
structured_output_agent = Agent(
    model=DashScope(id="qwen-plus"),
    description="You write movie scripts and return them as structured JSON data.",
    output_schema=MovieScript,
)

structured_output_agent.print_response(
    "Create a movie script about llamas ruling the world. "
    "Return a JSON object with: name (movie title), setting, ending, genre, "
    "characters (list of character names), and storyline (3 sentences)."
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export DASHSCOPE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/dashscope/structured_output.py
    ```
  </Step>
</Steps>
