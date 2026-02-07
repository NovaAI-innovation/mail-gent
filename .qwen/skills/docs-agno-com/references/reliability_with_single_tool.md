# Reliability with Single Tool

**Source:** https://docs.agno.com/evals/reliability/usage/basic.md
**Section:** Docs

**Description:** Example showing how to assert an Agent is making the expected tool calls.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Reliability with Single Tool

> Example showing how to assert an Agent is making the expected tool calls.

<Steps>
  <Step title="Create a Python file">
    ```python basic.py theme={null}
    from typing import Optional

    from agno.agent import Agent
    from agno.eval.reliability import ReliabilityEval, ReliabilityResult
    from agno.models.openai import OpenAIResponses
    from agno.run.agent import RunOutput
    from agno.tools.calculator import CalculatorTools


    def factorial():
        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            tools=[CalculatorTools()],
        )
        response: RunOutput = agent.run("What is 10!?")
        evaluation = ReliabilityEval(
            name="Tool Call Reliability",
            agent_response=response,
            expected_tool_calls=["factorial"],
        )
        result: Optional[ReliabilityResult] = evaluation.run(print_results=True)
        result.assert_passed()


    if __name__ == "__main__":
        factorial()
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
    python basic.py
    ```
  </Step>
</Steps>
