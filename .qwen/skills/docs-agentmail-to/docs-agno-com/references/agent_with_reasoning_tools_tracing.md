# Agent with Reasoning Tools Tracing

**Source:** https://docs.agno.com/agent-os/tracing/usage/agent-with-reasoning-tools-tracing.md
**Section:** Docs

**Description:** Trace agents with reasoning tools in AgentOS.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Reasoning Tools Tracing

> Trace agents with reasoning tools in AgentOS.

This example shows how to trace an agent that uses reasoning tools in AgentOS. The traces capture the agent's reasoning process, including all intermediate steps.

<Steps>
  <Step title="Create a Python file">
    ```python agent_with_reasoning_tools_tracing.py theme={null}
    from textwrap import dedent

    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.models.openai import OpenAIResponses
    from agno.os import AgentOS
    from agno.tools.reasoning import ReasoningTools

    db = SqliteDb(db_file="tmp/traces.db")

    reasoning_agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[ReasoningTools(add_instructions=True)],
        instructions=dedent("""\
            You are an expert problem-solving assistant with strong analytical skills! 🧠

            Your approach to problems:
            1. First, break down complex questions into component parts
            2. Clearly state your assumptions
            3. Develop a structured reasoning path
            4. Consider multiple perspectives
            5. Evaluate evidence and counter-arguments
            6. Draw well-justified conclusions

            When solving problems:
            - Use explicit step-by-step reasoning
            - Identify key variables and constraints
            - Explore alternative scenarios
            - Highlight areas of uncertainty
            - Explain your thought process clearly
            - Consider both short and long-term implications
            - Evaluate trade-offs explicitly

            For quantitative problems:
            - Show your calculations
            - Explain the significance of numbers
            - Consider confidence intervals when appropriate
            - Identify source data reliability

            For qualitative reasoning:
            - Assess how different factors interact
            - Consider psychological and social dynamics
            - Evaluate practical constraints
            - Address value considerations
            \
        """),
        add_datetime_to_context=True,
        stream_events=True,
        markdown=True,
        db=db,
    )

    # Setup AgentOS with tracing enabled
    agent_os = AgentOS(
        description="Example app for reasoning agent with tracing",
        agents=[reasoning_agent],
        tracing=True,
    )
    app = agent_os.get_app()

    if __name__ == "__main__":
        agent_os.serve(app="agent_with_reasoning_tools_tracing:app", reload=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno opentelemetry-api opentelemetry-sdk openinference-instrumentation-agno
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

  <Step title="Run AgentOS">
    ```bash  theme={null}
    python agent_with_reasoning_tools_tracing.py
    ```

    Your AgentOS will be available at `http://localhost:7777`. View traces in the AgentOS dashboard.
  </Step>
</Steps>
