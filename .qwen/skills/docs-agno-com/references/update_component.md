# Update Component

**Source:** https://docs.agno.com/reference-api/schema/components/update-component.md
**Section:** Docs

**Description:** Update a component's metadata.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Component

> Update a component's metadata.

## Path Parameters

| Parameter      | Type     | Description      |
| -------------- | -------- | ---------------- |
| `component_id` | `string` | The component ID |

## Request Body

All fields are optional.

| Field             | Type     | Description                    |
| ----------------- | -------- | ------------------------------ |
| `name`            | `string` | Updated display name           |
| `description`     | `string` | Updated description            |
| `component_type`  | `string` | Updated type                   |
| `metadata`        | `dict`   | Updated metadata               |
| `current_version` | `int`    | Set the current version number |

## Response `200`

Returns the updated `ComponentResponse`.
