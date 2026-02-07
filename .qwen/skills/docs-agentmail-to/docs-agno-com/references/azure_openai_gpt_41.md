# Azure OpenAI GPT 4.1

**Source:** https://docs.agno.com/reasoning/usage/models/azure-openai/reasoning-model-gpt4-1.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Azure OpenAI GPT 4.1

<Steps>
  <Step title="Add the following code to your Python file">
    ```python azure_openai.py theme={null}
    from agno.agent import Agent
    from agno.models.azure.openai_chat import AzureOpenAI

    agent = Agent(
        model=AzureOpenAI(id="gpt-5.2"), 
        reasoning_model=AzureOpenAI(id="gpt-5.2")
    )
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
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Set your Azure OpenAI credentials">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export AZURE_OPENAI_API_KEY="xxx"
        export AZURE_OPENAI_ENDPOINT="xxx"
        export AZURE_DEPLOYMENT="xxx"
      ```

      ```bash Windows theme={null}
        $Env:AZURE_OPENAI_API_KEY="xxx"
        $Env:AZURE_OPENAI_ENDPOINT="xxx"
        $Env:AZURE_DEPLOYMENT="xxx"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python azure_openai.py
    ```
  </Step>
</Steps>
