# Mistral

**Source:** https://docs.agno.com/reference/models/mistral.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Mistral

The Mistral model provides access to Mistral's language models.

## Parameters

| Parameter               | Type            | Default                       | Description                                                      |
| ----------------------- | --------------- | ----------------------------- | ---------------------------------------------------------------- |
| `id`                    | `str`           | `"mistral-large-latest"`      | The id of the Mistral model to use                               |
| `name`                  | `str`           | `"Mistral"`                   | The name of the model                                            |
| `provider`              | `str`           | `"Mistral"`                   | The provider of the model                                        |
| `api_key`               | `Optional[str]` | `None`                        | The API key for Mistral (defaults to MISTRAL\_API\_KEY env var)  |
| `base_url`              | `str`           | `"https://api.mistral.ai/v1"` | The base URL for the Mistral API                                 |
| `retries`               | `int`           | `0`                           | Number of retries to attempt before raising a ModelProviderError |
| `delay_between_retries` | `int`           | `1`                           | Delay between retries, in seconds                                |
| `exponential_backoff`   | `bool`          | `False`                       | If True, the delay between retries is doubled each time          |

Mistral extends the OpenAI-compatible interface and supports most parameters from OpenAI.
