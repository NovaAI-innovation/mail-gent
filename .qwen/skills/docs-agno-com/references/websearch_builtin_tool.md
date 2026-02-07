# Websearch Builtin Tool

**Source:** https://docs.agno.com/models/providers/native/openai/responses/usage/websearch-builtin-tool.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Websearch Builtin Tool

## Code

```python cookbook/11_models/openai/responses/websearch_builtin_tool.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.file import FileTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5-mini"),
    tools=[{"type": "web_search_preview"}, FileTools()],
    instructions="Save the results to a file with a relevant name.",
    markdown=True,
)
agent.print_response("Whats happening in France?")

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/openai/responses/websearch_builtin_tool.py
    ```
  </Step>
</Steps>
