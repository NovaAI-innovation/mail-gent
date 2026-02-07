# Performance on Agent with Storage

**Source:** https://docs.agno.com/evals/performance/usage/performance-with-storage.md
**Section:** Docs

**Description:** Example showing how to analyze the runtime and memory usage of an Agent that is using storage.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Performance on Agent with Storage

> Example showing how to analyze the runtime and memory usage of an Agent that is using storage.

<Steps>
  <Step title="Create a Python file">
    ```python performance_with_storage.py theme={null}
    """Run `uv pip install openai agno` to install dependencies."""

    from agno.agent import Agent
    from agno.db.sqlite import SqliteDb
    from agno.eval.performance import PerformanceEval
    from agno.models.openai import OpenAIResponses

    db = SqliteDb(db_file="tmp/storage.db")


    def run_agent():
        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            system_message="Be concise, reply with one sentence.",
            add_history_to_context=True,
            db=db,
        )
        response_1 = agent.run("What is the capital of France?")
        print(response_1.content)

        response_2 = agent.run("How many people live there?")
        print(response_2.content)

        return response_2.content


    response_with_storage_perf = PerformanceEval(
        name="Storage Performance",
        func=run_agent,
        num_iterations=1,
        warmup_runs=0,
    )

    if __name__ == "__main__":
        response_with_storage_perf.run(print_results=True, print_summary=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
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
    python performance_with_storage.py
    ```
  </Step>
</Steps>
