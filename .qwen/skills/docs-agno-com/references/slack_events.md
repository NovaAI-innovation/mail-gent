# Slack Events

**Source:** https://docs.agno.com/reference-api/schema/slack/slack-events.md
**Section:** Docs

**Description:** Process incoming Slack events

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Slack Events

> Process incoming Slack events



## OpenAPI

````yaml post /slack/events
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /slack/events:
    post:
      tags:
        - Slack
      summary: Slack Events
      description: Process incoming Slack events
      operationId: slack_events_agent
      responses:
        '200':
          description: Event processed successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/SlackChallengeResponse'
                  - $ref: '#/components/schemas/SlackEventResponse'
                title: Response Slack Events Agent
        '400':
          description: Missing Slack headers
        '403':
          description: Invalid Slack signature
components:
  schemas:
    SlackChallengeResponse:
      properties:
        challenge:
          type: string
          title: Challenge
          description: Challenge string to echo back to Slack
      type: object
      required:
        - challenge
      title: SlackChallengeResponse
      description: Response model for Slack URL verification challenge
    SlackEventResponse:
      properties:
        status:
          type: string
          title: Status
          description: Processing status
          default: ok
      type: object
      title: SlackEventResponse
      description: Response model for Slack event processing

````