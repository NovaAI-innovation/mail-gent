# What are Workflows?

**Source:** https://docs.agno.com/workflows/overview.md
**Section:** Docs

**Description:** Workflows orchestrate agents, teams, and functions through defined steps for repeatable tasks.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# What are Workflows?

> Workflows orchestrate agents, teams, and functions through defined steps for repeatable tasks.

A Workflow orchestrates agents, teams, and functions as a collection of steps. Steps can run sequentially, in parallel, in loops, or conditionally based on results. Output from each step flows to the next, creating a predictable pipeline for complex tasks.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=a308215dbae7c8e9050d03af47cfcf1b" alt="Workflows flow diagram" data-og-width="2994" width="2994" data-og-height="756" height="756" data-path="images/workflows-flow-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=280&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=36da448838231c986ea6fbee6cd20adf 280w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=560&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=2f79f8986f962ceed254128c04e2fff0 560w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=840&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=602db868a58a7ebadfb6849d783dacdf 840w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=1100&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=79ab80554e556943fad1bb1c54c23c1b 1100w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=1650&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=0c06010680d6e281b4ca6f90f8febc23 1650w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow-light.png?w=2500&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=6195335508ec97552803e2920695044d 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=e9ef16c48420b7eee9312561ab56098e" alt="Workflows flow diagram" data-og-width="2994" width="2994" data-og-height="756" height="756" data-path="images/workflows-flow.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=280&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=cb8faae1ea504803ff761ae3b89c51fb 280w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=560&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=498fe144844ce93806c7f590823ae666 560w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=840&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=e8bd51333fbf023524a636d579f489f2 840w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=1100&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=f4447ccd6c0c84f2ca104eb2ce7b560b 1100w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=1650&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=5a6c0f92fc29f107e4249432216a6b0f 1650w, https://mintcdn.com/agno-v2/JYIBgMrzFEujZh3_/images/workflows-flow.png?w=2500&fit=max&auto=format&n=JYIBgMrzFEujZh3_&q=85&s=0192f698b51c565c3efd9259472c8750 2500w" />

## Your First Workflow

Here's a simple workflow that takes a topic, researches it, and writes an article:

```python  theme={null}
from agno.agent import Agent
from agno.workflow import Workflow
from agno.tools.hackernews import HackerNewsTools

researcher = Agent(
    name="Researcher",
    instructions="Find relevant information about the topic",
    tools=[HackerNewsTools()]
)

writer = Agent(
    name="Writer",
    instructions="Write a clear, engaging article based on the research"
)

content_workflow = Workflow(
    name="Content Creation",
    steps=[researcher, writer]
)

content_workflow.print_response("Write an article about AI trends", stream=True)
```

## When to Use Workflows

Use a workflow when:

* You need predictable, repeatable execution
* Tasks have clear sequential steps with defined inputs and outputs
* You want audit trails and consistent results across runs

Use a [Team](/teams/overview) when you need flexible, collaborative problem-solving where agents coordinate dynamically.

## What Can Be a Step?

| Step Type    | Description                                                 |
| ------------ | ----------------------------------------------------------- |
| **Agent**    | Individual AI executor with specific tools and instructions |
| **Team**     | Coordinated group of agents for complex sub-tasks           |
| **Function** | Custom Python function for specialized logic                |

## Controlling Workflows

Workflows support conditional logic, parallel execution, loops, and conversational interactions. See the guides below for details.

## Guides

<CardGroup cols={3}>
  <Card title="Build Workflows" icon="wrench" iconType="duotone" href="/workflows/building-workflows">
    Define steps, inputs, and outputs.
  </Card>

  <Card title="Run Workflows" icon="user-robot" iconType="duotone" href="/workflows/running-workflows">
    Execute workflows and handle responses.
  </Card>

  <Card title="Conversational Workflows" icon="comments" iconType="duotone" href="/workflows/conversational-workflows">
    Enable chat interactions on your workflows.
  </Card>
</CardGroup>

## Developer Resources

* [Workflow examples](/cookbook/workflows/overview)
* [Workflow reference](/reference/workflows/workflow)
