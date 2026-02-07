# List Config Versions

**Source:** https://docs.agno.com/reference-api/schema/components/list-configs.md
**Section:** Docs

**Description:** List all config versions for a component.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Config Versions

> List all config versions for a component.

## Path Parameters

| Parameter      | Type     | Description      |
| -------------- | -------- | ---------------- |
| `component_id` | `string` | The component ID |

## Query Parameters

| Parameter        | Type   | Default | Description                                  |
| ---------------- | ------ | ------- | -------------------------------------------- |
| `include_config` | `bool` | `true`  | Include the full config dict in the response |

## Response `200`

Returns a `List[ComponentConfigResponse]`.

```json  theme={null}
[
  {
    "component_id": "my-research-agent",
    "version": 1,
    "label": "v1.0",
    "stage": "published",
    "config": { ... },
    "notes": "Initial version",
    "created_at": "2025-01-15T10:30:00Z",
    "updated_at": "2025-01-15T10:30:00Z"
  },
  {
    "component_id": "my-research-agent",
    "version": 2,
    "label": "v1.1-improved-instructions",
    "stage": "draft",
    "config": { ... },
    "notes": "Updated instructions",
    "created_at": "2025-01-16T14:20:00Z",
    "updated_at": "2025-01-16T14:20:00Z"
  }
]
```
