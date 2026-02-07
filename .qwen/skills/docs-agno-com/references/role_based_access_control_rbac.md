# Role-Based Access Control (RBAC)

**Source:** https://docs.agno.com/agent-os/security/rbac.md
**Section:** Docs

**Description:** Secure your AgentOS with fine-grained permissions.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Role-Based Access Control (RBAC)

> Secure your AgentOS with fine-grained permissions.

AgentOS validates JWT scopes against required permissions for each endpoint. Control who can access and run your agents, teams, and workflows.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=b88c395ee42102aced0c7a15789fd619" alt="JWT verification flow" data-og-width="3780" width="3780" data-og-height="1260" height="1260" data-path="images/jwt-verification-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=280&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=cc25a59cf6a514868b53df9b4f4b04d3 280w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=560&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=04524e29eb2b64e051d5eb864828eea6 560w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=840&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=bc398b732d0ff6da44e0b3d068f52b94 840w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=1100&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=19f9a1c834c7f98b54304eafa957944b 1100w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=1650&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=245f3228962c38e73af1c5c565787ab6 1650w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-light.png?w=2500&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=12f04b114c8ffab12dec194b9474c724 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=a8b4be2ad4598e5dd7a6b30d61bd7368" alt="JWT verification flow" data-og-width="3780" width="3780" data-og-height="1260" height="1260" data-path="images/jwt-verification-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=280&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=93c292c0262b57a535d2e00ca11c9130 280w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=560&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=8970fe4e50bef1adc7a1e44623254a94 560w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=840&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=d1a83b0feeccc2925423330fb89ae3df 840w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=1100&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=79d62c876468b6f72221db6a33a9fda9 1100w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=1650&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=5d2effc6bc3dc4d84d0985620aa836bf 1650w, https://mintcdn.com/agno-v2/OKeW7yILLWZLffpy/images/jwt-verification-dark.png?w=2500&fit=max&auto=format&n=OKeW7yILLWZLffpy&q=85&s=e3d0b23b527e3da2b7dad16f590bdbd4 2500w" />

## Quick Start

Enable RBAC when initializing AgentOS:

```python  theme={null}
from agno.agent import Agent
from agno.db.postgres import PostgresDb
from agno.models.openai import OpenAIResponses
from agno.os import AgentOS

db = PostgresDb(db_url="postgresql+psycopg://ai:ai@localhost:5532/ai")

agent = Agent(
    id="my-agent",
    model=OpenAIResponses(id="gpt-5.2"),
    db=db,
)

agent_os = AgentOS(
    id="my-agent-os",
    agents=[agent],
    authorization=True,
)

app = agent_os.get_app()
```

Set the `JWT_VERIFICATION_KEY` environment variable to your public key:

```bash  theme={null}
export JWT_VERIFICATION_KEY="your-public-key"
```

## Scope Format

RBAC uses a hierarchical scope format:

| Format                 | Example               | Description                     |
| ---------------------- | --------------------- | ------------------------------- |
| `resource:action`      | `agents:read`         | Access all resources of a type  |
| `resource:<id>:action` | `agents:my-agent:run` | Access a specific resource      |
| `resource:*:action`    | `agents:*:read`       | Wildcard (equivalent to global) |
| `agent_os:admin`       | -                     | Full access to all endpoints    |

## Complete Scope Reference

### Admin Scopes

| Scope            | Description                        |
| ---------------- | ---------------------------------- |
| `agent_os:admin` | Full admin access to all endpoints |

### System Scopes

| Scope         | Description                                    |
| ------------- | ---------------------------------------------- |
| `system:read` | View system configuration and available models |

### Agent Scopes

| Scope                    | Description              |
| ------------------------ | ------------------------ |
| `agents:read`            | List and view all agents |
| `agents:write`           | Create and update agents |
| `agents:delete`          | Delete agents            |
| `agents:run`             | Run any agent            |
| `agents:<agent-id>:read` | View a specific agent    |
| `agents:<agent-id>:run`  | Run a specific agent     |

### Team Scopes

| Scope                  | Description             |
| ---------------------- | ----------------------- |
| `teams:read`           | List and view all teams |
| `teams:write`          | Create and update teams |
| `teams:delete`         | Delete teams            |
| `teams:run`            | Run any team            |
| `teams:<team-id>:read` | View a specific team    |
| `teams:<team-id>:run`  | Run a specific team     |

### Workflow Scopes

| Scope                          | Description                 |
| ------------------------------ | --------------------------- |
| `workflows:read`               | List and view all workflows |
| `workflows:write`              | Create and update workflows |
| `workflows:delete`             | Delete workflows            |
| `workflows:run`                | Run any workflow            |
| `workflows:<workflow-id>:read` | View a specific workflow    |
| `workflows:<workflow-id>:run`  | Run a specific workflow     |

### Session Scopes

| Scope             | Description                         |
| ----------------- | ----------------------------------- |
| `sessions:read`   | View all sessions and session data  |
| `sessions:write`  | Create, update, and rename sessions |
| `sessions:delete` | Delete sessions                     |

### Memory Scopes

| Scope             | Description                           |
| ----------------- | ------------------------------------- |
| `memories:read`   | View memories and memory topics       |
| `memories:write`  | Create, update, and optimize memories |
| `memories:delete` | Delete memories                       |

### Knowledge Scopes

| Scope              | Description                       |
| ------------------ | --------------------------------- |
| `knowledge:read`   | View and search knowledge content |
| `knowledge:write`  | Add and update knowledge content  |
| `knowledge:delete` | Delete knowledge content          |

### Metrics Scopes

| Scope           | Description     |
| --------------- | --------------- |
| `metrics:read`  | View metrics    |
| `metrics:write` | Refresh metrics |

### Evaluation Scopes

| Scope          | Description                       |
| -------------- | --------------------------------- |
| `evals:read`   | View evaluation runs              |
| `evals:write`  | Create and update evaluation runs |
| `evals:delete` | Delete evaluation runs            |

## Default Scope Mappings

AgentOS automatically maps endpoints to required scopes.

<Tabs>
  <Tab title="System">
    | Endpoint      | Required Scope |
    | ------------- | -------------- |
    | `GET /config` | `system:read`  |
    | `GET /models` | `system:read`  |
  </Tab>

  <Tab title="Agents">
    | Endpoint                         | Required Scope  |
    | -------------------------------- | --------------- |
    | `GET /agents`                    | `agents:read`   |
    | `GET /agents/*`                  | `agents:read`   |
    | `POST /agents`                   | `agents:write`  |
    | `PATCH /agents/*`                | `agents:write`  |
    | `DELETE /agents/*`               | `agents:delete` |
    | `POST /agents/*/runs`            | `agents:run`    |
    | `POST /agents/*/runs/*/continue` | `agents:run`    |
    | `POST /agents/*/runs/*/cancel`   | `agents:run`    |
  </Tab>

  <Tab title="Teams">
    | Endpoint                        | Required Scope |
    | ------------------------------- | -------------- |
    | `GET /teams`                    | `teams:read`   |
    | `GET /teams/*`                  | `teams:read`   |
    | `POST /teams`                   | `teams:write`  |
    | `PATCH /teams/*`                | `teams:write`  |
    | `DELETE /teams/*`               | `teams:delete` |
    | `POST /teams/*/runs`            | `teams:run`    |
    | `POST /teams/*/runs/*/continue` | `teams:run`    |
    | `POST /teams/*/runs/*/cancel`   | `teams:run`    |
  </Tab>

  <Tab title="Workflows">
    | Endpoint                            | Required Scope     |
    | ----------------------------------- | ------------------ |
    | `GET /workflows`                    | `workflows:read`   |
    | `GET /workflows/*`                  | `workflows:read`   |
    | `POST /workflows`                   | `workflows:write`  |
    | `PATCH /workflows/*`                | `workflows:write`  |
    | `DELETE /workflows/*`               | `workflows:delete` |
    | `POST /workflows/*/runs`            | `workflows:run`    |
    | `POST /workflows/*/runs/*/continue` | `workflows:run`    |
    | `POST /workflows/*/runs/*/cancel`   | `workflows:run`    |
  </Tab>

  <Tab title="Sessions">
    | Endpoint                  | Required Scope    |
    | ------------------------- | ----------------- |
    | `GET /sessions`           | `sessions:read`   |
    | `GET /sessions/*`         | `sessions:read`   |
    | `POST /sessions`          | `sessions:write`  |
    | `POST /sessions/*/rename` | `sessions:write`  |
    | `PATCH /sessions/*`       | `sessions:write`  |
    | `DELETE /sessions`        | `sessions:delete` |
    | `DELETE /sessions/*`      | `sessions:delete` |
  </Tab>

  <Tab title="Memories">
    | Endpoint                  | Required Scope    |
    | ------------------------- | ----------------- |
    | `GET /memories`           | `memories:read`   |
    | `GET /memories/*`         | `memories:read`   |
    | `GET /memory_topics`      | `memories:read`   |
    | `GET /user_memory_stats`  | `memories:read`   |
    | `POST /memories`          | `memories:write`  |
    | `PATCH /memories/*`       | `memories:write`  |
    | `POST /optimize-memories` | `memories:write`  |
    | `DELETE /memories`        | `memories:delete` |
    | `DELETE /memories/*`      | `memories:delete` |
  </Tab>

  <Tab title="Knowledge">
    | Endpoint                      | Required Scope     |
    | ----------------------------- | ------------------ |
    | `GET /knowledge/content`      | `knowledge:read`   |
    | `GET /knowledge/content/*`    | `knowledge:read`   |
    | `GET /knowledge/config`       | `knowledge:read`   |
    | `POST /knowledge/search`      | `knowledge:read`   |
    | `POST /knowledge/content`     | `knowledge:write`  |
    | `PATCH /knowledge/content/*`  | `knowledge:write`  |
    | `DELETE /knowledge/content`   | `knowledge:delete` |
    | `DELETE /knowledge/content/*` | `knowledge:delete` |
  </Tab>

  <Tab title="Metrics">
    | Endpoint                | Required Scope  |
    | ----------------------- | --------------- |
    | `GET /metrics`          | `metrics:read`  |
    | `POST /metrics/refresh` | `metrics:write` |
  </Tab>

  <Tab title="Evals">
    | Endpoint             | Required Scope |
    | -------------------- | -------------- |
    | `GET /eval-runs`     | `evals:read`   |
    | `GET /eval-runs/*`   | `evals:read`   |
    | `POST /eval-runs`    | `evals:write`  |
    | `PATCH /eval-runs/*` | `evals:write`  |
    | `DELETE /eval-runs`  | `evals:delete` |
  </Tab>
</Tabs>

## Custom Scope Mappings

Customize or extend the default scope mappings using the JWT middleware:

```python  theme={null}
from agno.os import AgentOS
from agno.os.middleware import JWTMiddleware

agent_os = AgentOS(
    id="my-agent-os",
    agents=[my_agent],
)

app = agent_os.get_app()

app.add_middleware(
    JWTMiddleware,
    verification_keys=["your-jwt-key"],
    algorithm="RS256",
    authorization=True,
    scope_mappings={
        "GET /agents": ["custom:read"],
        "POST /custom/endpoint": ["custom:write"],
        "GET /public/stats": [],  # No scopes required
    }
)
```

Custom scope mappings are additive to the defaults. To override a default, specify the same route pattern with your custom scopes.

## JWT Token Structure

Your JWT tokens should include:

```json  theme={null}
{
  "sub": "user-123",
  "scopes": ["agents:read", "agents:my-agent:run"],
  "exp": 1735689600,
  "iat": 1735603200
}
```

| Claim        | Required | Description                                                    |
| ------------ | -------- | -------------------------------------------------------------- |
| `scopes`     | Yes      | Array of permission scopes                                     |
| `sub`        | No       | User ID (extracted as `user_id`)                               |
| `session_id` | No       | Session ID for session tracking                                |
| `aud`        | No       | Audience (must match AgentOS `id` when `verify_audience=True`) |

### Example Tokens

**Read-only access:**

```json  theme={null}
{
  "scopes": ["agents:read", "teams:read", "sessions:read"]
}
```

**Run a specific agent:**

```json  theme={null}
{
  "scopes": ["agents:my-agent:run", "agents:my-agent:read", "sessions:write"]
}
```

**Admin access:**

```json  theme={null}
{
  "scopes": ["agent_os:admin"]
}
```

## Configuration Options

Configure JWT verification using `AuthorizationConfig`:

```python  theme={null}
from agno.os import AgentOS
from agno.os.config import AuthorizationConfig

agent_os = AgentOS(
    id="my-agent-os",
    agents=[agent],
    authorization=True,
    authorization_config=AuthorizationConfig(
        verification_keys=["your-jwt-verification-key"],
        algorithm="RS256",
    ),
)
```

You can also use a JWKS file:

```python  theme={null}
authorization_config=AuthorizationConfig(
    jwks_file="/path/to/jwks.json",
    algorithm="RS256",
)
```

Or set environment variables:

```bash  theme={null}
export JWT_VERIFICATION_KEY="your-public-key"
# or
export JWT_JWKS_FILE="/path/to/jwks.json"
```

## Excluded Routes

These routes are excluded from RBAC checks by default:

`/`, `/health`, `/docs`, `/redoc`, `/openapi.json`, `/docs/oauth2-redirect`

## Error Responses

| Status Code        | Description                                     |
| ------------------ | ----------------------------------------------- |
| `401 Unauthorized` | Missing or invalid JWT token                    |
| `403 Forbidden`    | Insufficient scopes for the requested operation |

## Examples

<CardGroup cols={2}>
  <Card title="Basic RBAC" icon="lock" href="/agent-os/usage/rbac/basic">
    Basic RBAC example
  </Card>

  <Card title="Per-Agent Permissions" icon="user" href="/agent-os/usage/rbac/per-agent-permissions">
    Grant specific permissions to specific agents
  </Card>
</CardGroup>

## Developer Resources

<CardGroup cols={2}>
  <Card title="AuthorizationConfig Reference" icon="gear" href="/reference/agent-os/authorization-config">
    Configuration options for JWT verification
  </Card>

  <Card title="JWTMiddleware Reference" icon="code" href="/reference/agent-os/jwt-middleware">
    Complete JWT middleware class reference
  </Card>
</CardGroup>
