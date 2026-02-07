# Basic Agent Tracing

**Source:** https://docs.agno.com/tracing/usage/basic-agent-tracing.md
**Section:** Docs

**Description:** Enable tracing and observability for agents.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Basic Agent Tracing

> Enable tracing and observability for agents.

This example shows how to enable tracing for an agent. Once tracing is enabled, all agent runs, model calls, and tool executions are automatically captured and stored in your database.

<Steps>
  <Step title="Create a Python file">
    ```python basic_agent_tracing.py theme={null}
    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.models.openai import OpenAIResponses
    from agno.tools.hackernews import HackerNewsTools
    from agno.tracing import setup_tracing

    # Set up database for traces
    db = SqliteDb(db_file="tmp/traces.db")

    # Enable tracing (call once at startup)
    setup_tracing(db=db)

    # Create agent - automatically traced!
    agent = Agent(
        name="HackerNews Agent",
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[HackerNewsTools()],
        instructions="You are a hacker news agent. Answer questions concisely.",
        markdown=True,
        db=db,
    )

    # Run the agent - traces are captured automatically
    agent.print_response("What's trending on HackerNews?")

    # Query traces from the database
    traces, count = db.get_traces(agent_id=agent.id, limit=10)
    print(f"\nFound {count} traces for agent '{agent.name}'")
    for trace in traces:
        print(f"  - {trace.name}: {trace.duration_ms}ms ({trace.status})")
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

  <Step title="Run the agent">
    ```bash  theme={null}
    python basic_agent_tracing.py
    ```
  </Step>
</Steps>

## Developer Resources
