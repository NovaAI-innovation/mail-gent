# Telegram

**Source:** https://docs.agno.com/tools/toolkits/social/telegram.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Telegram

**TelegramTools** enable an Agent to send messages to a Telegram chat using the Telegram Bot API.

## Prerequisites

```shell  theme={null}
uv pip install -U agno httpx
```

```shell  theme={null}
export TELEGRAM_TOKEN=***
```

## Example

The following agent will send a message to a Telegram chat.

```python cookbook/14_tools/telegram_tools.py theme={null}
from agno.agent import Agent
from agno.tools.telegram import TelegramTools

# How to get the token and chat_id:
# 1. Create a new bot with BotFather on Telegram. https://core.telegram.org/bots/features#creating-a-new-bot
# 2. Get the token from BotFather.
# 3. Send a message to the bot.
# 4. Get the chat_id by going to the URL:
#    https://api.telegram.org/bot/<your-bot-token>/getUpdates

telegram_token = "<enter-your-bot-token>"
chat_id = "<enter-your-chat-id>"

agent = Agent(
    name="telegram",
    tools=[TelegramTools(token=telegram_token, chat_id=chat_id)],
)

agent.print_response("Send message to telegram chat a paragraph about the moon")
```

## Toolkit Params

| Parameter             | Type              | Default | Description                                                                               |
| --------------------- | ----------------- | ------- | ----------------------------------------------------------------------------------------- |
| `token`               | `Optional[str]`   | `None`  | Telegram Bot API token. If not provided, will check TELEGRAM\_TOKEN environment variable. |
| `chat_id`             | `Union[str, int]` | -       | The ID of the chat to send messages to.                                                   |
| `enable_send_message` | `bool`            | `True`  | Enable the send\_message functionality.                                                   |
| `all`                 | `bool`            | `False` | Enable all functionality.                                                                 |

## Toolkit Functions

| Function       | Description                                                                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `send_message` | Sends a message to the specified Telegram chat. Takes a message string as input and returns the API response as text. If an error occurs, returns an error message. |

## Developer Resources

* View [Tools](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/telegram.py)
