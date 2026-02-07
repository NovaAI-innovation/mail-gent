# Agent as Judge with Custom Evaluator

**Source:** https://docs.agno.com/evals/agent-as-judge/usage/agent-as-judge-custom-evaluator.md
**Section:** Docs

**Description:** Using a custom evaluator agent with specific instructions

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent as Judge with Custom Evaluator

> Using a custom evaluator agent with specific instructions

This example demonstrates using a custom evaluator agent with specific instructions for evaluation.

<Steps>
  <Step title="Add the following code to your Python file">
    ```python agent_as_judge_custom_evaluator.py theme={null}
    from agno.agent import Agent
    from agno.eval.agent_as_judge import AgentAsJudgeEval
    from agno.models.openai import OpenAIResponses

    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        instructions="Explain technical concepts simply.",
    )

    response = agent.run("What is machine learning?")

    # Create a custom evaluator with specific instructions
    custom_evaluator = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        description="Strict technical evaluator",
        instructions="You are a strict evaluator. Only give high scores to exceptionally clear and accurate explanations.",
    )

    evaluation = AgentAsJudgeEval(
        name="Technical Accuracy",
        criteria="Explanation must be technically accurate and comprehensive",
        scoring_strategy="numeric",
        threshold=8,
        evaluator_agent=custom_evaluator,
    )

    result = evaluation.run(
        input="What is machine learning?",
        output=str(response.content),
    )

    print(f"Score: {result.results[0].score}/10")
    print(f"Passed: {result.results[0].passed}")

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
    python agent_as_judge_custom_evaluator.py
    ```
  </Step>
</Steps>
