# Groq with Reasoning Tools

**Source:** https://docs.agno.com/reasoning/usage/tools/groq-reasoning-tools.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Groq with Reasoning Tools

<Steps>
  <Step title="Add the following code to your Python file">
    ```python groq_llama_finance_agent.py theme={null}
    from textwrap import dedent

    from agno.agent import Agent
    from agno.models.groq import Groq
    from agno.tools.hackernews import HackerNewsTools
    from agno.tools.reasoning import ReasoningTools

    thinking_llama = Agent(
        model=Groq(id="meta-llama/llama-4-scout-17b-16e-instruct"),
        tools=[
            ReasoningTools(),
            HackerNewsTools(),
        ],
        instructions=dedent("""\
        ## General Instructions
        - Always start by using the think tool to map out the steps needed to complete the task.
        - After receiving tool results, use the think tool as a scratchpad to validate the results for correctness
        - Before responding to the user, use the think tool to jot down final thoughts and ideas.
        - Present final outputs in well-organized tables whenever possible.

        ## Using the think tool
        At every step, use the think tool as a scratchpad to:
        - Restate the object in your own words to ensure full comprehension.
        - List the  specific rules that apply to the current request
        - Check if all required information is collected and is valid
        - Verify that the planned action completes the task\
        """),
        markdown=True,
    )
    thinking_llama.print_response("Write a report comparing NVDA to TSLA", stream=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno groq ddgs
    ```
  </Step>

  <Step title="Export your Groq API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export GROQ_API_KEY="your_groq_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:GROQ_API_KEY="your_groq_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python groq_llama_finance_agent.py
    ```
  </Step>
</Steps>
