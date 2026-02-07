# LangDB

**Source:** https://docs.agno.com/observability/langdb.md
**Section:** Docs

**Description:** Integrate Agno with LangDB to trace agent execution, tool calls, and gain comprehensive observability into your agent's performance.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# LangDB

> Integrate Agno with LangDB to trace agent execution, tool calls, and gain comprehensive observability into your agent's performance.

## Integrating Agno with LangDB

[LangDB](https://langdb.ai/) provides an AI Gateway platform for comprehensive observability and tracing of AI agents and LLM interactions. By integrating Agno with LangDB, you can gain full visibility into your agent's operations, including agent runs, tool calls, team interactions, and performance metrics.

For detailed integration instructions, see the [LangDB Agno documentation](https://docs.langdb.ai/getting-started/working-with-agent-frameworks/working-with-agno).

<Frame caption="LangDB Finance Team Trace">
  <img src="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=12aaf8fd6e3e9ce0dcca4e7bd0da9c43" style={{ borderRadius: '10px', width: '100%', maxWidth: '800px' }} alt="langdb-agno finance team observability" data-og-width="1623" width="1623" data-og-height="900" height="900" data-path="images/langdb-finance-trace.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=280&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=44bb9cf4c423a327b5459917cd3562cb 280w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=560&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=a2589678cacdac15c3b5c8dc21903189 560w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=840&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=b3aeeed6a9e129f4465d41d2e9e75929 840w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=1100&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=d803a20ad4a20d1871212d0c23156624 1100w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=1650&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=3f5eb5fa7780f3c740331550747b190b 1650w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-trace.png?w=2500&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=a397f1a8bb1d2e1ef366866ec6484a04 2500w" />
</Frame>

## Prerequisites

1. **Install Dependencies**

   Ensure you have the necessary packages installed:

   ```bash  theme={null}
   uv pip install agno 'pylangdb[agno]'
   ```

2. **Setup LangDB Account**

   * Sign up for an account at [LangDB](https://app.langdb.ai/signup)
   * Create a new project in the LangDB dashboard
   * Obtain your API key and Project ID from the project settings

3. **Set Environment Variables**

   Configure your environment with the LangDB credentials:

   ```bash  theme={null}
   export LANGDB_API_KEY="<your_langdb_api_key>"
   export LANGDB_PROJECT_ID="<your_langdb_project_id>"
   ```

## Sending Traces to LangDB

### Example: Basic Agent Setup

This example demonstrates how to instrument your Agno agent with LangDB tracing.

```python  theme={null}
from pylangdb.agno import init

# Initialize LangDB tracing - must be called before creating agents
init()

from agno.agent import Agent
from agno.models.langdb import LangDB
from agno.tools.hackernews import HackerNewsTools

# Create agent with LangDB model (uses environment variables automatically)
agent = Agent(
    name="Web Research Agent",
    model=LangDB(id="openai/gpt-4.1"),
    tools=[HackerNewsTools()],
    instructions="Answer questions using web search and provide comprehensive information"
)

# Use the agent
response = agent.run("What are the latest developments in AI agents?")
print(response)
```

### Example: Multi-Agent Team Coordination

For more complex workflows, you can use Agno's `Team` class with LangDB tracing:

```python  theme={null}
from pylangdb.agno import init
init()

from agno.agent import Agent
from agno.team import Team
from agno.models.langdb import LangDB
from agno.tools.hackernews import HackerNewsTools
from agno.tools.yfinance import YFinanceTools

# Research Agent
web_agent = Agent(
    name="Market Research Agent",
    model=LangDB(id="openai/gpt-4.1"),
    tools=[HackerNewsTools()],
    instructions="Research current market conditions and news"
)

# Financial Analysis Agent
finance_agent = Agent(
    name="Financial Analyst",
    model=LangDB(id="xai/grok-4"),
    tools=[YFinanceTools(stock_price=True, company_info=True)],
    instructions="Perform quantitative financial analysis"
)

# Coordinated Team
reasoning_team = Team(
    name="Finance Reasoning Team",
    model=LangDB(id="xai/grok-4"),
    members=[web_agent, finance_agent],
    instructions=[
        "Collaborate to provide comprehensive financial insights",
        "Consider both fundamental analysis and market sentiment"
    ]
)

# Execute team workflow
reasoning_team.print_response("Analyze Apple (AAPL) investment potential")
```

## Sample Trace

View a complete example trace in the LangDB dashboard: [Finance Reasoning Team Trace](https://app.langdb.ai/sharing/threads/73c91c58-eab7-4c6b-afe1-5ab6324f1ada)

<Frame caption="LangDB Finance Team Thread">
  <img src="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=177481792ff1b6fcdc03d464b62f7711" style={{ borderRadius: '10px', width: '100%', maxWidth: '800px' }} alt="langdb-agno finance team observability" data-og-width="1241" width="1241" data-og-height="916" height="916" data-path="images/langdb-finance-thread.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=280&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=13536f1cb8949e0e540505a137e8c978 280w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=560&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=2783572ef55c1d8645c2f9dc34c31809 560w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=840&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=d08349da04673fd7f1f358f0201cfd55 840w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=1100&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=b13d7216f599fef647e6f1f705198368 1100w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=1650&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=0124f22d2915636b0086f19f628515f3 1650w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/langdb-finance-thread.png?w=2500&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=0470d1883900d3fc2e0e4d2515417291 2500w" />
</Frame>

## Advanced Features

### LangDB Capabilities

* **Virtual Models**: Save, share, and reuse model configurations—combining prompts, parameters, tools, and routing logic into a single named unit for consistent behavior across apps
* **MCP Support**: Enhanced tool capabilities through Model Context Protocol servers
* **Multi-Provider**: Support for OpenAI, Anthropic, Google, xAI, and other providers

## Notes

* **Initialization Order**: Always call `init()` before creating any Agno agents or teams
* **Environment Variables**: With `LANGDB_API_KEY` and `LANGDB_PROJECT_ID` set, you can create models with just `LangDB(id="model_name")`

## Resources

* [LangDB Documentation](https://docs.langdb.ai/)
* [Building a Reasoning Finance Team Guide](https://docs.langdb.ai/guides/building-agents/building-a-reasoning-finance-team-with-agno)
* [LangDB GitHub Samples](https://github.com/langdb/langdb-samples/tree/main/examples/agno)
* [LangDB Dashboard](https://app.langdb.ai/)

By following these steps, you can effectively integrate Agno with LangDB, enabling comprehensive observability and monitoring of your AI agents.
