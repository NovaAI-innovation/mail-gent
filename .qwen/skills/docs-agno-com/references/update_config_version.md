# Update Config Version

**Source:** https://docs.agno.com/reference-api/schema/components/update-config.md
**Section:** Docs

**Description:** Update a specific config version.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Config Version

> Update a specific config version.

## Path Parameters

| Parameter      | Type     | Description        |
| -------------- | -------- | ------------------ |
| `component_id` | `string` | The component ID   |
| `version`      | `int`    | The version number |

## Request Body

All fields are optional.

| Field    | Type     | Description                          |
| -------- | -------- | ------------------------------------ |
| `config` | `dict`   | Updated configuration data           |
| `label`  | `string` | Updated version label                |
| `stage`  | `string` | Updated stage (`draft`, `published`) |
| `notes`  | `string` | Updated notes                        |
| `links`  | `list`   | Updated child component links        |

## Response `200`

Returns the updated `ComponentConfigResponse`.
