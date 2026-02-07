# Redis for Agent

**Source:** https://docs.agno.com/database/providers/redis/usage/redis-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Redis for Agent

Agno supports using Redis as a storage backend for Agents using the `RedisDb` class.

## Usage

### Run Redis

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **Redis** on port **6379** using:

```bash  theme={null}
docker run -d \
  --name my-redis \
  -p 6379:6379 \
  redis
```

```python redis_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.base import SessionType
from agno.db.redis import RedisDb
from agno.tools.hackernews import HackerNewsTools

# Initialize Redis db (use the right db_url for your setup)
db = RedisDb(db_url="redis://localhost:6379")

# Create agent with Redis db
agent = Agent(
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
)

agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")

# Verify db contents
print("\nVerifying db contents...")
all_sessions = db.get_sessions(session_type=SessionType.AGENT)
print(f"Total sessions in Redis: {len(all_sessions)}")

if all_sessions:
    print("\nSession details:")
    session = all_sessions[0]
    print(f"The stored session: {session}")

```

## Params

<Snippet file="db-redis-params.mdx" />
