# Selecting Custom Table Names

**Source:** https://docs.agno.com/database/providers/selecting-tables.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Selecting Custom Table Names

Agno allows you to customize table names when using databases, providing flexibility in organizing your data storage.

## Usage

Specify custom table names when initializing your database connection.

```python selecting_tables.py theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb

# Setup the SQLite database with custom table names
db = SqliteDb(
    db_file="tmp/data.db",
    # Selecting which tables to use
    session_table="agent_sessions",
    memory_table="agent_memories",
    metrics_table="agent_metrics",
)

# Setup a basic agent with the SQLite database
agent = Agent(
    db=db,
    update_memory_on_run=True,
    add_history_to_context=True,
    add_datetime_to_context=True,
)

# The Agent sessions and runs will now be stored in SQLite with custom table names
agent.print_response("How many people live in Canada?")
agent.print_response("And in Mexico?")
agent.print_response("List my messages one by one")
```
