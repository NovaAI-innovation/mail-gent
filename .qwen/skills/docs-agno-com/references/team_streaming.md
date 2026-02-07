# Team Streaming

**Source:** https://docs.agno.com/teams/usage/streaming.md
**Section:** Docs

**Description:** Stream responses from a team in real-time.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Team Streaming

> Stream responses from a team in real-time.

Stream responses from a team with `stream=True` for real-time output as the team works.

<Steps>
  <Step title="Create a Python file">
    ```python streaming_team.py theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses
    from agno.team import Team
    from agno.tools.hackernews import HackerNewsTools
    from agno.tools.yfinance import YFinanceTools

    news_agent = Agent(
        name="News Agent",
        model=OpenAIResponses(id="gpt-5.2"),
        role="Gets trending tech stories from HackerNews.",
        tools=[HackerNewsTools()],
    )

    finance_agent = Agent(
        name="Finance Agent",
        model=OpenAIResponses(id="gpt-5.2"),
        role="Gets stock prices and financial data.",
        tools=[YFinanceTools()],
    )

    team = Team(
        name="Research Team",
        model=OpenAIResponses(id="gpt-5.2"),
        members=[news_agent, finance_agent],
        markdown=True,
        show_members_responses=True,
    )

    # Stream the response
    team.print_response(
        "What are the trending AI stories and how is NVDA stock doing?",
        stream=True,
    )
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai yfinance
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

  <Step title="Run Team">
    ```bash  theme={null}
    python streaming_team.py
    ```
  </Step>
</Steps>
