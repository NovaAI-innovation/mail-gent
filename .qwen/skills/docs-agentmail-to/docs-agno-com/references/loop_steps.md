# Loop Steps

**Source:** https://docs.agno.com/reference/workflows/loop-steps.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Loop Steps

| Parameter        | Type                                                                                                 | Default  | Description                                 |
| ---------------- | ---------------------------------------------------------------------------------------------------- | -------- | ------------------------------------------- |
| `steps`          | `WorkflowSteps`                                                                                      | Required | Steps to execute in each loop iteration     |
| `name`           | `Optional[str]`                                                                                      | `None`   | Name of the loop step                       |
| `description`    | `Optional[str]`                                                                                      | `None`   | Description of the loop step                |
| `max_iterations` | `int`                                                                                                | `3`      | Maximum number of iterations for the loop   |
| `end_condition`  | `Optional[Union[Callable[[List[StepOutput]], bool], Callable[[List[StepOutput]], Awaitable[bool]]]]` | `None`   | Function to evaluate if the loop should end |
