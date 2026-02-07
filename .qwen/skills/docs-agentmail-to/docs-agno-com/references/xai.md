# xAI

**Source:** https://docs.agno.com/reference/models/xai.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# xAI

The xAI model provides access to xAI's language models.

## Parameters

| Parameter               | Type            | Default                 | Description                                                      |
| ----------------------- | --------------- | ----------------------- | ---------------------------------------------------------------- |
| `id`                    | `str`           | `"grok-beta"`           | The id of the xAI model to use                                   |
| `name`                  | `str`           | `"xAI"`                 | The name of the model                                            |
| `provider`              | `str`           | `"xAI"`                 | The provider of the model                                        |
| `api_key`               | `Optional[str]` | `None`                  | The API key for xAI (defaults to XAI\_API\_KEY env var)          |
| `base_url`              | `str`           | `"https://api.x.ai/v1"` | The base URL for the xAI API                                     |
| `retries`               | `int`           | `0`                     | Number of retries to attempt before raising a ModelProviderError |
| `delay_between_retries` | `int`           | `1`                     | Delay between retries, in seconds                                |
| `exponential_backoff`   | `bool`          | `False`                 | If True, the delay between retries is doubled each time          |

xAI extends the OpenAI-compatible interface and supports most parameters from OpenAI.
