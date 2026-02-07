# What are Tools?

**Source:** https://docs.agno.com/tools/overview.md
**Section:** Docs

**Description:** Tools are functions Agents call to interact with external systems.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# What are Tools?

> Tools are functions Agents call to interact with external systems.

Tools are what make Agents and Teams capable of real-world action. While using LLMs directly you can only generate text responses, Agents and Teams equipped with tools can interact with external systems and perform practical actions.

Some examples of actions that can be performed with tools are: searching the web, running SQL, sending an email or calling APIs.

Agno comes with 120+ pre-built toolkits, which you can use to give your Agents all kind of abilities. You can also write your own tools, to give your Agents even more capabilities. The general syntax is:

```python  theme={null}
import random

from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools import tool

def get_weather(city: str) -> str:
    """Get the weather for the given city.

    Args:
        city (str): The city to get the weather for.
    """

    # In a real implementation, this would call a weather API
    weather_conditions = ["sunny", "cloudy", "rainy", "snowy", "windy"]
    random_weather = random.choice(weather_conditions)

    return f"The weather in {city} is {random_weather}."

# To equipt our Agent with our tool, we simply pass it with the tools parameter
agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[get_weather],
    markdown=True,
)

# Our Agent will now be able to use our tool, when it deems it relevant
agent.print_response("What is the weather in San Francisco?", stream=True)
```

<Tip>
  In the example above, the `get_weather` function is a tool. When called, the tool result is shown in the output.
</Tip>

## How do tools work?

The heart of Agent execution is the LLM loop. The typical execution flow of the LLM loop is:

1. The agent sends the run context (system message, user message, chat history, etc) and tool definitions to the model.
2. The model responds with a message or a tool call.
3. If the model makes a tool call, the tool is executed and the result is returned to the model.
4. The model processes the updated context, repeating this loop until it produces a final message without any tool calls.
5. The agent returns this final response to the caller.

### Tool definitions

Agno automatically converts your tool functions into the required tool definition format for the model. Typically this is a JSON schema that describes the parameters and return type of the tool.

For example:

```python  theme={null}
def get_weather(city: str) -> str:
    """
    Get the weather for a given city.

    Args:
        city (str): The city to get the weather for.
    """
    return f"The weather in {city} is sunny."
```

This will be converted into the following tool definition:

```json  theme={null}
{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Get the weather for a given city.",
        "parameters": {
            "type": "object",
            "properties": {
                "city": {
                    "type": "string",
                    "description": "The city to get the weather for."
                }
            },
            "required": ["city"]
        }
    }
}
```

This tool definition is then sent to the model so that it knows how to call the tool when it is requested.
You'll notice as well that the `Args` section is automatically stripped from the definition, parsed and used to populate the definitions of individualproperties.

When using a Pydantic model in an argument of a tool function, Agno will automatically convert the model into the required tool definition format.

For example:

```python  theme={null}

from pydantic import BaseModel, Field

class GetWeatherRequest(BaseModel):
    city: str = Field(description="The city to get the weather for")

def get_weather(request: GetWeatherRequest) -> str:
    """
    Get the weather for a given city.

    Args:
        request (GetWeatherRequest): The request object containing the city to get the weather for.

    """
    return f"The weather in {request.city} is sunny."
```

This will be converted into the following tool definition:

```json  theme={null}
{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Get the weather for a given city.",
        "parameters": {
            "type": "object",
            "properties": {
              "request": {
                "type": "object",
                "properties": {
                  "city": {
                    "type": "string",
                    "description": "The city to get the weather for."
                  }
                },
                "required": ["city"]
              }
            },
            "required": ["request"]
        }
    }
}
```

<Tip>
  * Always create a docstring for your tool functions. Make sure to include the `Args` section and cover each of the arguments of the function.
  * Use sensible names for your tool functions. Remember this is directly used by the model to call the tool when it is requested.
</Tip>

### Tool Execution

When the model requests a tool call, the tool is executed and the result is returned to the model.

* A model can request multiple tool calls in a single response.
* When using `arun` to execute the agent or team, and the model requested multiple tool calls, the tools will be executed concurrently.

Agno Agents can execute multiple tools concurrently, allowing you to process function calls that the model makes efficiently. This is especially valuable when the functions involve time-consuming operations. It improves responsiveness and reduces overall execution time.

<Check>
  When you call `arun` or `aprint_response`, your tools will execute concurrently. If you provide synchronous functions as tools, they will execute concurrently on separate threads.
</Check>

<Note>
  Concurrent execution of tools requires a model that supports parallel function
  calling. For example, OpenAI models have a `parallel_tool_calls` parameter
  (enabled by default) that allows multiple tool calls to be requested and
  executed simultaneously.
</Note>

<Accordion title="Async Execution Example">
  ```python async_tools.py theme={null}
  import asyncio
  import time

  from agno.agent import Agent
  from agno.models.openai import OpenAIResponses
  from agno.utils.log import logger

  async def atask1(delay: int):
      """Simulate a task that takes a random amount of time to complete
      Args:
          delay (int): The amount of time to delay the task
      """
      logger.info("Task 1 has started")
      for _ in range(delay):
          await asyncio.sleep(1)
          logger.info("Task 1 has slept for 1s")
      logger.info("Task 1 has completed")
      return f"Task 1 completed in {delay:.2f}s"


  async def atask2(delay: int):
      """Simulate a task that takes a random amount of time to complete
      Args:
          delay (int): The amount of time to delay the task
      """
      logger.info("Task 2 has started")
      for _ in range(delay):
          await asyncio.sleep(1)
          logger.info("Task 2 has slept for 1s")
      logger.info("Task 2 has completed")
      return f"Task 2 completed in {delay:.2f}s"


  async def atask3(delay: int):
      """Simulate a task that takes a random amount of time to complete
      Args:
          delay (int): The amount of time to delay the task
      """
      logger.info("Task 3 has started")
      for _ in range(delay):
          await asyncio.sleep(1)
          logger.info("Task 3 has slept for 1s")
      logger.info("Task 3 has completed")
      return f"Task 3 completed in {delay:.2f}s"


  async_agent = Agent(
      model=OpenAIResponses(id="gpt-5.2"),
      tools=[atask2, atask1, atask3],
      markdown=True,
  )

  asyncio.run(
      async_agent.aprint_response("Please run all tasks with a delay of 3s", stream=True)
  )
  ```

  In this example, `gpt-5-mini` makes three simultaneous tool calls to `atask1`, `atask2` and `atask3`. Normally these tool calls would execute sequentially, but using the `aprint_response` function, they run concurrently, improving execution time.

  <img height="200" src="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=4ec6216f4c1dafa6c7a675bd345c6ad2" style={{ borderRadius: "8px" }} data-og-width="344" data-og-height="463" data-path="images/async-tools.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=280&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=2ef332604d86c02722791a3beffa7589 280w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=560&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=948e641806ce6a2224074a78a5dd9521 560w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=840&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=9bbc9234b871fdec04c5229f69637c4a 840w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=1100&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=7a8dcfeb62df06475d15981339375437 1100w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=1650&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=7078423de7061f62251c3f6209dbb38e 1650w, https://mintcdn.com/agno-v2/Y7twezR0wF2re1xh/images/async-tools.png?w=2500&fit=max&auto=format&n=Y7twezR0wF2re1xh&q=85&s=512ee4e5ccf4e4bfa33edac026b3a472 2500w" />
</Accordion>

## Using a Toolkit

An Agno Toolkit provides a way to manage multiple tools with additional control over their execution.

```python  theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[
        HackerNewsTools(),
    ],
)

agent.print_response("What are the top stories on HackerNews?", markdown=True)
```

In this example, the `HackerNewsTools` toolkit is added to the agent. This toolkit enables the agent to fetch stories from HackerNews.

## Tool Built-in Parameters

Agno automatically provides special parameters to your tools that give access to the agent's parameters, state and other variables. These parameters are injected automatically - the agent doesn't need to know about them.

### Using the Run Context

You can access values from the current run via the `run_context` parameter: `run_context.session_state`, `run_context.dependencies`, `run_context.knowledge_filters`, `run_context.metadata`. See the [RunContext schema](/reference/run/run-context) for more information.

This allows tools to access and modify persistent data across conversations.

This is useful in cases where a tool result is relevant for the next steps of the conversation.

Add `run_context` as a parameter in your tool function to access the agent's persistent state:

```python  theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.openai import OpenAIResponses
from agno.run import RunContext


def add_item(run_context: RunContext, item: str) -> str:
    """Add an item to the shopping list."""
    if not run_context.session_state:
        run_context.session_state = {}

    run_context.session_state["shopping_list"].append(item)  # type: ignore
    return f"The shopping list is now {run_context.session_state['shopping_list']}"  # type: ignore


# Create an Agent that maintains state
agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    # Initialize the session state with a counter starting at 0 (this is the default session state for all users)
    session_state={"shopping_list": []},
    db=SqliteDb(db_file="tmp/agents.db"),
    tools=[add_item],
    # You can use variables from the session state in the instructions
    instructions="Current state (shopping list) is: {shopping_list}",
    markdown=True,
)

# Example usage
agent.print_response("Add milk, eggs, and bread to the shopping list", stream=True)
print(f"Final session state: {agent.get_session_state()}")
```

See more in [Agent State](/state/agent/overview).

### Using the Agent or Team

You can access the `Agent` or `Team` instance directly in your tool function by adding `agent` or `team` as a parameter. This gives you full access to the agent's or team's properties like model, instructions, etc.

```python  theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses

def get_agent_instructions(agent: Agent) -> str:
    """Get the model of the agent."""
    return agent.instructions

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    instructions="You are a helpful assistant that can answer questions about the model.",
    tools=[get_agent_instructions],
)

agent.print_response("What is the instructions of the agent?", stream=True)
```

<Note>
  When using `team` as a parameter, make sure the tool is being used within a Team context. Similarly, use `agent` when the tool is used with an Agent.
</Note>

### Media Parameters

The built-in parameter `images`, `videos`, `audio`, and `files` allows tools to access and modify the input media to an agent.

<Note>
  Using the `send_media_to_model` parameter, you can control whether the media is sent to the model or not and using `store_media` parameter, you can control whether the
  media is stored in the `RunOutput` or not.
</Note>

See the [image input example](/multimodal/agent/usage/image-input-for-tool) and [file input example](/multimodal/agent/usage/file-input-for-tool) for an advanced example using media.

## Tool Results

Tools can return different types of results depending on their complexity and what they need to communicate back to the agent.

### Simple Return Types

Most tools can return simple Python types directly like `str`, `int`, `float`, `dict`, and `list`:

```python  theme={null}
@tool
def get_weather(city: str) -> str:
    """Get the weather for a city."""
    return f"The weather in {city} is sunny and 75°F"

@tool
def calculate_sum(a: int, b: int) -> int:
    """Calculate the sum of two numbers."""
    return a + b

@tool
def get_user_info(user_id: str) -> dict:
    """Get user information."""
    return {
        "user_id": user_id,
        "name": "John Doe",
        "email": "john@example.com",
        "status": "active"
    }

@tool
def search_products(query: str) -> list:
    """Search for products."""
    return [
        {"id": 1, "name": "Product A", "price": 29.99},
        {"id": 2, "name": "Product B", "price": 39.99}
    ]
```

### `ToolResult` for Media Content

When your tool needs to return media artifacts (images, videos, audio), you **must** use `ToolResult`:

<Snippet file="tool-result-reference.mdx" />

```python  theme={null}
from agno.tools.function import ToolResult
from agno.media import Image

@tool
def generate_image(prompt: str) -> ToolResult:
    """Generate an image from a prompt."""

    # Create your image (example)
    image_artifact = Image(
        id="img_123",
        url="https://example.com/generated-image.jpg",
        original_prompt=prompt
    )

    return ToolResult(
        content=f"Generated image for: {prompt}",
        images=[image]
    )
```

This would **make generated media available** to the LLM model.

## Learn more

<CardGroup cols={3}>
  <Card href="/tools/agent" icon="robot" iconType="duotone">
    Equip agents with tools for external actions
  </Card>

  <Card href="/tools/team" icon="users" iconType="duotone">
    Give teams shared tool capabilities
  </Card>

  <Card title="Available Toolkits" icon="box-open" href="/tools/toolkits">
    Browse 120+ pre-built toolkits
  </Card>

  <Card title="MCP Tools" icon="robot" href="/tools/mcp">
    Connect to Model Context Protocol servers
  </Card>

  <Card title="Reasoning Tools" icon="brain-circuit" href="/tools/reasoning_tools">
    Add knowledge, memory, and workflow tools
  </Card>

  <Card title="Creating your own tools" icon="code" href="/tools/creating-tools/overview">
    Write custom Python functions as tools
  </Card>
</CardGroup>
