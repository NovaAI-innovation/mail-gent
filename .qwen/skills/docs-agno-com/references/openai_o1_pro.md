# OpenAI o1 pro

**Source:** https://docs.agno.com/reasoning/usage/models/openai/o1-pro.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# OpenAI o1 pro

<Steps>
  <Step title="Add the following code to your Python file">
    ```python openai.py theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses

    agent = Agent(model=OpenAIResponses(id="o1-pro"))
    agent.print_response(
        "Solve the trolley problem. Evaluate multiple ethical frameworks. "
        "Include an ASCII diagram of your solution.",
        stream=True,
    )
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

  <Step title="Run Agent">
    ```bash  theme={null}
    python openai.py
    ```
  </Step>
</Steps>
