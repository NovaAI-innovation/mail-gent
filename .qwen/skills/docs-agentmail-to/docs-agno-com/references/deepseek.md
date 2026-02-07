# DeepSeek

**Source:** https://docs.agno.com/reference/models/deepseek.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# DeepSeek

The DeepSeek model provides access to DeepSeek's language models.

## Parameters

| Parameter               | Type            | Default                      | Description                                                       |
| ----------------------- | --------------- | ---------------------------- | ----------------------------------------------------------------- |
| `id`                    | `str`           | `"deepseek-chat"`            | The id of the DeepSeek model to use                               |
| `name`                  | `str`           | `"DeepSeek"`                 | The name of the model                                             |
| `provider`              | `str`           | `"DeepSeek"`                 | The provider of the model                                         |
| `api_key`               | `Optional[str]` | `None`                       | The API key for DeepSeek (defaults to DEEPSEEK\_API\_KEY env var) |
| `base_url`              | `str`           | `"https://api.deepseek.com"` | The base URL for the DeepSeek API                                 |
| `retries`               | `int`           | `0`                          | Number of retries to attempt before raising a ModelProviderError  |
| `delay_between_retries` | `int`           | `1`                          | Delay between retries, in seconds                                 |
| `exponential_backoff`   | `bool`          | `False`                      | If True, the delay between retries is doubled each time           |

DeepSeek extends the OpenAI-compatible interface and supports most parameters from OpenAI.
