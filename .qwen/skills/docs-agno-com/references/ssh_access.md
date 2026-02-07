# SSH Access

**Source:** https://docs.agno.com/production/aws/ssh-access.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# SSH Access

SSH Access is an important part of the developer workflow.

## Dev SSH Access

SSH into the dev containers using the `docker exec` command

```bash  theme={null}
docker exec -it ai-api zsh
```

## Production SSH Access

Your ECS tasks are already enabled with SSH access. SSH into the production containers using:

```bash  theme={null}
ECS_CLUSTER=ai-app-prd-cluster
TASK_ARN=$(aws ecs list-tasks --cluster ai-app-prd-cluster --query "taskArns[0]" --output text)
CONTAINER_NAME=ai-api-prd

aws ecs execute-command --cluster $ECS_CLUSTER \
    --task $TASK_ARN \
    --container $CONTAINER_NAME \
    --interactive \
    --command "zsh"
```
