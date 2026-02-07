# Agent Using Multimodal Tool Response in Runs

**Source:** https://docs.agno.com/multimodal/agent/usage/agent-using-multimodal-tool-response-in-runs.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent Using Multimodal Tool Response in Runs

This example demonstrates how to create an agent that uses DALL-E to generate images and maintains conversation history across multiple runs, allowing the agent to remember previous interactions and images generated.

## Code

```python agent_using_multimodal_tool_response_in_runs.py theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.tools.dalle import DalleTools

# Create an Agent with the DALL-E tool
agent = Agent(
    tools=[DalleTools()],
    name="DALL-E Image Generator",
    add_history_to_context=True,
    db=SqliteDb(db_file="tmp/test.db"),
)

agent.print_response(
    "Generate an image of a Siamese white furry cat sitting on a couch?",
    markdown=True,
)

agent.print_response(
    "Which type of animal and the breed are we talking about?", markdown=True
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
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
    python agent_using_multimodal_tool_response_in_runs.py
    ```
  </Step>
</Steps>
