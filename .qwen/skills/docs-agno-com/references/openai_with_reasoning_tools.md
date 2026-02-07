# OpenAI with Reasoning Tools

**Source:** https://docs.agno.com/reasoning/usage/tools/openai-reasoning-tools.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# OpenAI with Reasoning Tools

<Steps>
  <Step title="Add the following code to your Python file">
    ```python openai_reasoning_tools.py theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses
    from agno.tools.hackernews import HackerNewsTools
    from agno.tools.reasoning import ReasoningTools

    reasoning_agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[
            ReasoningTools(
                think=True,
                analyze=True,
                add_instructions=True,
                add_few_shot=True,
            ),
            HackerNewsTools(),
        ],
        instructions="Use tables where possible",
        markdown=True,
    )
    reasoning_agent.print_response(
        "Write a report comparing NVDA to TSLA",
        stream=True,
        show_full_reasoning=True,
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
    python openai_reasoning_tools.py
    ```
  </Step>
</Steps>
