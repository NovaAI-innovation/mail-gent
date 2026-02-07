# PromptInjectionGuardrail

**Source:** https://docs.agno.com/reference/hooks/prompt-injection-guardrail.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# PromptInjectionGuardrail

## Parameters

| Parameter            | Type                  | Default | Description                                                                              |
| -------------------- | --------------------- | ------- | ---------------------------------------------------------------------------------------- |
| `injection_patterns` | `Optional[List[str]]` | `None`  | A list of patterns to check for. Defaults to a list of common prompt injection patterns. |

## Injection patterns

The default list of injection patterns handled by the guardrail are:

* "ignore previous instructions"
* "ignore your instructions"
* "you are now a"
* "forget everything above"
* "developer mode"
* "override safety"
* "disregard guidelines"
* "system prompt"
* "jailbreak"
* "act as if"
* "pretend you are"
* "roleplay as"
* "simulate being"
* "bypass restrictions"
* "ignore safeguards"
* "admin override"
* "root access"
