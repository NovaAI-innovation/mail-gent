# Gemini with Reasoning Tools

**Source:** https://docs.agno.com/reasoning/usage/tools/gemini-reasoning-tools.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Gemini with Reasoning Tools

<Steps>
  <Step title="Add the following code to your Python file">
    ```python gemini_reasoning_tools.py theme={null}
    from agno.agent import Agent
    from agno.models.google import Gemini
    from agno.tools.reasoning import ReasoningTools
    from agno.tools.hackernews import HackerNewsTools

    reasoning_agent = Agent(
        model=Gemini(id="gemini-2.5-pro-preview-03-25"),
        tools=[
            ReasoningTools(
                think=True,
                analyze=True,
                add_instructions=True,
            ),
            HackerNewsTools(),
        ],
        instructions="Use tables where possible",
        stream_events=True,
            markdown=True,
        debug_mode=True,
    )
    reasoning_agent.print_response(
        "Write a report comparing NVDA to TSLA.", show_full_reasoning=True
    )
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno google-genai ddgs
    ```
  </Step>

  <Step title="Export your Google API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export GOOGLE_API_KEY="your_google_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:GOOGLE_API_KEY="your_google_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python gemini_reasoning_tools.py
    ```
  </Step>
</Steps>
