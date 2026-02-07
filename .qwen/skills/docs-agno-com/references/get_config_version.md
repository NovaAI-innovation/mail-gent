# Get Config Version

**Source:** https://docs.agno.com/reference-api/schema/components/get-config-version.md
**Section:** Docs

**Description:** Get a specific config version for a component.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Config Version

> Get a specific config version for a component.

## Path Parameters

| Parameter      | Type     | Description        |
| -------------- | -------- | ------------------ |
| `component_id` | `string` | The component ID   |
| `version`      | `int`    | The version number |

## Response `200`

Returns the `ComponentConfigResponse` for the specified version.
