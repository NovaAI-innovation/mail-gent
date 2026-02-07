# Requesty

**Source:** https://docs.agno.com/reference/models/requesty.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Requesty

The Requesty model provides access to models through Requesty AI.

## Parameters

| Parameter               | Type            | Default                           | Description                                                       |
| ----------------------- | --------------- | --------------------------------- | ----------------------------------------------------------------- |
| `id`                    | `str`           | `"openai/gpt-4.1"`                | The id of the model to use through Requesty                       |
| `name`                  | `str`           | `"Requesty"`                      | The name of the model                                             |
| `provider`              | `str`           | `"Requesty"`                      | The provider of the model                                         |
| `api_key`               | `Optional[str]` | `None`                            | The API key for Requesty (defaults to REQUESTY\_API\_KEY env var) |
| `base_url`              | `str`           | `"https://router.requesty.ai/v1"` | The base URL for the Requesty API                                 |
| `max_tokens`            | `int`           | `1024`                            | The maximum number of tokens to generate                          |
| `retries`               | `int`           | `0`                               | Number of retries to attempt before raising a ModelProviderError  |
| `delay_between_retries` | `int`           | `1`                               | Delay between retries, in seconds                                 |
| `exponential_backoff`   | `bool`          | `False`                           | If True, the delay between retries is doubled each time           |

Requesty extends the OpenAI-compatible interface and supports most parameters from OpenAI.
