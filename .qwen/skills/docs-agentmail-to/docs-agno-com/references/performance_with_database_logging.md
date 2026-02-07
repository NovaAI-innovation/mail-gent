# Performance with Database Logging

**Source:** https://docs.agno.com/evals/performance/usage/performance-db-logging.md
**Section:** Docs

**Description:** Example showing how to store performance evaluation results in the database.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Performance with Database Logging

> Example showing how to store performance evaluation results in the database.

<Steps>
  <Step title="Create a Python file">
    ```python performance_db_logging.py theme={null}
    """Example showing how to store evaluation results in the database."""

    from agno.agent import Agent
    from agno.db.postgres.postgres import PostgresDb
    from agno.eval.performance import PerformanceEval
    from agno.models.openai import OpenAIResponses


    # Simple function to run an agent which performance we will evaluate
    def run_agent():
        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            system_message="Be concise, reply with one sentence.",
        )
        response = agent.run("What is the capital of France?")
        print(response.content)
        return response


    # Setup the database
    db_url = "postgresql+psycopg://ai:ai@localhost:5432/ai"
    db = PostgresDb(db_url=db_url, eval_table="eval_runs_cookbook")

    simple_response_perf = PerformanceEval(
        db=db,  # Pass the database to the evaluation. Results will be stored in the database.
        name="Simple Performance Evaluation",
        func=run_agent,
        num_iterations=1,
        warmup_runs=0,
    )

    if __name__ == "__main__":
        simple_response_perf.run(print_results=True, print_summary=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno psycopg
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
    python performance_db_logging.py
    ```
  </Step>
</Steps>
