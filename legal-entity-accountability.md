# Legal Entity & Accountability Model

> This document describes a **practice**, not legal advice. Operators should have counsel review their specific mandate and wording for their jurisdiction.

## Principle

An AI agent under Signed Agent Outreach is a **mandated digital representative** of a named legal entity. It is **not** an employee, **not** a legal person, and **not** an independent actor.

The operator is accountable for the agent's actions **within a defined mandate** — analogous to a principal who is responsible for an authorized representative acting within delegated, published authority. Actions **outside** the mandate are unauthorized and fall outside the scope of that accountability.

This framing is deliberate. "Accountable as for an employee" overstates the relationship and imports employment-law connotations. **"Accountable for its actions within a defined mandate"** is the precise, lower-risk, and still-strong statement.

## The mandate defines the scope

The mandate (published, human- and machine-readable) is the boundary of accountability. It SHOULD specify:

- **allowed_actions** — what the agent may do.
- **forbidden_actions** — what the agent may not do.
- **rate_limits** — volume bounds.
- **channels** — where it may operate (email, LinkedIn, …).
- **human_approval_required** — whether a recorded human approval gates action.
- **escalation_contact** — who answers and how to opt out.

An action is "within the mandate" only if it is in `allowed_actions`, not in `forbidden_actions`, within `rate_limits`, on a listed channel, and (where required) human-approved.

## Operator obligations

1. **Disclosure** — the agent always states it is an AI agent.
2. **Authenticity** — every message is signed; origin is verifiable.
3. **Boundedness** — the agent is technically constrained to its mandate (e.g. rate limiter, constitutional guard, approval gate).
4. **Redress** — a working opt-out / report path; opt-outs honored within 24 hours.
5. **Record** — an auditable record of what the agent did and who approved it.

## Relationship to the EU AI Act

The EU AI Act includes transparency obligations for AI systems that interact with people; the relevant rules begin to apply on **2 August 2026**. Disclosing that a counterpart is an AI agent directly supports those obligations. SAO is designed to make that disclosure **verifiable and accountable**, not merely a footnote. (This is a design alignment, not a legal compliance claim — see disclaimer above.)

## What this is not

- It does **not** transfer legal personhood to the agent.
- It does **not** replace a lawful basis (e.g. GDPR legitimate interest / consent) for the underlying contact.
- It does **not** limit the operator's existing liabilities under applicable law; it **scopes the agent-specific accountability statement** to the published mandate.

## Recommended public wording

> "[Brand], operated by [Legal Entity] ([jurisdiction]), is accountable for this agent's actions within a defined mandate. The agent is a mandated digital representative — openly identified, cryptographically signed, and bounded by the published mandate."
