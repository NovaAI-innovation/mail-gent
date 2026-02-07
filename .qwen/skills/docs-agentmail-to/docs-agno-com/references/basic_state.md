# Basic State

**Source:** https://docs.agno.com/state/agent/session-state-basic.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Basic State

This example demonstrates how to create an agent with basic session state management, maintaining a shopping list across interactions using SQLite storage.

<Steps>
  <Step title="Create a Python file">
    ```python session_state_basic.py theme={null}
    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.models.openai import OpenAIResponses


    def add_item(session_state, item: str) -> str:
        """Add an item to the shopping list."""
        session_state["shopping_list"].append(item)
        return f"The shopping list is now {session_state['shopping_list']}"


    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        session_state={"shopping_list": []},
        db=SqliteDb(db_file="tmp/agents.db"),
        tools=[add_item],
        instructions="Current state (shopping list) is: {shopping_list}",
        markdown=True,
    )

    agent.print_response("Add milk, eggs, and bread to the shopping list", stream=True)
    print(f"Final session state: {agent.get_session_state()}")
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    <Snippet file="set-openai-key.mdx" />
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python session_state_basic.py
    ```
  </Step>
</Steps>
