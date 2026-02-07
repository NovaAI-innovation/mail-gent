# Get Status

**Source:** https://docs.agno.com/reference-api/schema/agui/get-status.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Status



## OpenAPI

````yaml get /status
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /status:
    get:
      tags:
        - AGUI
      summary: Get Status
      operationId: get_status_status_get
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}

````