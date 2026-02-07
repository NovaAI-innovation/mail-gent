# AgentOS Security

**Source:** https://docs.agno.com/agent-os/security/overview.md
**Section:** Docs

**Description:** Secure your AgentOS with authentication and authorization.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentOS Security

> Secure your AgentOS with authentication and authorization.

AgentOS supports two security mechanisms:

| Method                   | Use Case                                                          |
| ------------------------ | ----------------------------------------------------------------- |
| **Basic Authentication** | Simple key validation for development                             |
| **RBAC**                 | JWT-powered authorization with fine-grained scopes for production |

## Basic Authentication

Set the `OS_SECURITY_KEY` environment variable:

```bash  theme={null}
export OS_SECURITY_KEY="your-secret-key"
```

Requests without a valid `Authorization: Bearer <key>` header return `401 Unauthorized`.

## Role-Based Access Control (RBAC)

RBAC validates JWT tokens and checks scopes against required permissions for each endpoint. Enable it with `authorization=True`:

```python  theme={null}
from agno.os import AgentOS

agent_os = AgentOS(
    id="my-agent-os",
    agents=[my_agent],
    authorization=True,
)
```

Set the `JWT_VERIFICATION_KEY` environment variable to your public key:

```bash  theme={null}
export JWT_VERIFICATION_KEY="your-public-key"
```

You can generate a key pair from the control plane when connecting a new OS or from the Settings page for an existing OS.

<video autoPlay muted controls className="w-full aspect-video" src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/auth-on-connect-web.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=f63fff9fd4eca9e8a0045da2cc2c5a6a" data-path="videos/auth-on-connect-web.mp4" />

Requests without a valid JWT return `401 Unauthorized`. Requests with insufficient scopes return `403 Forbidden`.

See [RBAC Documentation](/agent-os/security/rbac) for scope format, available scopes, and endpoint mappings.

<CardGroup cols={2}>
  <Card title="RBAC Documentation" icon="lock" href="/agent-os/security/rbac">
    Complete scopes, permissions, and access control configuration.
  </Card>

  <Card title="JWT Middleware" icon="key" href="/agent-os/middleware/jwt">
    JWT authentication with parameter injection and claims extraction.
  </Card>
</CardGroup>
