# Conditional Steps

**Source:** https://docs.agno.com/reference/workflows/conditional-steps.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Conditional Steps

| Parameter     | Type                                                                               | Default  | Description                                   |
| ------------- | ---------------------------------------------------------------------------------- | -------- | --------------------------------------------- |
| `evaluator`   | `Union[Callable[[StepInput], bool], Callable[[StepInput], Awaitable[bool]], bool]` | Required | Function or boolean to evaluate the condition |
| `steps`       | `WorkflowSteps`                                                                    | Required | Steps to execute if the condition is met      |
| `name`        | `Optional[str]`                                                                    | `None`   | Name of the condition step                    |
| `description` | `Optional[str]`                                                                    | `None`   | Description of the condition step             |
