# Async Agent as Judge

**Source:** https://docs.agno.com/evals/agent-as-judge/usage/agent-as-judge-async.md
**Section:** Docs

**Description:** Asynchronous evaluation with Agent as Judge

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Agent as Judge

> Asynchronous evaluation with Agent as Judge

This example demonstrates an asynchronous Agent as Judge evaluation with async callbacks.

<Steps>
  <Step title="Add the following code to your Python file">
    ```python agent_as_judge_async.py theme={null}
    import asyncio

    from agno.agent import Agent
    from agno.db.sqlite import AsyncSqliteDb
    from agno.eval.agent_as_judge import AgentAsJudgeEval, AgentAsJudgeEvaluation
    from agno.models.openai import OpenAIResponses


    async def on_evaluation_failure(evaluation: AgentAsJudgeEvaluation):
        """Async callback triggered when evaluation fails (score < threshold)."""
        print(f"Evaluation failed - Score: {evaluation.score}/10")
        print(f"Reason: {evaluation.reason}")


    async def main():
        # Setup database to persist eval results
        db = AsyncSqliteDb(db_file="tmp/agent_as_judge_async.db")

        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            instructions="Provide helpful and informative answers.",
            db=db,
        )

        response = await agent.arun("Explain machine learning in simple terms")

        evaluation = AgentAsJudgeEval(
            name="ML Explanation Quality",
            model=OpenAIResponses(id="gpt-5.2"),
            criteria="Explanation should be clear, beginner-friendly, and avoid jargon",
            scoring_strategy="numeric",
            threshold=9,
            on_fail=on_evaluation_failure,
            db=db,
        )

        result = await evaluation.arun(
            input="Explain machine learning in simple terms",
            output=str(response.content),
            print_results=True,
            print_summary=True,
        )


    if __name__ == "__main__":
        asyncio.run(main())

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
    python agent_as_judge_async.py
    ```
  </Step>
</Steps>
