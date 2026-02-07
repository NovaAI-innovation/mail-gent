# State in Instructions

**Source:** https://docs.agno.com/state/team/session-state-in-instructions.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# State in Instructions

This example demonstrates how to use session state variables directly in team instructions using template syntax. The session state values are automatically injected into the instructions, making them available to the team during execution.

<Steps>
  <Step title="Create a Python file">
    ```python session_state_in_instructions.py theme={null}
        from agno.team.team import Team

        team = Team(
            members=[],
            # Initialize the session state with a variable
            session_state={"user_name": "John"},
            instructions="Users name is {user_name}",
            markdown=True,
        )

    team.print_response("What is my name?", stream=True)
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
    python session_state_in_instructions.py
    ```
  </Step>
</Steps>
