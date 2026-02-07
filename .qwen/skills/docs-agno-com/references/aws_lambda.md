# AWS Lambda

**Source:** https://docs.agno.com/tools/toolkits/others/aws-lambda.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AWS Lambda

## Prerequisites

The following example requires the `boto3` library.

```shell  theme={null}
uv pip install openai boto3
```

## Example

The following agent will use AWS Lambda to list all Lambda functions in our AWS account and invoke a specific Lambda function.

```python cookbook/14_tools/aws_lambda_tools.py theme={null}

from agno.agent import Agent
from agno.tools.aws_lambda import AWSLambdaTools

# Create an Agent with the AWSLambdaTool
agent = Agent(
    tools=[AWSLambdaTools(region_name="us-east-1")],
    name="AWS Lambda Agent",
    )

# Example 1: List all Lambda functions
agent.print_response("List all Lambda functions in our AWS account", markdown=True)

# Example 2: Invoke a specific Lambda function
agent.print_response("Invoke the 'hello-world' Lambda function with an empty payload", markdown=True)
```

## Toolkit Params

| Parameter                | Type   | Default       | Description                                         |
| ------------------------ | ------ | ------------- | --------------------------------------------------- |
| `region_name`            | `str`  | `"us-east-1"` | AWS region name where Lambda functions are located. |
| `enable_list_functions`  | `bool` | `True`        | Enable the list\_functions functionality.           |
| `enable_invoke_function` | `bool` | `True`        | Enable the invoke\_function functionality.          |
| `all`                    | `bool` | `False`       | Enable all functionality.                           |

## Toolkit Functions

| Function          | Description                                                                                                           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| `list_functions`  | Lists all Lambda functions available in the AWS account.                                                              |
| `invoke_function` | Invokes a specific Lambda function with an optional payload. Takes `function_name` and optional `payload` parameters. |

## Developer Resources

* View [Tools](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/aws_lambda.py)
