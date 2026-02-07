# AuthorizationConfig

**Source:** https://docs.agno.com/reference/agent-os/authorization-config.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AuthorizationConfig

Configuration for JWT verification when RBAC authorization is enabled on AgentOS.

## Import

```python  theme={null}
from agno.os.config import AuthorizationConfig
```

## Parameters

| Parameter           | Type                  | Default | Description                                                                                                                                                                                                                                                        |
| ------------------- | --------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `verification_keys` | `Optional[List[str]]` | `None`  | List of keys used to verify JWT signatures. For asymmetric algorithms (e.g. RS256), use public keys. For symmetric algorithms (e.g. HS256), use shared secrets. Each key is tried in order until one succeeds - useful for accepting tokens from multiple issuers. |
| `jwks_file`         | `Optional[str]`       | `None`  | Path to a static JWKS (JSON Web Key Set) file containing public keys. Keys are matched by `kid` (key ID) from the JWT header. Alternative to `verification_keys` for RSA key management.                                                                           |
| `algorithm`         | `Optional[str]`       | `RS256` | JWT algorithm for token verification. Common options: `RS256` (asymmetric), `HS256` (symmetric).                                                                                                                                                                   |
| `verify_audience`   | `Optional[bool]`      | `False` | Whether to verify the audience claim of the JWT token. This should not be enabled for AgentOS Control Plane traffic.                                                                                                                                               |

## Usage

```python  theme={null}
from agno.os import AgentOS
from agno.os.config import AuthorizationConfig

agent_os = AgentOS(
    id="my-agent-os",
    agents=[my_agent],
    authorization=True,
    authorization_config=AuthorizationConfig(
        verification_keys=["your-public-key-or-secret"],
        algorithm="RS256",
    ),
)
```

## Algorithm Options

| Algorithm | Type               | Key Format              |
| --------- | ------------------ | ----------------------- |
| `RS256`   | Asymmetric (RSA)   | Public key (PEM format) |
| `RS384`   | Asymmetric (RSA)   | Public key (PEM format) |
| `RS512`   | Asymmetric (RSA)   | Public key (PEM format) |
| `HS256`   | Symmetric (HMAC)   | Shared secret string    |
| `HS384`   | Symmetric (HMAC)   | Shared secret string    |
| `HS512`   | Symmetric (HMAC)   | Shared secret string    |
| `ES256`   | Asymmetric (ECDSA) | Public key (PEM format) |
| `ES384`   | Asymmetric (ECDSA) | Public key (PEM format) |
| `ES512`   | Asymmetric (ECDSA) | Public key (PEM format) |

## Examples

### Using RS256 (Asymmetric)

```python  theme={null}
# RS256 with a public key
authorization_config = AuthorizationConfig(
    verification_keys=["""-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA...
-----END PUBLIC KEY-----"""],
    algorithm="RS256",
)
```

### Using HS256 (Symmetric)

```python  theme={null}
# HS256 with a shared secret
authorization_config = AuthorizationConfig(
    verification_keys=["your-256-bit-secret-key"],
    algorithm="HS256",
)
```

### Using JWKS File

```python  theme={null}
# RS256 with a JWKS file
authorization_config = AuthorizationConfig(
    jwks_file="/path/to/jwks.json",
    algorithm="RS256",
)
```

The JWKS file should follow the standard format:

```json  theme={null}
{
  "keys": [
    {
      "kty": "RSA",
      "kid": "my-key-id",
      "use": "sig",
      "alg": "RS256",
      "n": "0vx7agoebGc...",
      "e": "AQAB"
    }
  ]
}
```

## See Also

* [Security Overview](/agent-os/security/overview) - AgentOS security overview
* [RBAC Documentation](/agent-os/security/rbac) - Complete RBAC scopes and permissions
* [JWT Middleware](/agent-os/middleware/jwt) - Advanced JWT configuration
* [JWTMiddleware Reference](/reference/agent-os/jwt-middleware) - Middleware class reference
