# AgentOS on AWS

**Source:** https://docs.agno.com/production/templates/aws.md
**Section:** Docs

**Description:** Deploy AgentOS to AWS ECS.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentOS on AWS

> Deploy AgentOS to AWS ECS.

This template deploys AgentOS to AWS with ECS Fargate, RDS PostgreSQL, and an Application Load Balancer. Production-grade infrastructure that runs entirely in your cloud.

## Step-by-step Guide

<Steps>
  <Step title="Install tools">
    * Install [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/)
    * Install [uv](https://docs.astral.sh/uv/) (Python package manager)
    * Install and configure the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
  </Step>

  <Step title="Create and activate a virtual environment">
    ```bash  theme={null}
    uv venv --python 3.12
    source .venv/bin/activate
    ```
  </Step>

  <Step title="Install Agno">
    ```bash  theme={null}
    uv pip install -U 'agno[infra]'
    ```
  </Step>

  <Step title="Create your codebase">
    ```bash  theme={null}
    ag infra create --template agentos-aws --name agentos-aws

    cd agentos-aws
    ```

    <Tip>
      Or clone directly: `git clone https://github.com/agno-agi/agentos-aws-template.git`
    </Tip>
  </Step>

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=sk-***
    ```

    <Tip>
      Agno works with any model provider. Just update the agents in your codebase.
    </Tip>
  </Step>

  <Step title="Configure AWS settings">
    Update `infra/settings.py` with your AWS configuration:

    ```python  theme={null}
    infra_settings = InfraSettings(
        aws_region="us-east-1",
        subnet_ids=["subnet-xxx", "subnet-yyy"],
        image_repo="[ACCOUNT_ID].dkr.ecr.us-east-1.amazonaws.com",
    )
    ```
  </Step>

  <Step title="Test locally (optional)">
    ```bash  theme={null}
    ag infra up
    ```

    Open [http://localhost:8000/docs](http://localhost:8000/docs) to verify it works.
  </Step>

  <Step title="Deploy to AWS">
    ```bash  theme={null}
    ag infra up prd:aws
    ```

    Press Enter to confirm. This creates:

    * Docker image pushed to ECR
    * RDS PostgreSQL instance
    * ECS Cluster, Service, and Task Definition
    * Application Load Balancer with Target Group

    RDS takes about 5 minutes to provision. Monitor progress on the AWS Console.
  </Step>

  <Step title="Get your endpoint">
    Find your Load Balancer DNS in the AWS Console (EC2 → Load Balancers). Navigate to `https://<load-balancer-dns>/docs` to see your AgentOS API.
  </Step>

  <Step title="Connect your AgentOS to the control plane">
    1. Open [os.agno.com](https://os.agno.com)
    2. Click "Connect OS" and select "Live"
    3. Enter your Load Balancer DNS as the endpoint

    <Frame>
      <img src="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=dace555ba53468d3b5d8c8a3a50f9acb" alt="AgentOS connection dialog" data-og-width="2472" width="2472" data-og-height="2408" height="2408" data-path="images/agent-os-connection-dialog.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=280&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=0a6df0f8e440140f73eb1d6b5a9600eb 280w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=560&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=97967d6ed45c07eb13d81eeb39cae267 560w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=840&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=419ccf4c560b3fae2e56fc85659fb8d6 840w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=1100&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=ee04e8acffb1ca82c4091447c6f0e871 1100w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=1650&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=8e647d974cc5b1a1916cc976a86c131a 1650w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=2500&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=e9dcbbeb8274cb21e5dcdc91f3b5d7e7 2500w" />
    </Frame>
  </Step>
</Steps>

## Tips

**Update deployment**: After making changes to your agents:

```bash  theme={null}
ag infra patch prd:aws
```

**Stop deployment**:

```bash  theme={null}
ag infra down prd:aws
```

<Warning>
  This removes all AWS resources including the database. Back up your data first.
</Warning>

**Project structure:**

```
agentos-aws/
├── agents/              # Your agents
├── teams/               # Your teams
├── workflows/           # Your workflows
├── app/                 # AgentOS directory
├── db/                  # Database tables
├── infra/               # AWS infrastructure configuration
│   └── settings.py      # InfraSettings (region, subnets, etc.)
├── compose.yml          # Docker Compose for local testing
├── Dockerfile           # Container build
└── pyproject.toml       # Python dependencies
```

**AWS Resources Created:**

The `ag infra up prd:aws` command provisions:

* **ECR**: Container registry for your Docker image
* **ECS Fargate**: Serverless container hosting
* **RDS PostgreSQL**: Managed database with pgvector
* **Application Load Balancer**: HTTPS endpoint
* **AWS Secrets Manager**: Secure credential storage
* **Security Groups**: Network access controls

**Cost Estimate:**

Estimated monthly costs (US East):

* ECS Fargate: \$30-50
* RDS db.t3.micro: \$15-20
* Load Balancer: \$20-25

Total: \~\$65-100/month. Use the [AWS Pricing Calculator](https://calculator.aws/) for detailed estimates.

## Troubleshooting

<AccordionGroup>
  <Accordion title="RDS not accessible">
    The RDS instance takes about 5 minutes to provision. Check status in the AWS Console (RDS → Databases).
  </Accordion>

  <Accordion title="ECS task failing">
    View task logs in CloudWatch. Common issues: missing environment variables, incorrect database connection string.
  </Accordion>

  <Accordion title="Load Balancer returns 503">
    The ECS service may still be starting. Wait 2-3 minutes for health checks to pass.
  </Accordion>
</AccordionGroup>
