# Change State on Run

**Source:** https://docs.agno.com/state/team/change-state-on-run.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Change State on Run

This example demonstrates how to set and manage session state for different users and sessions. It shows how session state can be passed during runs and persists across multiple interactions within the same session.

<Steps>
  <Step title="Create a Python file">
    ```python change_state_on_run.py theme={null}
        from agno.db.in_memory import InMemoryDb
        from agno.models.openai import OpenAIResponses
        from agno.team import Team

        team = Team(
            db=InMemoryDb(),
            model=OpenAIResponses(id="gpt-5.2"),
            members=[],
            instructions="Users name is {user_name} and age is {age}",
        )

        # Sets the session state for the session with the id "user_1_session_1"
        team.print_response(
            "What is my name?",
            session_id="user_1_session_1",
            user_id="user_1",
            session_state={"user_name": "John", "age": 30},
        )

        # Will load the session state from the session with the id "user_1_session_1"
        team.print_response("How old am I?", session_id="user_1_session_1", user_id="user_1")

        # Sets the session state for the session with the id "user_2_session_1"
        team.print_response(
            "What is my name?",
            session_id="user_2_session_1",
            user_id="user_2",
            session_state={"user_name": "Jane", "age": 25},
        )

        # Will load the session state from the session with the id "user_2_session_1"
    team.print_response("How old am I?", session_id="user_2_session_1", user_id="user_2")
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

  <Step title="Run Team">
    ```bash  theme={null}
    python change_state_on_run.py
    ```
  </Step>
</Steps>
