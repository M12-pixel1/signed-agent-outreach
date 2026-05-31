# Signed Agent Outreach — v0.1 (Draft)

**Status:** Draft / Proposed Standard
**Editors:** Margelis.ai, operated by Rūpestėlis Holding UAB (Vilnius, Lithuania)
**Date:** 2026-05-31
**License:** CC-BY-4.0

## Abstract

Signed Agent Outreach (SAO) defines how an autonomous software agent that contacts people on behalf of an organization (a) identifies itself as an AI agent, (b) proves its origin cryptographically, (c) publishes the mandate that bounds its behavior, and (d) names the legal entity accountable for its actions **within that mandate**.

## 1. Motivation

1.1. Autonomous agents increasingly initiate contact by email, messaging, and voice. The prevailing practice is to conceal that the sender is an agent and to imitate a human.

1.2. This erodes trust, enables impersonation and fraud, and is on a collision course with transparency obligations — including the EU AI Act's rules on AI–human interaction, which begin to apply on **2 August 2026**.

1.3. SAO proposes the opposite default: agents that **disclose, sign, and operate within a published, accountable mandate**.

## 2. Terminology

The key words **MUST**, **MUST NOT**, **SHOULD**, **MAY** are to be interpreted as described in RFC 2119.

- **Agent** — an autonomous software process that initiates contact with a person.
- **Operator** — the legal entity that deploys the agent and is accountable for it.
- **Mandate** — the published, human- and machine-readable definition of what the agent may and may not do.
- **Manifest** — the structured document describing the agent, its operator, its mandate, and its signature (see `agent-manifest.schema.json`).
- **Mandate Page** — a human-readable page, served over HTTPS on a domain the operator controls, rendering the mandate.

## 3. Requirements

A conforming outbound agent:

- **3.1.** MUST clearly disclose, in every message, that it is an AI agent. It MUST NOT impersonate a human or imply that it is one.
- **3.2.** MUST cryptographically sign each message — or produce a verifiable per-message record — using a **published public key**, so a recipient can confirm the message originated from the operator.
- **3.3.** MUST link to a public **Mandate Page**, served over HTTPS on a domain the operator controls.
- **3.4.** MUST name a real **legal entity** (with jurisdiction and a contact/escalation address) accountable for the agent's actions within the mandate.
- **3.5.** MUST operate within its published mandate. Actions outside the mandate are **not authorized**.
- **3.6.** SHOULD require **recorded human approval** before sending outreach to individuals.
- **3.7.** SHOULD enforce and publish **rate limits**.
- **3.8.** MUST provide a low-friction **opt-out / report** path, and SHOULD honor opt-outs within 24 hours.

## 4. The human-readable signature block

Every message MUST carry a short, plain-language block. Example:

```
———
Sent by Legatus — an autonomous outreach agent of Margelis.ai, operated by
Rūpestėlis Holding UAB (Vilnius, Lithuania). This is an AI agent, openly
identified — not a human, and not pretending to be one. Rūpestėlis Holding UAB
is accountable for its actions within a defined mandate.
Cryptographically signed (Sigillum). Verify it, read the agent's mandate, or
report misconduct: https://legatus.rupestelis.com/agent?ref=<message_id>
```

## 5. The Agent Manifest

The machine-readable manifest is defined by [`agent-manifest.schema.json`](./agent-manifest.schema.json). Required fields:

`agent_id`, `agent_name`, `legal_entity`, `public_mandate_url`, `allowed_actions`, `forbidden_actions`, `signature`, `verification`, `issued_at`.

A conforming Mandate Page SHOULD expose the manifest (e.g. at `/.well-known/agent-manifest.json` or linked from the page).

## 6. Accountability model

See [`legal-entity-accountability.md`](./legal-entity-accountability.md). In summary: the agent is a **mandated digital representative** of the operator. The operator is accountable for the agent's actions **within the defined mandate** — not as an employer for an employee, but as a principal for an authorized representative acting within delegated, published authority. Actions outside the mandate are unauthorized and outside the scope of that accountability.

## 7. Verification

See [`verification.md`](./verification.md).

## 8. Non-goals

- SAO does not standardize the agent's task or message content.
- SAO is **not** a substitute for consent or a lawful basis under applicable law (e.g. GDPR).
- SAO does **not** make the agent a legal person.

## 9. Reference implementation

- Live signed agent + Mandate Page: https://legatus.rupestelis.com/agent
- Standard page: https://margelis.ai/signed-agents
- Signing: Sigillum (Ed25519); runtime guard: Antkaklis (rate limits, constitutional gate); human-approval gate before send.

## 10. Status

This is a **proposal under active implementation**. We invite review and adoption. We do not claim priority; we claim accountability.
