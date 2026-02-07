# Create Config Version

**Source:** https://docs.agno.com/reference-api/schema/components/create-config.md
**Section:** Docs

**Description:** Create a new config version for a component.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Config Version

> Create a new config version for a component.

## Path Parameters

| Parameter      | Type     | Description      |
| -------------- | -------- | ---------------- |
| `component_id` | `string` | The component ID |

## Request Body

| Field         | Type     | Required | Description                                  |
| ------------- | -------- | -------- | -------------------------------------------- |
| `config`      | `dict`   | Yes      | The configuration data                       |
| `version`     | `int`    | No       | Version number (auto-incremented if omitted) |
| `label`       | `string` | No       | Version label (e.g., `v1.0`, `beta`)         |
| `stage`       | `string` | No       | Version stage (default: `draft`)             |
| `notes`       | `string` | No       | Version notes                                |
| `links`       | `list`   | No       | Links to child components                    |
| `set_current` | `bool`   | No       | Set this version as current                  |

## Response `201`

Returns a `ComponentConfigResponse` with the created config version.
