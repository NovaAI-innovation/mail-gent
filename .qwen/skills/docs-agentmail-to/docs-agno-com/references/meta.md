# Meta

**Source:** https://docs.agno.com/reference/models/meta.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Meta

The Meta model provides access to Meta's language models.

## Parameters

| Parameter               | Type            | Default                                     | Description                                                      |
| ----------------------- | --------------- | ------------------------------------------- | ---------------------------------------------------------------- |
| `id`                    | `str`           | `"meta-llama/Meta-Llama-3.1-405B-Instruct"` | The id of the Meta model to use                                  |
| `name`                  | `str`           | `"MetaLlama"`                               | The name of the model                                            |
| `provider`              | `str`           | `"Meta"`                                    | The provider of the model                                        |
| `api_key`               | `Optional[str]` | `None`                                      | The API key for Meta (defaults to META\_API\_KEY env var)        |
| `base_url`              | `str`           | `"https://api.llama-api.com"`               | The base URL for the Meta API                                    |
| `retries`               | `int`           | `0`                                         | Number of retries to attempt before raising a ModelProviderError |
| `delay_between_retries` | `int`           | `1`                                         | Delay between retries, in seconds                                |
| `exponential_backoff`   | `bool`          | `False`                                     | If True, the delay between retries is doubled each time          |

Meta extends the OpenAI-compatible interface and supports most parameters from OpenAI.
