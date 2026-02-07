# Tool Call Limit

**Source:** https://docs.agno.com/tools/tool-call-limit.md
**Section:** Docs

**Description:** Limit the number of tool calls an agent can make.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Tool Call Limit

> Limit the number of tool calls an agent can make.

Limiting the number of tool calls an Agent can make is useful to prevent loops and have better control over costs and performance.

Doing this is very simple with Agno. You just need to pass the `tool_call_limit` parameter when initializing your Agent or Team.

For example:

```python  theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.yfinance import YFinanceTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[YFinanceTools(company_news=True, cache_results=True)],
    tool_call_limit=1, # The Agent will not perform more than one tool call.
)

# The first tool call will be performed. The second one will fail gracefully.
agent.print_response(
    "Find me the current price of TSLA, then after that find me the latest news about Tesla.",
    stream=True,
)

```

<Tip>
  Important to consider:

  * If the Agent tries to run a number of tool calls that exceeds the limit **all at once**, the limit will remain effective. Only as many tool calls as allowed will be performed.
  * The limit is enforced **across a full run**, and not per individual requests triggered by the Agent.
</Tip>
