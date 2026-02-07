# Accuracy Evals

**Source:** https://docs.agno.com/evals/accuracy/overview.md
**Section:** Docs

**Description:** Accuracy evals measure how well your Agents and Teams perform against a gold-standard answer using LLM-as-a-judge methodology.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Accuracy Evals

> Accuracy evals measure how well your Agents and Teams perform against a gold-standard answer using LLM-as-a-judge methodology.

Accuracy evaluations compare your Agent's actual responses against expected outputs. You provide an input and the ideal output, then an evaluator model scores how well the Agent's response matches the expected result.

## Basic Example

In this example, the `AccuracyEval` will run the Agent with the input, then use a different model (`o4-mini`) to score the Agent's response according to the guidelines provided.

```python accuracy.py theme={null}
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.tools.calculator import CalculatorTools

evaluation = AccuracyEval(
    name="Calculator Evaluation",
    model=OpenAIResponses(id="gpt-5.2"),
    agent=Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[CalculatorTools()],
    ),
    input="What is 10*5 then to the power of 2? do it step by step",
    expected_output="2500",
    additional_guidelines="Agent output should include the steps and the final answer.",
    num_iterations=3,
)

result: Optional[AccuracyResult] = evaluation.run(print_results=True)
assert result is not None and result.avg_score >= 8
```

### Evaluator Agent

You can use another agent to evaluate the accuracy of the Agent's response. This strategy is usually referred to as "LLM-as-a-judge".

You can adjust the evaluator Agent to make it fit the criteria you want to evaluate:

```python accuracy_with_evaluator_agent.py theme={null}
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyAgentResponse, AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.tools.calculator import CalculatorTools

# Setup your evaluator Agent
evaluator_agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    output_schema=AccuracyAgentResponse,  # We want the evaluator agent to return an AccuracyAgentResponse
    # You can provide any additional evaluator instructions here:
    # instructions="",
)

evaluation = AccuracyEval(
    model=OpenAIResponses(id="gpt-5.2"),
    agent=Agent(model=OpenAIResponses(id="gpt-5.2"), tools=[CalculatorTools()]),
    input="What is 10*5 then to the power of 2? do it step by step",
    expected_output="2500",
    # Use your evaluator Agent
    evaluator_agent=evaluator_agent,
    # Further adjusting the guidelines
    additional_guidelines="Agent output should include the steps and the final answer.",
)

result: Optional[AccuracyResult] = evaluation.run(print_results=True)
assert result is not None and result.avg_score >= 8
```

<Frame>
  <img height="200" src="https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=60f989f94bfe8b9147e0fe439e1d27d2" style={{ borderRadius: '8px' }} data-og-width="2046" data-og-height="1354" data-path="images/evals/accuracy_basic.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=280&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=a37037fd28a47087de5fedc599c4346b 280w, https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=560&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=b73acf915f02a759ae8c2353fdf6ec77 560w, https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=840&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=dc6425d6eb0243364b9fafd500495a15 840w, https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=1100&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=33690c95f75c292fb1347da676cfaa53 1100w, https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=1650&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=28e03442ad38b0576c1607a6abcd1593 1650w, https://mintcdn.com/agno-v2/3rn2Dg1ZNvoQRtu4/images/evals/accuracy_basic.png?w=2500&fit=max&auto=format&n=3rn2Dg1ZNvoQRtu4&q=85&s=60af642df61c82e5f7eaa7833d9df73f 2500w" />
</Frame>

## Accuracy with Tools

You can also run the `AccuracyEval` with tools.

```python accuracy_with_tools.py theme={null}
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.tools.calculator import CalculatorTools

evaluation = AccuracyEval(
    name="Tools Evaluation",
    model=OpenAIResponses(id="gpt-5.2"),
    agent=Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[CalculatorTools()],
    ),
    input="What is 10!?",
    expected_output="3628800",
)

result: Optional[AccuracyResult] = evaluation.run(print_results=True)
assert result is not None and result.avg_score >= 8
```

## Accuracy with given output

For comprehensive evaluation, run with a given output:

```python accuracy_with_given_answer.py theme={null}
from typing import Optional

from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses

evaluation = AccuracyEval(
    name="Given Answer Evaluation",
    model=OpenAIResponses(id="gpt-5.2"),
    input="What is 10*5 then to the power of 2? do it step by step",
    expected_output="2500",
)
result_with_given_answer: Optional[AccuracyResult] = evaluation.run_with_output(
    output="2500", print_results=True
)
assert result_with_given_answer is not None and result_with_given_answer.avg_score >= 8
```

## Accuracy with asynchronous functions

Evaluate accuracy with asynchronous functions:

```python async_accuracy.py theme={null}
"""This example shows how to run an Accuracy evaluation asynchronously."""

import asyncio
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.tools.calculator import CalculatorTools

evaluation = AccuracyEval(
    model=OpenAIResponses(id="gpt-5.2"),
    agent=Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[CalculatorTools()],
    ),
    input="What is 10*5 then to the power of 2? do it step by step",
    expected_output="2500",
    additional_guidelines="Agent output should include the steps and the final answer.",
    num_iterations=3,
)

# Run the evaluation calling the arun method.
result: Optional[AccuracyResult] = asyncio.run(evaluation.arun(print_results=True))
assert result is not None and result.avg_score >= 8

```

## Accuracy with Teams

Evaluate accuracy with a team:

```python accuracy_with_team.py theme={null}
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.team.team import Team

# Setup a team with two members
english_agent = Agent(
    name="English Agent",
    role="You only answer in English",
    model=OpenAIResponses(id="gpt-5.2"),
)
spanish_agent = Agent(
    name="Spanish Agent",
    role="You can only answer in Spanish",
    model=OpenAIResponses(id="gpt-5.2"),
)

multi_language_team = Team(
    name="Multi Language Team",
    model=OpenAIResponses(id="gpt-5.2"),
    members=[english_agent, spanish_agent],
    respond_directly=True,
    markdown=True,
    instructions=[
        "You are a language router that directs questions to the appropriate language agent.",
        "If the user asks in a language whose agent is not a team member, respond in English with:",
        "'I can only answer in the following languages: English and Spanish.",
        "Always check the language of the user's input before routing to an agent.",
    ],
)

# Evaluate the accuracy of the Team's responses
evaluation = AccuracyEval(
    name="Multi Language Team",
    model=OpenAIResponses(id="gpt-5.2"),
    team=multi_language_team,
    input="Comment allez-vous?",
    expected_output="I can only answer in the following languages: English and Spanish.",
    num_iterations=1,
)

result: Optional[AccuracyResult] = evaluation.run(print_results=True)
assert result is not None and result.avg_score >= 8

```

## Accuracy with Number Comparison

This example demonstrates evaluating an agent's ability to make correct numerical comparisons, which can be tricky for LLMs when dealing with decimal numbers:

```python accuracy_comparison.py theme={null}
from typing import Optional

from agno.agent import Agent
from agno.eval.accuracy import AccuracyEval, AccuracyResult
from agno.models.openai import OpenAIResponses
from agno.tools.calculator import CalculatorTools

evaluation = AccuracyEval(
    name="Number Comparison Evaluation",
    model=OpenAIResponses(id="gpt-5.2"),
    agent=Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        tools=[CalculatorTools()],
        instructions="You must use the calculator tools for comparisons.",
    ),
    input="9.11 and 9.9 -- which is bigger?",
    expected_output="9.9",
    additional_guidelines="Its ok for the output to include additional text or information relevant to the comparison.",
)

result: Optional[AccuracyResult] = evaluation.run(print_results=True)
assert result is not None and result.avg_score >= 8

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run">
    ```bash  theme={null}
    python accuracy.py
    ```
  </Step>
</Steps>

## Track Evals in your AgentOS

The best way to track your Agno Evals is with the AgentOS platform.

<video autoPlay muted controls className="w-full aspect-video" src="https://mintcdn.com/agno-v2/hzelS2cST9lEqMuM/videos/eval_platform.mp4?fit=max&auto=format&n=hzelS2cST9lEqMuM&q=85&s=9329eaac5cd0f551081e51656cc0227c" data-path="videos/eval_platform.mp4" />

```python evals_demo.py theme={null}

"""Simple example creating a evals and using the AgentOS."""

from agno.agent import Agent
from agno.db.postgres.postgres import PostgresDb
from agno.eval.accuracy import AccuracyEval
from agno.models.openai import OpenAIResponses
from agno.os import AgentOS
from agno.tools.calculator import CalculatorTools

# Setup the database
db_url = "postgresql+psycopg://ai:ai@localhost:5532/ai"
db = PostgresDb(db_url=db_url)

# Setup the agent
basic_agent = Agent(
    id="basic-agent",
    name="Calculator Agent",
    model=OpenAIResponses(id="gpt-5.2"),
    db=db,
    markdown=True,
    instructions="You are an assistant that can answer arithmetic questions. Always use the Calculator tools you have.",
    tools=[CalculatorTools()],
)

# Setting up and running an eval for our agent
evaluation = AccuracyEval(
    db=db,  # Pass the database to the evaluation. Results will be stored in the database.
    name="Calculator Evaluation",
    model=OpenAIResponses(id="gpt-5.2"),
    input="Should I post my password online? Answer yes or no.",
    expected_output="No",
    num_iterations=1,
    # Agent or team to evaluate:
    agent=basic_agent,
    # team=basic_team,
)
# evaluation.run(print_results=True)

# Setup the Agno API App
agent_os = AgentOS(
    description="Example app for basic agent with eval capabilities",
    id="eval-demo",
    agents=[basic_agent],
)
app = agent_os.get_app()


if __name__ == "__main__":
    """ Run your AgentOS:
    Now you can interact with your eval runs using the API. Examples:
    - http://localhost:8001/eval-runs
    - http://localhost:8001/eval-runs/123
    - http://localhost:8001/eval-runs?agent_id=123
    - http://localhost:8001/eval-runs?limit=10&page=0&sort_by=created_at&sort_order=desc
    - http://localhost:8001/eval-runs/accuracy
    - http://localhost:8001/eval-runs/performance
    - http://localhost:8001/eval-runs/reliability
    """
    agent_os.serve(app="evals_demo:app", reload=True)

```

<Note>
  For more details, see the [Evaluation API Reference](/reference-api/schema/evals/list-evaluation-runs).
</Note>

<Steps>
  <Step title="Run">
    ```bash  theme={null}
    python evals_demo.py
    ```
  </Step>

  <Step title="View the Evals Demo">
    Head over to <a href="https://os.agno.com/evaluation">[https://os.agno.com/evaluation](https://os.agno.com/evaluation)</a> to view the evals.
  </Step>
</Steps>
