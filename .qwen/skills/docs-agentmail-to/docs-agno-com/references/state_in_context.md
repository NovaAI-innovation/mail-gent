# State in Context

**Source:** https://docs.agno.com/state/agent/session-state-in-context.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# State in Context

This example demonstrates how to use session state and manage user context across different sessions. It shows how session state persists and can be retrieved for different users and sessions.

<Steps>
  <Step title="Create a Python file">
    ```python session_state_in_context.py theme={null}
    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.models.openai import OpenAIResponses

    db = SqliteDb(db_file="tmp/agent.db")

    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        instructions="Users name is {user_name} and age is {age}",
        db=db,
    )

    # Sets the session state for the session with the id "user_1_session_1"
    agent.print_response(
        "What is my name?",
        session_id="user_1_session_1",
        user_id="user_1",
        session_state={"user_name": "John", "age": 30},
        stream=True,
    )

    # Will load the session state from the session with the id "user_1_session_1"
    agent.print_response("How old am I?", session_id="user_1_session_1", user_id="user_1", stream=True)

    # Sets the session state for the session with the id "user_2_session_1"
    agent.print_response(
        "What is my name?",
        session_id="user_2_session_1",
        user_id="user_2",
        session_state={"user_name": "Jane", "age": 25},
        stream=True,
    )

    # Will load the session state from the session with the id "user_2_session_1"
    agent.print_response("How old am I?", session_id="user_2_session_1", user_id="user_2", stream=True)
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
    python session_state_in_context.py
    ```
  </Step>
</Steps>
