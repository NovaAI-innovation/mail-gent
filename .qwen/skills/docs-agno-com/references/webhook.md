# Webhook

**Source:** https://docs.agno.com/reference-api/schema/whatsapp/webhook.md
**Section:** Docs

**Description:** Handle incoming WhatsApp messages

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Webhook

> Handle incoming WhatsApp messages



## OpenAPI

````yaml post /whatsapp/webhook
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /whatsapp/webhook:
    post:
      tags:
        - Whatsapp
      summary: Webhook
      description: Handle incoming WhatsApp messages
      operationId: webhook_whatsapp_webhook_post
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}

````