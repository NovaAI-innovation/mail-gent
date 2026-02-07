# Agent as Judge with Guidelines

**Source:** https://docs.agno.com/evals/agent-as-judge/usage/agent-as-judge-with-guidelines.md
**Section:** Docs

**Description:** Using additional guidelines for more detailed evaluation criteria

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent as Judge with Guidelines

> Using additional guidelines for more detailed evaluation criteria

This example demonstrates using additional guidelines to provide more specific evaluation criteria.

<Steps>
  <Step title="Add the following code to your Python file">
    ```python agent_as_judge_with_guidelines.py theme={null}
    from typing import Optional

    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.eval.agent_as_judge import AgentAsJudgeEval, AgentAsJudgeResult
    from agno.models.openai import OpenAIResponses

    # Setup database to persist eval results
    db = SqliteDb(db_file="tmp/agent_as_judge_guidelines.db")

    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        instructions="You are a Tesla Model 3 product specialist. Provide detailed and helpful specifications.",
        db=db,
    )

    response = agent.run("What is the maximum speed of the Tesla Model 3?")

    evaluation = AgentAsJudgeEval(
        name="Product Info Quality",
        model=OpenAIResponses(id="gpt-5.2"),
        criteria="Response should be informative, well-formatted, and accurate for product specifications",
        scoring_strategy="numeric",
        threshold=8,
        additional_guidelines=[
            "Must include specific numbers with proper units (mph, km/h, etc.)",
            "Should provide context for different model variants if applicable",
            "Information should be technically accurate and complete",
        ],
        db=db,
    )

    result: Optional[AgentAsJudgeResult] = evaluation.run(
        input="What is the maximum speed?",
        output=str(response.content),
        print_results=True,
    )

    # Query database for stored results
    print("Database Results:")
    eval_runs = db.get_eval_runs()
    print(f"Total evaluations stored: {len(eval_runs)}")
    if eval_runs:
        latest = eval_runs[-1]
        print(f"Eval ID: {latest.run_id}")
        print(f"Additional guidelines used: {len(evaluation.additional_guidelines)}")

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
    python agent_as_judge_with_guidelines.py
    ```
  </Step>
</Steps>
