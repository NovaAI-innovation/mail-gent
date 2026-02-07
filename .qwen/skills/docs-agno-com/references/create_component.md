# Create Component

**Source:** https://docs.agno.com/reference-api/schema/components/create-component.md
**Section:** Docs

**Description:** Create a new component (agent, team, or workflow).

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Component

> Create a new component (agent, team, or workflow).

## Request Body

| Field            | Type     | Required | Description                                     |
| ---------------- | -------- | -------- | ----------------------------------------------- |
| `name`           | `string` | Yes      | Display name for the component                  |
| `component_id`   | `string` | No       | Unique ID (auto-generated from name if omitted) |
| `component_type` | `string` | Yes      | One of: `agent`, `team`, `workflow`             |
| `description`    | `string` | No       | Description of the component                    |
| `metadata`       | `dict`   | No       | Additional metadata                             |
| `config`         | `dict`   | No       | Initial configuration                           |
| `label`          | `string` | No       | Version label                                   |
| `stage`          | `string` | No       | Version stage (default: `draft`)                |
| `notes`          | `string` | No       | Version notes                                   |
| `set_current`    | `bool`   | No       | Set this version as current                     |

```json  theme={null}
{
  "name": "Research Agent",
  "component_type": "agent",
  "description": "An agent that researches topics",
  "config": {
    "model": "gpt-5-mini",
    "tools": ["WebSearchTools"],
    "instructions": "Research topics thoroughly."
  },
  "stage": "draft"
}
```

## Response `201`

Returns a `ComponentResponse` with the created component.
