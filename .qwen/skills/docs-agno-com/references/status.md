# Status

**Source:** https://docs.agno.com/reference-api/schema/whatsapp/status.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Status



## OpenAPI

````yaml get /whatsapp/status
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /whatsapp/status:
    get:
      tags:
        - Whatsapp
      summary: Status
      operationId: status_whatsapp_status_get
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}

````