# Slack Reasoning Finance Agent

**Source:** https://docs.agno.com/agent-os/usage/interfaces/slack/reasoning-agent.md
**Section:** Docs

**Description:** Slack agent with advanced reasoning and financial analysis capabilities

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Slack Reasoning Finance Agent

> Slack agent with advanced reasoning and financial analysis capabilities

## Code

```python cookbook/os/interfaces/slack/reasoning_agent.py theme={null}
from agno.agent import Agent
from agno.db.sqlite.sqlite import SqliteDb
from agno.models.anthropic.claude import Claude
from agno.os.app import AgentOS
from agno.os.interfaces.slack.slack import Slack
from agno.tools.thinking import ThinkingTools
from agno.tools.yfinance import YFinanceTools

agent_db = SqliteDb(session_table="agent_sessions", db_file="tmp/persistent_memory.db")

reasoning_finance_agent = Agent(
    name="Reasoning Finance Agent",
    model=Claude(id="claude-3-7-sonnet-latest"),
    db=agent_db,
    tools=[
        ThinkingTools(add_instructions=True),
        YFinanceTools(
            stock_price=True,
            analyst_recommendations=True,
            company_info=True,
            company_news=True,
        ),
    ],
    instructions="Use tables to display data. When you use thinking tools, keep the thinking brief.",
    add_datetime_to_context=True,
    markdown=True,
)

agent_os = AgentOS(
    agents=[reasoning_finance_agent],
    interfaces=[Slack(agent=reasoning_finance_agent)],
)
app = agent_os.get_app()

if __name__ == "__main__":
    agent_os.serve(app="reasoning_agent:app", reload=True)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set Environment Variables">
    ```bash  theme={null}
    export SLACK_TOKEN=xoxb-your-bot-user-token
    export SLACK_SIGNING_SECRET=your-signing-secret
    export ANTHROPIC_API_KEY=your-anthropic-api-key
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno yfinance
    ```
  </Step>

  <Step title="Run Example">
    ```bash  theme={null}
    python cookbook/os/interfaces/slack/reasoning_agent.py
    ```
  </Step>
</Steps>

## Key Features

* **Advanced Reasoning**: ThinkingTools for step-by-step financial analysis
* **Real-time Data**: Stock prices, analyst recommendations, company news
* **Claude Powered**: Superior analytical and reasoning capabilities
* **Slack Integration**: Works in channels and direct messages
* **Structured Output**: Well-formatted tables and financial insights
