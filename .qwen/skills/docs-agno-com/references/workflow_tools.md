# Workflow Tools

**Source:** https://docs.agno.com/workflows/workflow-tools.md
**Section:** Docs

**Description:** How to execute a workflow inside an Agent or Team

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Workflow Tools

> How to execute a workflow inside an Agent or Team

## Example

You can give a workflow to an Agent or Team to execute using `WorkflowTools`.

```python  theme={null}
from agno.agent import Agent    
from agno.models.openai import OpenAIResponses
from agno.tools.workflow import WorkflowTools

# Create your workflows...

workflow_tools = WorkflowTools(
    workflow=blog_post_workflow,
)

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[workflow_tools],
)

agent.print_response("Create a blog post on the topic: AI trends in 2024", stream=True)
```

See the [Workflow Tools](/tools/reasoning_tools/workflow-tools) documentation for more details.
