# Code Execution Tool

**Source:** https://docs.agno.com/models/providers/native/anthropic/usage/code-execution.md
**Section:** Docs

**Description:** Execute Python code in a sandboxed environment with Anthropic's code execution tool.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Code Execution Tool

> Execute Python code in a sandboxed environment with Anthropic's code execution tool.

With Anthropic's [code execution tool](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/code-execution-tool), your model can execute Python code in a secure, sandboxed environment.
This is useful for your model to perform tasks as analyzing data, creating visualizations, or performing complex calculations.

## Working example

```python  theme={null}
from agno.agent import Agent
from agno.models.anthropic import Claude

agent = Agent(
    model=Claude(
        id="claude-sonnet-4-20250514",
        betas=["code-execution-2025-05-22"],
    ),
    tools=[
        {
            "type": "code_execution_20250522",
            "name": "code_execution",
        }
    ],
    markdown=True,
)

agent.print_response(
    "Calculate the mean and standard deviation of [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]",
    stream=True,
)
```
