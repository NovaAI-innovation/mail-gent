# Running Teams

**Source:** https://docs.agno.com/teams/running-teams.md
**Section:** Docs

**Description:** Execute teams with Team.run() and process their output.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Running Teams

> Execute teams with Team.run() and process their output.

Run your team with `Team.run()` (sync) or `Team.arun()` (async).

## Basic Execution

```python  theme={null}
from agno.team import Team
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools
from agno.tools.yfinance import YFinanceTools
from agno.utils.pprint import pprint_run_response

news_agent = Agent(name="News Agent", role="Get tech news", tools=[HackerNewsTools()])
finance_agent = Agent(name="Finance Agent", role="Get stock data", tools=[YFinanceTools()])

team = Team(
    name="Research Team",
    members=[news_agent, finance_agent],
    model=OpenAIResponses(id="gpt-4o")
)

# Run and get response
response = team.run("What are the trending AI stories?")
print(response.content)

# Run with streaming
stream = team.run("What are the trending AI stories?", stream=True)
for chunk in stream:
    print(chunk.content, end="", flush=True)
```

## Execution Flow

When you call `run()`:

1. **Pre-hooks execute** (if configured)
2. **Reasoning runs** (if enabled) to plan the task
3. **Context is built** with system message, history, memories, and session state
4. **Model decides** whether to respond directly, use tools, or delegate to members
5. **Members execute** their tasks (concurrently in async mode)
6. **Leader synthesizes** member results into a final response
7. **Post-hooks execute** (if configured)
8. **Session and metrics are stored** (if database configured)

<Accordion title="Execution Flow Diagram">
  <img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=620f30536d975bf35fd7a39e44f343bc" alt="Team execution flow" data-og-width="3636" width="3636" data-og-height="5664" height="5664" data-path="images/teams/team-details-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=e3d863ed3a9710f8f9c30c7bf2759349 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=53722384f2acbe892e9b2e6d308f97be 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7f575c44ea568261de09a60d7a1047a9 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=532005f08da6722a638a4119000922e8 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=d631f4a778e58e2948ba88d60ea16ac1 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=715b5ca74b465e857e331b9eaf6ff2f4 2500w" />

  <img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=bb04b20f1810e17d08f4f3880f7a1615" alt="Team execution flow" data-og-width="3636" width="3636" data-og-height="5664" height="5664" data-path="images/teams/team-details-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=53e911082ca802723c89443fb6e859cc 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=ad31aa1ff5078f01382e5b291725e5a4 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=2e5e07e3dc2e5e4b74b989db695489e7 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=57be6f8c58e62def20fdea637a38e257 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0914ded32d9a5fcfc6a1a5ad59b661b7 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-details-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=f7fedcdac8556ab81f81c9f605083a1d 2500w" />
</Accordion>

## Streaming

Enable streaming with `stream=True`. This returns an iterator of events instead of a single response.

```python  theme={null}
stream = team.run("What are the top AI stories?", stream=True)
for chunk in stream:
    print(chunk.content, end="", flush=True)
```

### Stream All Events

By default, only content is streamed. Set `stream_events=True` to get tool calls, reasoning steps, and other internal events:

```python  theme={null}
stream = team.run(
    "What are the trending AI stories?",
    stream=True,
    stream_events=True
)

for event in stream:
    if event.event == TeamRunEvent.run_content:
        print(event.content, end="", flush=True)
    elif event.event == TeamRunEvent.tool_call_started:
        print(f"Tool call started")
    elif event.event == TeamRunEvent.tool_call_completed:
        print(f"Tool call completed")
```

### Stream Member Events

When using `arun()` with multiple members, they execute concurrently. Member events arrive as they happen, not in order.

Disable member event streaming with `stream_member_events=False`:

```python  theme={null}
team = Team(
    name="Research Team",
    members=[news_agent, finance_agent],
    model=OpenAIResponses(id="gpt-4o"),
    stream_member_events=False
)
```

## Run Output

`Team.run()` returns a `TeamRunOutput` object containing:

| Field              | Description                       |
| ------------------ | --------------------------------- |
| `content`          | The final response text           |
| `messages`         | All messages sent to the model    |
| `metrics`          | Token usage, execution time, etc. |
| `member_responses` | Responses from delegated members  |

See [TeamRunOutput reference](/reference/teams/team-response) for the full schema.

## Async Execution

Use `arun()` for async execution. Members run concurrently when the leader delegates to multiple members at once.

```python  theme={null}
import asyncio

async def main():
    response = await team.arun("Research AI trends and stock performance")
    print(response.content)

asyncio.run(main())
```

## Specifying User and Session

Associate runs with a user and session for history tracking:

```python  theme={null}
team.run(
    "Get my monthly report",
    user_id="john@example.com",
    session_id="session_123"
)
```

See [Sessions](/sessions/overview) for details.

## Passing Files

Pass images, audio, video, or files to the team:

```python  theme={null}
from agno.media import Image

team.run(
    "Analyze this image",
    images=[Image(url="https://example.com/image.jpg")]
)
```

See [Multimodal](/multimodal/overview) for details.

## Structured Output

Pass an output schema to get structured responses:

```python  theme={null}
from pydantic import BaseModel

class Report(BaseModel):
    overview: str
    findings: list[str]

response = team.run("Analyze the market", output_schema=Report)
```

See [Input & Output](/input-output/overview) for details.

## Cancelling Runs

Cancel a running team with `Team.cancel_run()`. See [Run Cancellation](/run-cancellation/overview).

## Print Response

For development, use `print_response()` to display formatted output:

```python  theme={null}
team.print_response("What are the top AI stories?", stream=True)

# Show member responses too
team.print_response("What are the top AI stories?", show_members_responses=True)
```

<Accordion title="Event Types Reference">
  ### Core Events

  | Event                     | Description                |
  | ------------------------- | -------------------------- |
  | `TeamRunStarted`          | Run started                |
  | `TeamRunContent`          | Response text chunk        |
  | `TeamRunContentCompleted` | Content streaming complete |
  | `TeamRunCompleted`        | Run completed successfully |
  | `TeamRunError`            | Error occurred             |
  | `TeamRunCancelled`        | Run was cancelled          |

  ### Tool Events

  | Event                   | Description         |
  | ----------------------- | ------------------- |
  | `TeamToolCallStarted`   | Tool call started   |
  | `TeamToolCallCompleted` | Tool call completed |

  ### Reasoning Events

  | Event                    | Description           |
  | ------------------------ | --------------------- |
  | `TeamReasoningStarted`   | Reasoning started     |
  | `TeamReasoningStep`      | Single reasoning step |
  | `TeamReasoningCompleted` | Reasoning completed   |

  ### Memory Events

  | Event                       | Description             |
  | --------------------------- | ----------------------- |
  | `TeamMemoryUpdateStarted`   | Memory update started   |
  | `TeamMemoryUpdateCompleted` | Memory update completed |

  ### Hook Events

  | Event                   | Description         |
  | ----------------------- | ------------------- |
  | `TeamPreHookStarted`    | Pre-hook started    |
  | `TeamPreHookCompleted`  | Pre-hook completed  |
  | `TeamPostHookStarted`   | Post-hook started   |
  | `TeamPostHookCompleted` | Post-hook completed |
</Accordion>

## Developer Resources

* [Team reference](/reference/teams/team)
* [TeamRunOutput schema](/reference/teams/team-response)
* [Team examples](/cookbook/teams/overview)
