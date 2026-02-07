# Perplexity

**Source:** https://docs.agno.com/reference/models/perplexity.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Perplexity

The Perplexity model provides access to Perplexity's language models.

## Parameters

| Parameter                       | Type              | Default                        | Description                                                                                            |
| ------------------------------- | ----------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `id`                            | `str`             | `"sonar"`                      | The ID of the Perplexity model to use                                                                  |
| `name`                          | `str`             | `"Perplexity"`                 | The name of the model                                                                                  |
| `provider`                      | `str`             | `"Perplexity"`                 | The provider of the model                                                                              |
| `api_key`                       | `Optional[str]`   | `None`                         | The API key for Perplexity (defaults to PERPLEXITY\_API\_KEY env var)                                  |
| `base_url`                      | `str`             | `"https://api.perplexity.ai/"` | The base URL for the Perplexity API                                                                    |
| `max_tokens`                    | `int`             | `1024`                         | Maximum number of tokens to generate                                                                   |
| `top_k`                         | `Optional[float]` | `None`                         | Number of highest probability tokens to consider for generation                                        |
| `collect_metrics_on_completion` | `bool`            | `True`                         | Collect token metrics only from the final streaming chunk (for providers with cumulative token counts) |
| `retries`                       | `int`             | `0`                            | Number of retries to attempt before raising a ModelProviderError                                       |
| `delay_between_retries`         | `int`             | `1`                            | Delay between retries, in seconds                                                                      |
| `exponential_backoff`           | `bool`            | `False`                        | If True, the delay between retries is doubled each time                                                |

Perplexity extends the OpenAI-compatible interface and supports most parameters from OpenAI.
