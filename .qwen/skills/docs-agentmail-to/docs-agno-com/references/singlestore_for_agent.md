# Singlestore for Agent

**Source:** https://docs.agno.com/database/providers/singlestore/usage/singlestore-for-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Singlestore for Agent

Agno supports using Singlestore as a storage backend for Agents using the `SingleStoreDb` class.

## Usage

Obtain the credentials for Singlestore from [here](https://portal.singlestore.com/)

```python singlestore_for_agent.py theme={null}
from os import getenv

from agno.agent import Agent
from agno.db.singlestore.singlestore import SingleStoreDb
from agno.tools.hackernews import HackerNewsTools

# Configure SingleStore DB connection
USERNAME = getenv("SINGLESTORE_USERNAME")
PASSWORD = getenv("SINGLESTORE_PASSWORD")
HOST = getenv("SINGLESTORE_HOST")
PORT = getenv("SINGLESTORE_PORT")
DATABASE = getenv("SINGLESTORE_DATABASE")

db_url = (
    f"mysql+pymysql://{USERNAME}:{PASSWORD}@{HOST}:{PORT}/{DATABASE}?charset=utf8mb4"
)

db = SingleStoreDb(db_url=db_url)

# Create an agent with SingleStore db
agent = Agent(
    db=db,
    tools=[HackerNewsTools()],
    add_history_to_context=True,
)
agent.print_response("How many people live in Canada?")
agent.print_response("What is their national anthem called?")

```

## Params

<Snippet file="db-singlestore-params.mdx" />
