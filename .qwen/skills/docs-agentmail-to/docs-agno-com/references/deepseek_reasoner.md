# DeepSeek Reasoner

**Source:** https://docs.agno.com/reasoning/usage/models/deepseek/deepseek-reasoner.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# DeepSeek Reasoner

<Steps>
  <Step title="Add the following code to your Python file">
    ```python deepseek_reasoner.py theme={null}
    from agno.agent import Agent
    from agno.models.deepseek import DeepSeek
    from agno.models.openai import OpenAIResponses

    task = (
        "You are a philosopher tasked with analyzing the classic 'Trolley Problem'. In this scenario, a runaway trolley "
        "is barreling down the tracks towards five people who are tied up and unable to move. You are standing next to "
        "a large stranger on a footbridge above the tracks. The only way to save the five people is to push this stranger "
        "off the bridge onto the tracks below. This will kill the stranger, but save the five people on the tracks. "
        "Should you push the stranger to save the five people? Provide a well-reasoned answer considering utilitarian, "
        "deontological, and virtue ethics frameworks. "
        "Include a simple ASCII art diagram to illustrate the scenario."
    )

    reasoning_agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        reasoning_model=DeepSeek(id="deepseek-reasoner"),
        markdown=True,
    )
    reasoning_agent.print_response(task, stream=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
    ```
  </Step>

  <Step title="Export your DeepSeek API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export DEEPSEEK_API_KEY="your_deepseek_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:DEEPSEEK_API_KEY="your_deepseek_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python deepseek.py
    ```
  </Step>
</Steps>
