# In-Memory Storage for Agents

**Source:** https://docs.agno.com/database/providers/in-memory/usage/in-memory-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# In-Memory Storage for Agents

Example using `InMemoryDb` with agent.

## Usage

```python  theme={null}
from agno.agent import Agent
from agno.db.in_memory import InMemoryDb

# Setup in-memory database
db = InMemoryDb()

# Create agent with database
agent = Agent(db=db)

# Agent sessions stored in memory
agent.print_response("Give me an easy dinner recipe")
```
