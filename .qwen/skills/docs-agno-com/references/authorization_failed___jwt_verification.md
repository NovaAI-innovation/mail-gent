# Authorization Failed - JWT Verification

**Source:** https://docs.agno.com/faq/rbac-auth-failed.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Authorization Failed - JWT Verification

If you are experiencing authorization failures when both security key and authorization are enabled in your AgentOS, this guide will help you resolve the issue.

## The Issue

When both security key authentication and authorization are enabled simultaneously, you may encounter an authorization failed error:

<img src="https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=0ff5ba9a0d2d58299a278faa4dba1369" alt="Authorization Failed Error" data-og-width="507" width="507" data-og-height="355" height="355" data-path="images/auth-failed.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=280&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=326be178c0a346567da6488e652a51b1 280w, https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=560&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=fd51cbaff872ef1be77c6296bf83cc07 560w, https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=840&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=a5dd641db8eabbc3aee1f13718090c6e 840w, https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=1100&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=3efa778ba8a6ce4d85aa8f871b7b8444 1100w, https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=1650&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=4f697a23a2da8b6303ea3a7351aa195a 1650w, https://mintcdn.com/agno-v2/ReEksY_AYjeI43lH/images/auth-failed.png?w=2500&fit=max&auto=format&n=ReEksY_AYjeI43lH&q=85&s=6af1346cf5db98c4a6cbb8ffdebed044 2500w" />

This occurs because authorization is preferred over security key. Learn more about [security key](https://docs.agno.com/agent-os/security/overview#security-key-authentication).

## Solution

The solution depends on your AgentOS version:

### For Older Versions (Before v2.3.13)

If you are running an AgentOS version older than **v2.3.13**, the platform only supports security key authentication.

<Accordion title="Switch Off Authorization" defaultOpen={true}>
  1. **Disable Authorization** on the AgentOS Control Plane
  2. Continue using security key authentication only
</Accordion>

### For Newer Versions <Badge icon="code-branch" color="orange"><Tooltip tip="Introduced in v2.3.13" cta="View release notes" href="https://github.com/agno-agi/agno/releases/tag/v2.3.13">v2.3.13</Tooltip></Badge> and Later

If you are running AgentOS version **v2.3.13** or newer, you have two options to resolve this conflict:

<Note>
  Authorization (JWT verification) is preferred over security key authentication as it provides fine-grained permissions of RBAC.
</Note>

<AccordionGroup>
  <Accordion title="Option 1: Switch Off Authorization">
    If you want to continue using security key authentication:

    1. **Disable Authorization** from the AgentOS Control Plane
    2. Continue using security key authentication only
  </Accordion>

  <Accordion title="Option 2: Switch to Authorization (Preferred)" defaultOpen={true}>
    If you want to use Authorization with JWT verification:

    1. **Disable security key authentication** from the AgentOS Control Plane
    2. **Unset the security key** from your environment:

    ```bash  theme={null}
    # Remove the old security key
    unset OS_SECURITY_KEY
    ```

    3. **Ensure Authorization is enabled** on the AgentOS Control Plane and set the verification key. [More info](https://docs.agno.com/agent-os/security/overview#switching-to-rbac)

    ```bash  theme={null}
    # Set the new JWT verification key
    export JWT_VERIFICATION_KEY="your-public-key"
    ```
  </Accordion>
</AccordionGroup>

## Next Steps

* [JWT Authorization configuration](https://docs.agno.com/agent-os/security/overview)
* [Migration to RBAC](https://docs.agno.com/agent-os/security/overview#switching-to-rbac)
