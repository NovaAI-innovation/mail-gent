# Branching Workflow

**Source:** https://docs.agno.com/workflows/workflow-patterns/branching-workflow.md
**Section:** Docs

**Description:** Complex decision trees requiring dynamic path selection based on content analysis

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Branching Workflow

> Complex decision trees requiring dynamic path selection based on content analysis

**Example Use-Cases**: Expert routing, content type detection, multi-path processing

Dynamic routing workflows provide intelligent path selection while maintaining predictable execution within each chosen branch.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=11256e6d5ebe78ee137ba56647bb732c" alt="Workflows router steps diagram" data-og-width="2493" width="2493" data-og-height="921" height="921" data-path="images/workflows-router-steps-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=280&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=bbbf338fb349e3d6e9e66f92873ca74b 280w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=560&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=3c341c1b87faa0eca3092ea8f93c5d0b 560w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=840&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=75dabdfd37b0806915bd56520c176d0a 840w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=1100&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=8e91a1cb88327098c3420a0bd4994e69 1100w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=1650&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=e948b1e5b7f48fde2637265f2daef7f5 1650w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps-light.png?w=2500&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=74139a11491c79a755974923831ad406 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=593bc69b1647af6571151c051145e7c6" alt="Workflows router steps diagram" data-og-width="2493" width="2493" data-og-height="921" height="921" data-path="images/workflows-router-steps.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=280&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=575bc73e719bb2ccf703278e5aaaa4b3 280w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=560&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=6886d723d73a9fc1ffec318b2fe33d3c 560w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=840&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=0c364bb81456fc509a64fcac0cb8373a 840w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=1100&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=d9ede7db094389fc173c590ea28aa21c 1100w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=1650&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=117488ab5bcecbf9e982474dd91580e8 1650w, https://mintcdn.com/agno-v2/6A2IKapU7R02zCpZ/images/workflows-router-steps.png?w=2500&fit=max&auto=format&n=6A2IKapU7R02zCpZ&q=85&s=e0f5a19e133076f0ba74ced4f21ba411 2500w" />

## Selector Flexibility

The Router selector function supports multiple return types:

* **String**: Return step name - Router resolves it from choices
* **Step**: Return Step object directly
* **List\[Step]**: Return list of steps for chaining

The selector can also receive `step_choices` as an optional second parameter for dynamic selection.

## Example: String-based Selector

The simplest approach - return the step name as a string:

```python branching_workflow.py theme={null}
from typing import Union, List

from agno.agent import Agent
from agno.models.openai import OpenAIChat
from agno.workflow.router import Router
from agno.workflow.step import Step
from agno.workflow.types import StepInput
from agno.workflow.workflow import Workflow

tech_expert = Agent(
    name="tech_expert",
    model=OpenAIChat(id="gpt-4o-mini"),
    instructions="You are a tech expert. Provide technical analysis.",
)

biz_expert = Agent(
    name="biz_expert",
    model=OpenAIChat(id="gpt-4o-mini"),
    instructions="You are a business expert. Provide business insights.",
)

generalist = Agent(
    name="generalist",
    model=OpenAIChat(id="gpt-4o-mini"),
    instructions="You are a generalist. Provide general information.",
)

tech_step = Step(name="Tech Research", agent=tech_expert)
business_step = Step(name="Business Research", agent=biz_expert)
general_step = Step(name="General Research", agent=generalist)


def route_by_topic(step_input: StepInput) -> Union[str, Step, List[Step]]:
    """Selector can return step name as string - Router resolves it."""
    topic = step_input.input.lower()

    if "tech" in topic or "ai" in topic or "software" in topic:
        return "Tech Research"  # Return name as string
    elif "business" in topic or "market" in topic or "finance" in topic:
        return "Business Research"
    else:
        return "General Research"


workflow = Workflow(
    name="Expert Routing",
    steps=[
        Router(
            name="Topic Router",
            selector=route_by_topic,
            choices=[tech_step, business_step, general_step],
        ),
    ],
)

workflow.print_response("Latest developments in artificial intelligence", markdown=True)
```

## Example: Using step\_choices Parameter

Access available choices dynamically for more flexible routing:

```python dynamic_routing.py theme={null}
def dynamic_selector(step_input: StepInput, step_choices: list) -> Union[str, Step, List[Step]]:
    """
    Selector receives step_choices - can select by name or return Step directly.
    step_choices contains the prepared Step objects from Router.choices.
    """
    user_input = step_input.input.lower()

    # Build name map from step_choices
    step_map = {s.name: s for s in step_choices if hasattr(s, "name") and s.name}

    # Can return step name as string
    if "research" in user_input:
        return "researcher"

    # Can return Step object directly
    if "write" in user_input:
        return step_map.get("writer", step_choices[0])

    # Can return list of Steps for chaining
    if "full" in user_input:
        return [step_map["researcher"], step_map["writer"], step_map["reviewer"]]

    # Default
    return step_choices[0]


workflow = Workflow(
    name="Dynamic Routing",
    steps=[
        Router(
            name="Dynamic Router",
            selector=dynamic_selector,
            choices=[researcher, writer, reviewer],
        ),
    ],
)
```

## Example: Nested Choices

Nested lists in choices become Steps containers for sequential execution:

```python nested_routing.py theme={null}
def nested_selector(step_input: StepInput, step_choices: list) -> Union[str, Step, List[Step]]:
    """
    When choices contains nested lists like [step_a, [step_b, step_c]],
    the nested list becomes a Steps container in step_choices.
    """
    user_input = step_input.input.lower()

    # step_choices[0] = Step for step_a
    # step_choices[1] = Steps container with [step_b, step_c]

    if "single" in user_input:
        return step_choices[0]  # Just step_a
    else:
        return step_choices[1]  # Steps container: step_b -> step_c


workflow = Workflow(
    name="Nested Choices Routing",
    steps=[
        Router(
            name="Nested Router",
            selector=nested_selector,
            choices=[step_a, [step_b, step_c]],  # Nested list becomes Steps container
        ),
    ],
)
```

## Developer Resources

* [Router Steps Workflow](/workflows/usage/router-steps-workflow)
* [Router with step\_choices](/workflows/usage/router-with-step-choices)

## Reference

For complete API documentation, see [Router Steps Reference](/reference/workflows/router-steps).
