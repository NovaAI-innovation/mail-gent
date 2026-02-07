# Verify Webhook

**Source:** https://docs.agno.com/reference-api/schema/whatsapp/verify-webhook.md
**Section:** Docs

**Description:** Handle WhatsApp webhook verification

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Verify Webhook

> Handle WhatsApp webhook verification



## OpenAPI

````yaml get /whatsapp/webhook
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /whatsapp/webhook:
    get:
      tags:
        - Whatsapp
      summary: Verify Webhook
      description: Handle WhatsApp webhook verification
      operationId: verify_webhook_whatsapp_webhook_get
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}

````