# Agent with Structured Output

**Source:** https://docs.agno.com/models/providers/native/perplexity/usage/structured-output.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Structured Output

## Code

```python cookbook/11_models/perplexity/structured_output.py theme={null}
from typing import List

from agno.agent import Agent, RunOutput  # noqa
from agno.models.perplexity import Perplexity
from pydantic import BaseModel, Field

class MovieScript(BaseModel):
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
    name: str = Field(..., description="Give a name to this movie")
    characters: List[str] = Field(..., description="Name of characters for this movie.")
    storyline: str = Field(
        ..., description="3 sentence storyline for the movie. Make it exciting!"
    )

# Agent that uses JSON mode
json_mode_agent = Agent(
    model=Perplexity(id="sonar-pro"),
    description="You write movie scripts.",
    output_schema=MovieScript,
    markdown=True,
)

# Get the response in a variable
# json_mode_response: RunOutput = json_mode_agent.run("New York")
# pprint(json_mode_response.content)
# structured_output_response: RunOutput = structured_output_agent.run("New York")
# pprint(structured_output_response.content)

json_mode_agent.print_response("New York")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export PERPLEXITY_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/perplexity/structured_output.py
    ```
  </Step>
</Steps>
