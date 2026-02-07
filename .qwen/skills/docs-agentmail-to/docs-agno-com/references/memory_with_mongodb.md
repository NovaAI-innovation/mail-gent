# Memory with MongoDB

**Source:** https://docs.agno.com/memory/working-with-memories/mongodb-memory.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Memory with MongoDB

## Code

```python mem-mongodb-memory.py theme={null}
from agno.agent import Agent
from agno.db.mongo import MongoDb

# Setup MongoDb
db_url = "mongodb://localhost:27017"

db = MongoDb(db_url=db_url)

agent = Agent(
    db=db,
    update_memory_on_run=True,
)

agent.print_response("My name is John Doe and I like to play basketball on the weekends.")
agent.print_response("What's do I do in weekends?")
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set environment variables">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai pymongo
    ```
  </Step>

  <Step title="Run Example">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
      python mem-mongodb-memory.py
      ```

      ```bash Windows theme={null}
      python mem-mongodb-memory.py
      ```
    </CodeGroup>
  </Step>
</Steps>
