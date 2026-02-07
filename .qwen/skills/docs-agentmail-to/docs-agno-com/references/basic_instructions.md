# Basic Instructions

**Source:** https://docs.agno.com/context/agent/instructions.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Basic Instructions

This example demonstrates how to provide basic instructions to an agent to guide its response behavior and storytelling style.

## Code

```python instructions.py theme={null}
from agno.agent import Agent

agent = Agent(instructions="Share a 2 sentence story about")
agent.print_response("Love in the year 12000.")
```

## Usage

<Steps>
  <Step title="Create a Python file">
    Create `instructions.py` with the code above.
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
    python instructions.py
    ```
  </Step>
</Steps>
