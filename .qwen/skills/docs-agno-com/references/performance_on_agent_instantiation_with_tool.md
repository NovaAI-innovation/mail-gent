# Performance on Agent Instantiation with Tool

**Source:** https://docs.agno.com/evals/performance/usage/performance-instantiation-with-tool.md
**Section:** Docs

**Description:** Example showing how to analyze the runtime and memory usage of an Agent that is using tools.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Performance on Agent Instantiation with Tool

> Example showing how to analyze the runtime and memory usage of an Agent that is using tools.

<Steps>
  <Step title="Create a Python file">
    ```python performance_instantiation_with_tool.py theme={null}
    """Run `uv pip install agno openai memory_profiler` to install dependencies."""

    from typing import Literal

    from agno.agent import Agent
    from agno.eval.performance import PerformanceEval
    from agno.models.openai import OpenAIResponses


    def get_weather(city: Literal["nyc", "sf"]):
        """Use this to get weather information."""
        if city == "nyc":
            return "It might be cloudy in nyc"
        elif city == "sf":
            return "It's always sunny in sf"


    tools = [get_weather]


    def instantiate_agent():
        return Agent(model=OpenAIResponses(id="gpt-5.2"), tools=tools)  # type: ignore


    instantiation_perf = PerformanceEval(
        name="Tool Instantiation Performance", func=instantiate_agent, num_iterations=1000
    )

    if __name__ == "__main__":
        instantiation_perf.run(print_results=True, print_summary=True)
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
    python performance_instantiation_with_tool.py
    ```
  </Step>
</Steps>
