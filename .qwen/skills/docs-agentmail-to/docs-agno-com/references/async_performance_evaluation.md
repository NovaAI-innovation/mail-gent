# Async Performance Evaluation

**Source:** https://docs.agno.com/evals/performance/usage/performance-async.md
**Section:** Docs

**Description:** Example showing how to run performance evaluations on async functions.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Async Performance Evaluation

> Example showing how to run performance evaluations on async functions.

<Steps>
  <Step title="Create a Python file">
    ```python performance_async.py theme={null}
    """This example shows how to run a Performance evaluation on an async function."""

    import asyncio

    from agno.agent import Agent
    from agno.eval.performance import PerformanceEval
    from agno.models.openai import OpenAIResponses


    # Simple async function to run an Agent.
    async def arun_agent():
        agent = Agent(
            model=OpenAIResponses(id="gpt-5.2"),
            system_message="Be concise, reply with one sentence.",
        )
        response = await agent.arun("What is the capital of France?")
        return response


    performance_eval = PerformanceEval(func=arun_agent, num_iterations=10)

    # Because we are evaluating an async function, we use the arun method.
    asyncio.run(performance_eval.arun(print_summary=True, print_results=True))
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
    python performance_async.py
    ```
  </Step>
</Steps>
