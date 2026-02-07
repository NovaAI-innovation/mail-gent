# Instructions via Function

**Source:** https://docs.agno.com/context/agent/instructions-via-function.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Instructions via Function

This example demonstrates how to provide instructions to an agent via a function that can access the agent's properties, enabling dynamic and personalized instruction generation.

## Code

```python instructions_via_function.py theme={null}
from typing import List

from agno.agent import Agent


def get_instructions(agent: Agent) -> List[str]:
    return [
        f"Your name is {agent.name}!",
        "Talk in haiku's!",
        "Use poetry to answer questions.",
    ]


agent = Agent(
    name="AgentX",
    instructions=get_instructions,
    markdown=True,
)
agent.print_response("Who are you?", stream=True)
```

## Usage

<Steps>
  <Step title="Create a Python file">
    Create `instructions_via_function.py` with the code above.
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
      export OPENAI_API_KEY="your_openai_api_key_here"
      ```

      ```bash Windows theme={null}
      $Env:OPENAI_API_KEY="your_openai_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python instructions_via_function.py
    ```
  </Step>
</Steps>
