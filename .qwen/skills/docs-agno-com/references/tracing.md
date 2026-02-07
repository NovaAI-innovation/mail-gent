# Tracing

**Source:** https://docs.agno.com/tracing/overview.md
**Section:** Docs

**Description:** Gain deep visibility into your Agno agents with OpenTelemetry-based observability

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Tracing

> Gain deep visibility into your Agno agents with OpenTelemetry-based observability

<Badge icon="code-branch" color="orange">
  <Tooltip tip="Introduced in v2.3.5" cta="View release notes" href="https://github.com/agno-agi/agno/releases/tag/v2.3.5">v2.3.5</Tooltip>
</Badge>

In the systems you build with Agno, agents will make autonomous decisions, interact with external tools, and coordinate with each other in ways that aren't immediately visible from your recorded sessions alone. Observability is key to staying on top of what your agents are doing and how your system is performing.

**Agno Tracing** is the recommended way to introduce observability for your Agno agents, teams, and workflows.
It automatically captures all relevant execution details, helping you understand what your agents are doing, simplifying debugging and helping you optimize your system.

Tracing leverages [OpenTelemetry](https://opentelemetry.io/) to instrument the Agno agents and teams, capturing traces and spans.

<Frame caption="Traces stored in SQLite database viewed with AgentOS">
  <img src="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=0e007064a21a14cabadeed560a9c207a" alt="Traces viewed in AgentOS" data-og-width="2932" width="2932" data-og-height="1314" height="1314" data-path="images/traces-in-os.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=280&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=651a73bbca101d922693ec384ee47083 280w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=560&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=b4cb3fd081298932ffc2679447686574 560w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=840&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=5bc9389ffb66d6cf7047c41b15a40d87 840w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=1100&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=4f06c18c6b7189c26089ca56bbe432af 1100w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=1650&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=83cf8de1945335ee4e2ef71a400c29a3 1650w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-in-os.png?w=2500&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=682376786ba9a10592e684390a0f301e 2500w" />
</Frame>

## Why is Observability Important?

As your Agno system become more complex (Agents using multiple tools, making sequential decisions, and coordinating with other agents), understanding its behavior becomes challenging.

**Agno Tracing** solves this:

* **Debugging**: See exactly what went wrong when an agent fails
* **Performance**: Identify bottlenecks in agent execution
* **Cost Tracking**: Monitor token usage and API calls
* **Behavior Analysis**: Understand decision-making patterns
* **Audit Trail**: Track what agents did and why

<Note>
  All Agno Tracing data is stored in your own database. No tracing data will leave your system, or be sent to third parties: you are in complete control.
</Note>

## Understanding Traces and Spans

Think of tracing like a family tree for your agent's execution:

### Trace

A **trace** represents one complete agent execution from start to finish. Each trace has a unique `trace_id` that groups all related operations together.

### Span

A **span** is a single operation within that execution. Spans form a parent-child hierarchy:

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=9154b13c041f6fd5674224fda47065c0" alt="Traces vs spans diagram" data-og-width="1827" width="1827" data-og-height="930" height="930" data-path="images/traces-vs-spans-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=280&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=9cfde54b1f868542f84929eaa38d27a9 280w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=560&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=7ad28bf2fdaf0313bae5ef3fdfe97ae3 560w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=840&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=174cf3379538b44ba11efae87677fc78 840w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=1100&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=700830eaa494fa36c945ac0fc07c895b 1100w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=1650&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=dc52b7d0d20c4b2c96ec2991c22cee54 1650w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-light.png?w=2500&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=3ad50142e5cf8a6b7370f23ba508842b 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=c513cdba94b11c908653287085397bd0" alt="Traces vs spans diagram" data-og-width="1827" width="1827" data-og-height="930" height="930" data-path="images/traces-vs-spans-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=280&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=49fe1ffa407cab97107331cda9101ced 280w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=560&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=f8693e2efa8f079a6208d6a2dd947d37 560w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=840&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=0e0f880e9a920ad9b11150adcf4c7d22 840w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=1100&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=e24b518f77b3bfa4ffcd0ec0291e9078 1100w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=1650&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=7b0e4ceed3c629c174f9c4f3ef8f8693 1650w, https://mintcdn.com/agno-v2/gChHNQRMu2Gpq6Xe/images/traces-vs-spans-dark.png?w=2500&fit=max&auto=format&n=gChHNQRMu2Gpq6Xe&q=85&s=08d4acaa62b95a71966216809f102104 2500w" />

Each span captures:

* **What happened**: Operation name (e.g., `agent.run`, `model.response`)
* **When**: Start and end timestamps
* **Context**: Input arguments, outputs, token usage
* **Relationships**: Parent span, child spans
* **Metadata**: Agent ID, session ID, run ID

## What Gets Traced

Agno automatically captures:

| Operation               | What Gets Traced                                               |
| ----------------------- | -------------------------------------------------------------- |
| **Agent Runs**          | Every `agent.run()` or `agent.arun()` call with full context   |
| **Model Calls**         | LLM interactions including prompts, responses, and token usage |
| **Tool Executions**     | Tool invocations with arguments and results                    |
| **Team Operations**     | Team coordination and member agent runs                        |
| **Workflow Operations** | Workflow coordination and step runs                            |

## Key Features

* **Zero-Code Instrumentation**: No need to modify your agent code
* **Database Storage**: Traces stored in your Agno database (SQLite, PostgreSQL, etc.)
* **Flexible Querying**: Filter by agent, session, run, or time range
* **OpenTelemetry Standard**: Export to external tools like Arize Phoenix, Langfuse
* **Non-Blocking**: Tracing never slows down your agents
* **Configurable**: Adjust batch sizes and processing for your needs

## Quick Start

<Steps>
  <Step title="Install Dependencies">
    ```bash  theme={null}
    uv pip install -U opentelemetry-api opentelemetry-sdk openinference-instrumentation-agno
    ```
  </Step>

  <Step title="Enable Tracing">
    ```python  theme={null}
    from agno.tracing import setup_tracing
    from agno.db.sqlite import SqliteDb

    db = SqliteDb(db_file="tmp/traces.db")
    setup_tracing(db=db) # Call this once at startup
    ```
  </Step>

  <Step title="Run Your Agent">
    ```python  theme={null}
    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses

    agent = Agent(
        name="My Agent",
        model=OpenAIResponses(id="gpt-5.2"),
        instructions="You are a helpful assistant",
    )

    agent.run("Hello!")  # Automatically traced!
    ```
  </Step>

  <Step title="Query Traces">
    ```python  theme={null}
    traces, total = db.get_traces(agent_id=agent.id, limit=10)
    for trace in traces:
        print(f"{trace.name}: {trace.duration_ms}ms")
    ```
  </Step>
</Steps>

## Guides

<CardGroup cols={3}>
  <Card title="Basic Setup" icon="rocket" href="/tracing/basic-setup">
    Configure and enable tracing
  </Card>

  <Card title="Tracing in AgentOS" icon="rocket" href="/agent-os/tracing/overview">
    Trace your agents, teams, and workflows in AgentOS
  </Card>

  <Card title="DB Functions" icon="database" href="/tracing/db-functions">
    Query traces and spans from your database
  </Card>
</CardGroup>
