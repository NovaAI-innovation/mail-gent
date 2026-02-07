# Confirmation Required with Toolkit

**Source:** https://docs.agno.com/hitl/usage/confirmation-required-toolkit.md
**Section:** Docs

**Description:** This example demonstrates human-in-the-loop functionality using toolkit-based tools that require confirmation. It shows how to handle user confirmation when working with pre-built tool collections like YFinanceTools.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Confirmation Required with Toolkit

> This example demonstrates human-in-the-loop functionality using toolkit-based tools that require confirmation. It shows how to handle user confirmation when working with pre-built tool collections like YFinanceTools.

<Steps>
  <Step title="Create a Python file">
    ```python confirmation_required_toolkit.py theme={null}
    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.models.openai import OpenAIResponses
    from agno.tools.yfinance import YFinanceTools
    from agno.utils import pprint
    from rich.console import Console
    from rich.prompt import Prompt

    console = Console()

    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[YFinanceTools(requires_confirmation_tools=["get_stock_price"])],
        markdown=True,
        db=SqliteDb(db_file="tmp/example.db"),
    )

    run_response = agent.run("What is the current stock price of Apple?")
    if run_response.is_paused:  # Or agent.run_response.is_paused
        for requirement in run_response.active_requirements:
            if requirement.needs_confirmation:
                # Ask for confirmation
                console.print(
                    f"Tool name [bold blue]{requirement.tool_execution.tool_name}({requirement.tool_execution.tool_args})[/] requires confirmation."
                )
                message = (
                    Prompt.ask("Do you want to continue?", choices=["y", "n"], default="y")
                    .strip()
                    .lower()
                )

                if message == "n":
                    requirement.reject()
                else:
                    requirement.confirm()

        run_response = agent.continue_run(
            run_id=run_response.run_id,
            requirements=run_response.requirements,
        )
        pprint.pprint_run_response(run_response)

    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai yfinance rich
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
    python confirmation_required_toolkit.py
    ```
  </Step>
</Steps>
