# Groq DeepSeek R1

**Source:** https://docs.agno.com/reasoning/usage/models/groq/groq.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Groq DeepSeek R1

<Steps>
  <Step title="Add the following code to your Python file">
    ```python groq.py theme={null}
    from agno.agent import Agent
    from agno.models.groq import Groq

    agent = Agent(
        model=Groq(
            id="deepseek-r1-distill-llama-70b", temperature=0.6, max_tokens=1024, top_p=0.95
        ),
        markdown=True,
    )
    agent.print_response("9.11 and 9.9 -- which is bigger?", stream=True)
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno groq
    ```
  </Step>

  <Step title="Export your Groq API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export GROQ_API_KEY="your_groq_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:GROQ_API_KEY="your_groq_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python groq.py
    ```
  </Step>
</Steps>
