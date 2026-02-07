# Performance on Agent Instantiation

**Source:** https://docs.agno.com/evals/performance/usage/performance-agent-instantiation.md
**Section:** Docs

**Description:** Example showing how to analyze the runtime and memory usage of an Agent.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Performance on Agent Instantiation

> Example showing how to analyze the runtime and memory usage of an Agent.

<Steps>
  <Step title="Create a Python file">
    ```python performance_agent_instantiation.py theme={null}
    """Run `uv pip install agno openai` to install dependencies."""

    from agno.agent import Agent
    from agno.eval.performance import PerformanceEval


    def instantiate_agent():
        return Agent(system_message="Be concise, reply with one sentence.")


    instantiation_perf = PerformanceEval(
        name="Instantiation Performance", func=instantiate_agent, num_iterations=1000
    )

    if __name__ == "__main__":
        instantiation_perf.run(print_results=True, print_summary=True)
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
    python performance_agent_instantiation.py
    ```
  </Step>
</Steps>
