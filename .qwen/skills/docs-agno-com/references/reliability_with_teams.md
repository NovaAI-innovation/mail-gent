# Reliability with Teams

**Source:** https://docs.agno.com/evals/reliability/usage/reliability-with-teams.md
**Section:** Docs

**Description:** Example showing how to assert an Agno Team is making the expected tool calls.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Reliability with Teams

> Example showing how to assert an Agno Team is making the expected tool calls.

<Steps>
  <Step title="Create a Python file">
    ```python reliability_with_teams.py theme={null}
    from typing import Optional

    from agno.agent import Agent
    from agno.eval.reliability import ReliabilityEval, ReliabilityResult
    from agno.models.openai import OpenAIResponses
    from agno.run.team import TeamRunOutput
    from agno.team.team import Team
    from agno.tools.yfinance import YFinanceTools

    team_member = Agent(
        name="Stock Searcher",
        model=OpenAIResponses("gpt-5.2"),
        role="Searches the web for information on a stock.",
        tools=[YFinanceTools(stock_price=True)],
    )

    team = Team(
        name="Stock Research Team",
        model=OpenAIResponses("gpt-5.2"),
        members=[team_member],
        markdown=True,
        show_members_responses=True,
    )

    expected_tool_calls = [
        "delegate_task_to_member",  # Tool call used to delegate a task to a Team member
        "get_current_stock_price",  # Tool call used to get the current stock price of a stock
    ]


    def evaluate_team_reliability():
        response: TeamRunOutput = team.run("What is the current stock price of NVDA?")
        evaluation = ReliabilityEval(
            name="Team Reliability Evaluation",
            team_response=response,
            expected_tool_calls=expected_tool_calls,
        )
        result: Optional[ReliabilityResult] = evaluation.run(print_results=True)
        if result:
            result.assert_passed()


    if __name__ == "__main__":
        evaluate_team_reliability()
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno yfinance
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

  <Step title="Run Team">
    ```bash  theme={null}
    python reliability_with_teams.py
    ```
  </Step>
</Steps>
