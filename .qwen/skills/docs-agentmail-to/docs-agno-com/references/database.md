# Database

**Source:** https://docs.agno.com/database/overview.md
**Section:** Docs

**Description:** Give your agents persistent storage for sessions, context, memory and knowledge.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Database

> Give your agents persistent storage for sessions, context, memory and knowledge.

Databases are a foundational part of agent engineering. Add a database to your agent and you get persistent storage for sessions, context, memory, learnings, and evaluation datasets.

* **Chat history.** Include previous messages in context for multi-turn conversations.
* **Session persistence.** Store session information and conversation history across requests.
* **State management.** Store internal agent state across runs. Critical for planning agents.
* **Context control.** Summarize, compress, enrich, and prune context for better responses.
* **Memory and knowledge.** Store user-level facts, searchable knowledge, decision traces, and learned insights.
* **Tracing and evaluation.** Store detailed traces for debugging, monitoring, and building evaluation datasets.
* **Data ownership.** No third-party dependencies. Query your own database. Build evaluation datasets, extract few-shot examples, flag low-quality responses for review.

This is how good software is built. Agents are no different.

## Quick Start

```python  theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb

agent = Agent(
    db=SqliteDb(db_file="agent.db"),
    add_history_to_context=True,
    num_history_runs=3,
)

# First message
agent.print_response("I'm working on a Python API project", session_id="dev_session")

# Later — agent remembers the context
agent.print_response("What testing framework should I use?", session_id="dev_session")
```

The agent now persists sessions and includes the last 3 runs in every request.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=aa1aa1bf3b18e6d008bb7f1e17b3f539" alt="Database storage overview" style={{ maxWidth: '100%', transform: 'scale(1.1)' }} data-og-width="3741" width="3741" data-og-height="906" height="906" data-path="images/storage-overview-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0023c1e7e592ae9b779bbf99c23d5289 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0737ecbdf0c0114eb46283bac2da9452 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=19c47c18c749b0725fd22d07296ef4f6 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=04ce3da485e8c4bd0750f7146296ad0e 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7f65a9a54f14f0368da8cbe008dc3981 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=97fcf30feacd1e264ea90d71efa06ed6 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=18c17269a4ced29b5a160768cc86e2d6" alt="Database storage overview" style={{ maxWidth: '100%', transform: 'scale(1.1)' }} data-og-width="3741" width="3741" data-og-height="906" height="906" data-path="images/storage-overview-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=f0d7c601809b3f6874f90b2b45b4be96 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=814c6ba4c626e21a645fa54c26dd5c25 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=715ac7ca26004ca669051e5797be9f13 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7045e13a52b0ffbd6fcf45f48bffa7c8 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=3bebd2a3ef5ea85c99cb85a0c490a53c 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/storage-overview-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c083d35f8fe5acfb87feac38e21eaae4 2500w" />

## Guides

<CardGroup cols={2}>
  <Card title="Chat History" icon="clock-rotate-left" iconType="duotone" href="/database/chat-history">
    Include previous messages in context for multi-turn conversations.
  </Card>

  <Card title="Session Storage" icon="database" iconType="duotone" href="/database/session-storage">
    Store and retrieve session data from your database.
  </Card>

  <Card title="Session Summaries" icon="compress" iconType="duotone" href="/sessions/session-summaries">
    Condense long conversations to manage token costs.
  </Card>

  <Card title="Storage Control" icon="sliders" iconType="duotone" href="/sessions/persisting-sessions/storage-control">
    Choose what gets persisted to your database.
  </Card>
</CardGroup>

## Works With Teams and Workflows

Storage works identically across Agents, Teams, and Workflows:

```python  theme={null}
from agno.team import Team
from agno.workflow import Workflow
from agno.db.postgres import PostgresDb

db = PostgresDb(db_url="postgresql://user:pass@localhost:5432/mydb")

team = Team(db=db, ...)
workflow = Workflow(db=db, ...)
```

## Supported Databases

Agno supports 13+ databases for session storage. Use SQLite for development, PostgreSQL for production. [View all supported databases](/database/providers/overview).

## Async Support

For async applications, use the async database classes:

```python  theme={null}
from agno.agent import Agent
from agno.db.postgres import AsyncPostgresDb

agent = Agent(
    db=AsyncPostgresDb(db_url="postgresql+psycopg_async://..."),
)
```

## Troubleshooting

<Accordion title="MissingGreenlet exception">
  You're using a synchronous engine with an async database class. Use `create_async_engine` from `sqlalchemy.ext.asyncio`.
</Accordion>

<Accordion title="AsyncContextNotStarted exception">
  You're using an async engine with a synchronous database class. Use `create_engine` from `sqlalchemy`.
</Accordion>
