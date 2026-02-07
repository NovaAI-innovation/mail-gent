# Background Hooks

**Source:** https://docs.agno.com/agent-os/background-tasks/overview.md
**Section:** Docs

**Description:** Run agent hooks as non-blocking background tasks in AgentOS

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Background Hooks

> Run agent hooks as non-blocking background tasks in AgentOS

When serving agents or teams through AgentOS, you can configure pre-hooks and post-hooks to run as background tasks. This means the API response is returned immediately to the user while the hooks continue executing in the background.

## Why Use Background Hooks?

By default, hooks used by agents and teams in your AgentOS are in the execution path and block the response:

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=615b75c6fd7b2bc946dd12cb853f41b6" alt="Background tasks not enabled" data-og-width="2895" width="2895" data-og-height="906" height="906" data-path="images/background-tasks-notenabled-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=280&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=c3dcec05473d3750f9c6f9a8a2766239 280w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=560&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=942c15c932e0d71652f874088a2fcbea 560w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=840&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=84d728448bc3646060cb3af299d6117d 840w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=1100&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=e9816cdb46d2394bd0e453840a7c61be 1100w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=1650&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=d6ff0b683d01424eca2cc5112985f458 1650w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-light.png?w=2500&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=76d678d154f114a7cf27a93a093220f9 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=510be4326e46562ee9d0e527a76feb33" alt="Background tasks not enabled" data-og-width="2895" width="2895" data-og-height="906" height="906" data-path="images/background-tasks-notenabled-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=280&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=49cf4e5f2c43a56342ef13e3781317b5 280w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=560&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=1b511f27bef977b7caebef20f7df5eff 560w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=840&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=1cc96f5f92036c66a7fb3dadf51f3af9 840w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=1100&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=94e25e9536ca3685ea2b4a1dec0f9660 1100w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=1650&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=de03d910764ae08d2102b26ad6bfcbb0 1650w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-notenabled-dark.png?w=2500&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=8fddb0de142ac887091432456fb46e55 2500w" />

With background hooks enabled, your hooks won't block the response, increasing response speed:

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=b274e516d035f89d422e312945a29aaa" alt="Background tasks enabled" data-og-width="2271" width="2271" data-og-height="906" height="906" data-path="images/background-tasks-enabled-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=280&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=0f9a9b3b3aeb4e353b7f3bf992e89da7 280w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=560&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=38c9e23810aaf50738deae73d851c4fb 560w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=840&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=cf7a55219acaedd0560d2db624f5e81f 840w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=1100&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=7cd4428ab9c6ed95bee09fc7cd132219 1100w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=1650&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=297ff38f65490b1ab71844f7019b9efd 1650w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-light.png?w=2500&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=62a4622b6eaa8134427799ce9af58c4d 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=dddbd20dd6bccab04949979587e67042" alt="Background tasks enabled" data-og-width="2271" width="2271" data-og-height="906" height="906" data-path="images/background-tasks-enabled-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=280&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=dcfb71d67b3b3dabc6d94d9952b56b95 280w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=560&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=98cb92e42b038280f3207a9517c9f2b5 560w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=840&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=fa3436b0d198f8c36c055ab86320a127 840w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=1100&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=9da5f237c3adcd2ddfc2df78d628f112 1100w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=1650&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=5bf6395194962d35f0137167e7c3a5bc 1650w, https://mintcdn.com/agno-v2/I_OqdwByK40CFkbk/images/background-tasks-enabled-dark.png?w=2500&fit=max&auto=format&n=I_OqdwByK40CFkbk&q=85&s=b2b2258684ff3ac029fd00825294bacf 2500w" />

This is useful for:

* **Agent Evaluation**: Evaluate the agent's responses without affecting the responses themselves
* **Analytics and logging**: Track usage patterns without affecting response time
* **Notifications**: Send emails, Slack messages, or webhook calls
* **External API calls**: Sync data with third-party services
* **Non-critical data processing**: Tasks that don't affect the response

## Enabling Background Tasks

There are two ways to enable background execution for hooks:

### Option 1: Global Setting via AgentOS

Enable background execution for **all** hooks across all agents and teams (even as part of a workflow):

```python  theme={null}
from agno.os import AgentOS

agent_os = AgentOS(
    agents=[agent],
    teams=[team],
    workflows=[workflow],
    run_hooks_in_background=True,  # All hooks run in background
)
```

When enabled, this setting automatically propagates to:

* All agents registered with AgentOS
* All teams and their member agents (including nested teams)
* All workflows and the agents/teams within their steps

See [Global Background Hooks Example](/agent-os/usage/background-hooks-global) for an example.

<Note>
  Note that pre-hooks are typically used for validation or modification of the input of a run. If you use them as background tasks, they will execute after the run has already been initiated.

  If you have hooks that should not run as background tasks, you should use the second option and mark only the specific hooks to run in background.
</Note>

### Option 2: Per-Hook Setting via Decorator

Mark specific hooks to run in background using the `@hook` decorator:

```python  theme={null}
from agno.hooks import hook

@hook(run_in_background=True)
async def send_notification(run_output, agent):
    """Only this hook runs in the background."""
    await send_slack_message(run_output.content)
```

This approach gives you fine-grained control: critical hooks are executed during the run while non-critical hooks run in the background.

See [Per-Hook Background Example](/agent-os/usage/background-hooks-decorator) for an example.

<Check>
  **Background tasks require AgentOS.** When running agents directly (not through AgentOS), the `@hook(run_in_background=True)` decorator has no effect - hooks will run synchronously.
</Check>

## How It Works

AgentOS uses FastAPI's [BackgroundTasks](https://fastapi.tiangolo.com/tutorial/background-tasks/) to schedule hooks for execution after the response is sent.

Background tasks execute **sequentially** after the response is sent. If you have multiple background hooks, they run one after another.

<Warning>
  **Pre- and post-hooks in background mode cannot modify the request or response.** Any modifications to `run_input` or `run_output` won't affect the agent's processing. Only use background mode for pre- and post-hooks that perform logging or monitoring. This means background mode is not suitable for Guardrails.
</Warning>

### Data Isolation

When hooks run in the background, AgentOS automatically creates deep copies of:

* `run_input` - The input to the agent run
* `run_context` - The current run context
* `run_output` - The output from the agent

This prevents race conditions where background hooks might accidentally modify data that's being used elsewhere.

### Error Handling

Errors in background tasks don't affect the API response (since it's already been sent). Make sure to implement proper error handling and logging in your background hooks:

```python  theme={null}
@hook(run_in_background=True)
async def safe_background_hook(run_output, agent):
    try:
        await external_api_call(run_output)
    except Exception as e:
        logger.error(f"Background hook failed: {e}")
```

## Examples

<CardGroup cols={3}>
  <Card title="Global Background Hooks" icon="gear" href="/agent-os/usage/background-hooks-global">
    Enable background hooks globally for all agents
  </Card>

  <Card title="Per-Hook Background" icon="code" href="/agent-os/usage/background-hooks-decorator">
    Mix synchronous and background hooks
  </Card>

  <Card title="Output Evaluation" icon="clipboard-check" href="/agent-os/usage/background-output-evaluation">
    Use an agent-as-judge to evaluate responses
  </Card>
</CardGroup>

## Developer Resources

* [@hook Decorator Reference](/reference/hooks/hook-decorator)
* [Hooks Overview](/hooks/overview)
