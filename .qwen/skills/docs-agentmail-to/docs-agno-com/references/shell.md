# Shell

**Source:** https://docs.agno.com/tools/toolkits/local/shell.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Shell

**ShellTools** enable an Agent to interact with the shell to run commands.

## Example

The following agent will run a shell command and show contents of the current directory.

<Note>
  Mention your OS to the agent to make sure it runs the correct command.
</Note>

```python cookbook/14_tools/shell_tools.py theme={null}
from agno.agent import Agent
from agno.tools.shell import ShellTools

agent = Agent(tools=[ShellTools()])
agent.print_response("Show me the contents of the current directory", markdown=True)
```

## Toolkit Params

| Parameter                  | Type   | Default | Description                                 |                                            |
| -------------------------- | ------ | ------- | ------------------------------------------- | ------------------------------------------ |
| `base_dir`                 | \`Path | str\`   | `None`                                      | Base directory for shell command execution |
| `enable_run_shell_command` | `bool` | `True`  | Enables functionality to run shell commands |                                            |
| `all`                      | `bool` | `False` | Enables all functionality when set to True  |                                            |

## Toolkit Functions

| Function            | Description                                           |
| ------------------- | ----------------------------------------------------- |
| `run_shell_command` | Runs a shell command and returns the output or error. |

## Developer Resources

* View [Tools](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/shell.py)
