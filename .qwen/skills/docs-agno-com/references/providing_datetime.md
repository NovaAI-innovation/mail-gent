# Providing Datetime

**Source:** https://docs.agno.com/context/agent/datetime-instructions.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Providing Datetime

This example demonstrates how to add current date and time context to agent instructions, enabling the agent to provide time-aware responses.

## Code

```python datetime_instructions.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    add_datetime_to_context=True,
    timezone_identifier="Etc/UTC",
)
agent.print_response(
    "What is the current date and time? What is the current time in NYC?"
)
```

## Usage

<Steps>
  <Step title="Create a Python file">
    Create `datetime_instructions.py` with the code above.
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
    python datetime_instructions.py
    ```
  </Step>
</Steps>
