# DeepInfra

**Source:** https://docs.agno.com/reference/models/deepinfra.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# DeepInfra

The DeepInfra model provides access to DeepInfra's hosted language models.

## Parameters

| Parameter               | Type            | Default                                 | Description                                                         |
| ----------------------- | --------------- | --------------------------------------- | ------------------------------------------------------------------- |
| `id`                    | `str`           | `"meta-llama/Llama-2-70b-chat-hf"`      | The id of the DeepInfra model to use                                |
| `name`                  | `str`           | `"DeepInfra"`                           | The name of the model                                               |
| `provider`              | `str`           | `"DeepInfra"`                           | The provider of the model                                           |
| `api_key`               | `Optional[str]` | `None`                                  | The API key for DeepInfra (defaults to DEEPINFRA\_API\_KEY env var) |
| `base_url`              | `str`           | `"https://api.deepinfra.com/v1/openai"` | The base URL for the DeepInfra API                                  |
| `retries`               | `int`           | `0`                                     | Number of retries to attempt before raising a ModelProviderError    |
| `delay_between_retries` | `int`           | `1`                                     | Delay between retries, in seconds                                   |
| `exponential_backoff`   | `bool`          | `False`                                 | If True, the delay between retries is doubled each time             |

DeepInfra extends the OpenAI-compatible interface and supports most parameters from OpenAI.
