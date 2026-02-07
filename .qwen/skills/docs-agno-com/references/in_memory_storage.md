# In-Memory Storage

**Source:** https://docs.agno.com/database/providers/in-memory/overview.md
**Section:** Docs

**Description:** Use in-memory storage for testing and development.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# In-Memory Storage

> Use in-memory storage for testing and development.

Agno supports using In-Memory storage with the `InMemoryDb` class. By doing this, you will be able to use all features that depend on having a database, without having to set one up.

<Warning>
  Using the In-Memory storage is not recommended for production applications.
  Use it for demos, testing and any other use case where you don't want to setup a database.
</Warning>

## Usage

```python  theme={null}
from agno.agent import Agent
from agno.db.in_memory import InMemoryDb

# Setup in-memory database
db = InMemoryDb()

# Create agent with database
agent = Agent(db=db)
```
