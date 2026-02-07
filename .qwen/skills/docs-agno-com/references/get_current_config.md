# Get Current Config

**Source:** https://docs.agno.com/reference-api/schema/components/get-current-config.md
**Section:** Docs

**Description:** Get the current (active) config version for a component.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Current Config

> Get the current (active) config version for a component.

## Path Parameters

| Parameter      | Type     | Description      |
| -------------- | -------- | ---------------- |
| `component_id` | `string` | The component ID |

## Response `200`

Returns the `ComponentConfigResponse` for the current active version.

```json  theme={null}
{
  "component_id": "my-research-agent",
  "version": 3,
  "label": "v1.2",
  "stage": "published",
  "config": {
    "model": "gpt-5-mini",
    "tools": ["WebSearchTools"],
    "instructions": "Research topics thoroughly using web search."
  },
  "notes": "Improved instructions",
  "created_at": "2025-01-16T14:20:00Z",
  "updated_at": "2025-01-16T14:20:00Z"
}
```
