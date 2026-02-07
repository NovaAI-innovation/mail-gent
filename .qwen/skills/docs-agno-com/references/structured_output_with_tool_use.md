# Structured Output With Tool Use

**Source:** https://docs.agno.com/models/providers/native/mistral/usage/structured-output-with-tool-use.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Structured Output With Tool Use

## Code

```python cookbook/11_models/mistral/structured_output_with_tool_use.py theme={null}
from agno.agent import Agent
from agno.models.mistral import MistralChat
from agno.tools.hackernews import HackerNewsTools
from pydantic import BaseModel

class Person(BaseModel):
    name: str
    description: str

model = MistralChat(
    id="mistral-medium-latest",
    temperature=0.0,
)

researcher = Agent(
    name="Researcher",
    model=model,
    role="You find people with a specific role at a provided company.",
    instructions=[
        "- Search the web for the person described"
        "- Find out if they have public contact details"
        "- Return the information in a structured format"
    ],
    tools=[HackerNewsTools()],
    output_schema=Person,
    add_datetime_to_context=True,
)

researcher.print_response("Find information about Elon Musk")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export MISTRAL_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U mistralai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/mistral/structured_output_with_tool_use.py
    ```
  </Step>
</Steps>
