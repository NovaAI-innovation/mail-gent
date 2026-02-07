# Set Current Config

**Source:** https://docs.agno.com/reference-api/schema/components/set-current-config.md
**Section:** Docs

**Description:** Set a specific config version as the current active version.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Set Current Config

> Set a specific config version as the current active version.

## Path Parameters

| Parameter      | Type     | Description                          |
| -------------- | -------- | ------------------------------------ |
| `component_id` | `string` | The component ID                     |
| `version`      | `int`    | The version number to set as current |

## Response `200`

Returns the updated `ComponentResponse` with the new `current_version`.
