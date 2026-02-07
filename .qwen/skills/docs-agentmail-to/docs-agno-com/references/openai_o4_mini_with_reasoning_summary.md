# OpenAI o4-mini with reasoning summary

**Source:** https://docs.agno.com/reasoning/usage/models/openai/reasoning-summary.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# OpenAI o4-mini with reasoning summary

<Steps>
  <Step title="Add the following code to your Python file">
    ```python openai.py theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses
    from agno.tools.hackernews import HackerNewsTools

    # Setup the reasoning Agent
    agent = Agent(
        model=OpenAIResponses(
            id="o4-mini",
            reasoning_summary="auto",  # Requesting a reasoning summary
        ),
        tools=[HackerNewsTools()],
        instructions="Use tables to display the analysis",
        markdown=True,
    )

    agent.print_response(
        "Write a brief report comparing NVDA to TSLA",
        stream=True,
    )
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai ddgs
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
    python openai.py
    ```
  </Step>
</Steps>
