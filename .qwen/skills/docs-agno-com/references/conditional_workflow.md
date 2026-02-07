# Conditional Workflow

**Source:** https://docs.agno.com/workflows/workflow-patterns/conditional-workflow.md
**Section:** Docs

**Description:** Deterministic branching based on input analysis or business rules

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Conditional Workflow

> Deterministic branching based on input analysis or business rules

**Example Use-Cases**: Content type routing, topic-specific processing, quality-based decisions

Conditional workflows provide predictable branching logic while maintaining deterministic execution paths.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=4707a731d8959351f09170c57e311704" alt="Workflows condition steps diagram" data-og-width="2952" width="2952" data-og-height="756" height="756" data-path="images/workflows-condition-steps-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=280&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=aa15772ba647c918c09ef4dfbc53af7d 280w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=560&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=77f4b4759cf10372b02d2e7c990d136d 560w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=840&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=297ff4cbcce464219457514300c2601f 840w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=1100&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=c807562a263d6291a1b0cbc5bc62edfb 1100w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=1650&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=6f1848a78b424f5f8d22fd1f42ecd4f7 1650w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps-light.png?w=2500&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=95a59de11afa29f61c3546e02addc930 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=8a4040e90a6beadd349e845193af3c3d" alt="Workflows condition steps diagram" data-og-width="2952" width="2952" data-og-height="756" height="756" data-path="images/workflows-condition-steps.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=280&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=13df5b1d29c25a99b71f5022f4c05dd2 280w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=560&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=10ea63c548fcb11c937772a1d725f9f5 560w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=840&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=94db25e3be465d44b9c20ab8d32f7694 840w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=1100&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=1b64f7283e6ac075b10af9c8cfb925c9 1100w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=1650&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=08e7845b7a0b3cf7252cff0045e80951 1650w, https://mintcdn.com/agno-v2/2M3_dMYopb5-EJab/images/workflows-condition-steps.png?w=2500&fit=max&auto=format&n=2M3_dMYopb5-EJab&q=85&s=5e7d39dc68e3017c9972f8a17ee6462a 2500w" />

## How It Works

The `Condition` class evaluates a function and executes different steps based on the result:

* **If branch (`steps`)**: Executes when the evaluator returns `True`
* **Else branch (`else_steps`)**: Executes when the evaluator returns `False` (optional)

If the condition is `False` and no `else_steps` are provided, the condition is skipped and the workflow continues to the next step.

## Basic Example

```python conditional_workflow.py theme={null}
from agno.workflow import Condition, Step, Workflow

def is_tech_topic(step_input) -> bool:
    topic = step_input.input.lower()
    return any(keyword in topic for keyword in ["ai", "tech", "software"])

workflow = Workflow(
    name="Conditional Research",
    steps=[
        Condition(
            name="Tech Topic Check",
            evaluator=is_tech_topic,
            steps=[Step(name="Tech Research", agent=tech_researcher)]
        ),
        Step(name="General Analysis", agent=general_analyst),
    ]
)

workflow.print_response("Comprehensive analysis of AI and machine learning trends", markdown=True)
```

## If/Else Branching

Use `else_steps` to define an alternative execution path when the condition is `False`:

```python condition_with_else.py theme={null}
from agno.workflow import Condition, Step, Workflow

def is_technical_issue(step_input) -> bool:
    text = (step_input.input or "").lower()
    tech_keywords = ["error", "bug", "crash", "not working", "api", "timeout"]
    return any(kw in text for kw in tech_keywords)

workflow = Workflow(
    name="Customer Support Router",
    steps=[
        Condition(
            name="TechnicalTriage",
            evaluator=is_technical_issue,
            # If branch: technical pipeline
            steps=[
                Step(name="Diagnose", agent=diagnostic_agent),
                Step(name="Engineer", agent=engineering_agent),
            ],
            # Else branch: general support
            else_steps=[
                Step(name="GeneralSupport", agent=general_support_agent),
            ],
        ),
        Step(name="FollowUp", agent=followup_agent),
    ],
)

# Technical query -> executes Diagnose, Engineer, then FollowUp
workflow.print_response("My app keeps crashing with a timeout error")

# Non-technical query -> executes GeneralSupport, then FollowUp
workflow.print_response("How do I change my shipping address?")
```

## Developer Resources

* [Condition Steps Workflow](/workflows/usage/condition-steps-workflow-stream)
* [Condition with List of Steps](/workflows/usage/condition-with-list-of-steps)

## Reference

For complete API documentation, see [Condition Steps Reference](/reference/workflows/conditional-steps).
