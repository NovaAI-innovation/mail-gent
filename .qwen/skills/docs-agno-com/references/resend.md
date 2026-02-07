# Resend

**Source:** https://docs.agno.com/tools/toolkits/others/resend.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Resend

**ResendTools** enable an Agent to send emails using Resend

## Prerequisites

The following example requires the `resend` library and an API key from [Resend](https://resend.com/).

```shell  theme={null}
uv pip install -U resend
```

```shell  theme={null}
export RESEND_API_KEY=***
```

## Example

The following agent will send an email using Resend

```python cookbook/14_tools/resend_tools.py theme={null}
from agno.agent import Agent
from agno.tools.resend import ResendTools

from_email = "<enter_from_email>"
to_email = "<enter_to_email>"

agent = Agent(tools=[ResendTools(from_email=from_email)])
agent.print_response(f"Send an email to {to_email} greeting them with hello world")
```

## Toolkit Params

| Parameter           | Type   | Default | Description                                                   |
| ------------------- | ------ | ------- | ------------------------------------------------------------- |
| `api_key`           | `str`  | -       | API key for authentication purposes.                          |
| `from_email`        | `str`  | -       | The email address used as the sender in email communications. |
| `enable_send_email` | `bool` | `True`  | Enable the send\_email functionality.                         |
| `all`               | `bool` | `False` | Enable all functionality.                                     |

## Toolkit Functions

| Function     | Description                         |
| ------------ | ----------------------------------- |
| `send_email` | Send an email using the Resend API. |

## Developer Resources

* View [Tools](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/resend.py)
