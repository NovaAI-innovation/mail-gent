# Router Steps

**Source:** https://docs.agno.com/reference/workflows/router-steps.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Router Steps

## Parameters

| Parameter     | Type                                                             | Default  | Description                                                                                    |
| ------------- | ---------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `selector`    | `Callable[[StepInput], ...] \| Callable[[StepInput, list], ...]` | Required | Function to select steps dynamically. Can optionally accept `step_choices` as second parameter |
| `choices`     | `WorkflowSteps`                                                  | Required | Available steps for selection. Supports nested lists (becomes Steps container)                 |
| `name`        | `Optional[str]`                                                  | `None`   | Name of the router step                                                                        |
| `description` | `Optional[str]`                                                  | `None`   | Description of the router step                                                                 |

## Selector Return Types

The selector function can return any of the following:

| Return Type  | Description                                           |
| ------------ | ----------------------------------------------------- |
| `str`        | Step name as string - Router resolves it from choices |
| `Step`       | Step object directly                                  |
| `List[Step]` | List of steps for chaining execution                  |

## Selector Function Signatures

### Basic Signature

```python  theme={null}
def selector(step_input: StepInput) -> Union[str, Step, List[Step]]:
    ...
```

### Extended Signature (with step\_choices)

```python  theme={null}
def selector(step_input: StepInput, step_choices: list) -> Union[str, Step, List[Step]]:
    ...
```

The `step_choices` parameter provides access to the prepared Step objects from `Router.choices`, enabling dynamic selection based on available options.

### Async Support

Both signatures support async functions:

```python  theme={null}
async def selector(step_input: StepInput, step_choices: list) -> Union[str, Step, List[Step]]:
    ...
```
