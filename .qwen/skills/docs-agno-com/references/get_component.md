# Get Component

**Source:** https://docs.agno.com/reference-api/schema/components/get-component.md
**Section:** Docs

**Description:** Get details of a specific component by ID.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Component

> Get details of a specific component by ID.

## Path Parameters

| Parameter      | Type     | Description      |
| -------------- | -------- | ---------------- |
| `component_id` | `string` | The component ID |

## Response `200`

Returns a `ComponentResponse`.

```json  theme={null}
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
```
