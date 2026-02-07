# List Components

**Source:** https://docs.agno.com/reference-api/schema/components/list-components.md
**Section:** Docs

**Description:** List all components with optional filtering and pagination.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Components

> List all components with optional filtering and pagination.

## Query Parameters

| Parameter        | Type     | Default | Description                                 |
| ---------------- | -------- | ------- | ------------------------------------------- |
| `component_type` | `string` | `None`  | Filter by type: `agent`, `team`, `workflow` |
| `page`           | `int`    | `1`     | Page number (≥ 1)                           |
| `limit`          | `int`    | `20`    | Items per page (1-100)                      |

## Response `200`

Returns a `PaginatedResponse[ComponentResponse]`.

```json  theme={null}
{
  "data": [
    {
      "component_id": "my-research-agent",
      "component_type": "agent",
      "name": "Research Agent",
      "description": "An agent that researches topics",
      "current_version": 3,
      "metadata": {},
      "created_at": "2025-01-15T10:30:00Z",
      "updated_at": "2025-01-16T14:20:00Z"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total_pages": 1,
    "total_count": 1,
    "search_time_ms": 5
  }
}
```
