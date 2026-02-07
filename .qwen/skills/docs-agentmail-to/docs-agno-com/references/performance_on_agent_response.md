# Performance on Agent Response

**Source:** https://docs.agno.com/evals/performance/usage/performance-simple-response.md
**Section:** Docs

**Description:** Example showing how to analyze the runtime and memory usage of an Agent's run, given its response.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Performance on Agent Response

> Example showing how to analyze the runtime and memory usage of an Agent's run, given its response.

<Steps>
  <Step title="Create a Python file">
    ```python performance_simple_response.py theme={null}
    """Run `uv pip install openai agno memory_profiler` to install dependencies."""

    from agno.agent import Agent
    from agno.eval.performance import PerformanceEval
    from agno.models.openai import OpenAIResponses


    def run_agent():
        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            system_message="Be concise, reply with one sentence.",
        )

        response = agent.run("What is the capital of France?")
        print(f"Agent response: {response.content}")

        return response


    simple_response_perf = PerformanceEval(
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
    uv pip install -U openai agno memory_profiler
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
    python performance_simple_response.py
    ```
  </Step>
</Steps>
