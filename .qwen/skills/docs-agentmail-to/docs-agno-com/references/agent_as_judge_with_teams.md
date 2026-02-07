# Agent as Judge with Teams

**Source:** https://docs.agno.com/evals/agent-as-judge/usage/agent-as-judge-team.md
**Section:** Docs

**Description:** Evaluating team outputs with Agent as Judge

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent as Judge with Teams

> Evaluating team outputs with Agent as Judge

This example demonstrates evaluating team outputs using Agent as Judge evaluation.

<Steps>
  <Step title="Add the following code to your Python file">
    ```python agent_as_judge_team.py theme={null}
    from typing import Optional

    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.eval.agent_as_judge import AgentAsJudgeEval, AgentAsJudgeResult
    from agno.models.openai import OpenAIResponses
    from agno.team.team import Team

    # Setup database to persist eval results
    db = SqliteDb(db_file="tmp/agent_as_judge_team.db")

    # Setup a team with researcher and writer
    researcher = Agent(
        name="Researcher",
        role="Research and gather information",
        model=OpenAIResponses(id="gpt-5.2"),
    )

    writer = Agent(
        name="Writer",
        role="Write clear and concise summaries",
        model=OpenAIResponses(id="gpt-5.2"),
    )

    research_team = Team(
        name="Research Team",
        model=OpenAIResponses("gpt-5.2"),
        members=[researcher, writer],
        instructions=["First research the topic thoroughly, then write a clear summary."],
        db=db,
    )

    response = research_team.run("Explain quantum computing")

    evaluation = AgentAsJudgeEval(
        name="Team Response Quality",
        model=OpenAIResponses(id="gpt-5.2"),
        criteria="Response should be well-researched, clear, and comprehensive with good flow",
        scoring_strategy="binary",
        db=db,
    )

    result: Optional[AgentAsJudgeResult] = evaluation.run(
        input="Explain quantum computing",
        output=str(response.content),
        print_results=True,
        print_summary=True,
    )

    # Query database for stored results
    print("Database Results:")
    eval_runs = db.get_eval_runs()
    print(f"Total evaluations stored: {len(eval_runs)}")
    if eval_runs:
        latest = eval_runs[-1]
        print(f"Eval ID: {latest.run_id}")
        print(f"Team: {research_team.name}")

    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
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

  <Step title="Run the example">
    ```bash  theme={null}
    python agent_as_judge_team.py
    ```
  </Step>
</Steps>
