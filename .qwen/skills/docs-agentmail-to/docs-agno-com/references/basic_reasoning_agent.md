# Basic Reasoning Agent

**Source:** https://docs.agno.com/reasoning/usage/agents/basic-cot.md
**Section:** Docs

**Description:** Equip agents with chain-of-thought reasoning capabilities.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Basic Reasoning Agent

> Equip agents with chain-of-thought reasoning capabilities.

Example showing how to configure a basic Reasoning Agent, using the `reasoning=True` flag.

<Steps>
  <Step title="Add the following code to your Python file">
    ```python basic_cot.py theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses

    task = (
        "Analyze the key factors that led to the signing of the Treaty of Versailles in 1919. "
        "Discuss the political, economic, and social impacts of the treaty on Germany and how it "
        "contributed to the onset of World War II. Provide a nuanced assessment that includes "
        "multiple historical perspectives."
    )

    reasoning_agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        reasoning=True, # The Agent will be able to reason.
        markdown=True,
    )
    reasoning_agent.print_response(task, stream=True, show_full_reasoning=True)
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
    python basic_cot.py
    ```
  </Step>
</Steps>
