# Sign Your Agents — an open call

**A public call to adopt Signed Agent Outreach.** From Margelis.ai (operated by Rūpestėlis Holding UAB, Vilnius). Status: open · License: CC-BY-4.0.

---

## The call

If you deploy AI agents that contact people on your behalf — **sign them.**

Most AI outreach today is built to hide that it's AI and imitate a human. That is a choice. We are asking the industry to make the opposite one, before it becomes a problem for everyone:

> When an AI agent reaches out, it should **disclose** it is an AI, be **cryptographically signed**, carry a **published mandate** of what it may and may not do, and name a **legal entity accountable** for its actions within that mandate.

We are not claiming to be first. We are asking to make this **normal** — and we are doing it ourselves, in the open, so the request is not hypocritical.

## Why now

On **2 August 2026**, the EU AI Act's transparency rules on AI–human interaction begin to apply. The accountability question — *when an agent acts, who approved it, and can you prove it?* — arrives with them. "Sign Your Agents" is a concrete, shippable answer you can adopt today, not a compliance scramble in August.

## The four requirements (the floor)

1. **Disclose** — every message states it is from an AI agent. No fake personas.
2. **Sign** — every message is cryptographically signed (e.g. Ed25519), so a recipient can verify it is genuinely yours and untampered.
3. **Mandate** — publish, at a stable URL, what the agent may do and may not do.
4. **Accountable** — name a real legal entity accountable for the agent's actions **within that defined mandate**, with a working opt-out / report path.

The full spec, JSON schema, and verification method: [`SIGNED_AGENT_OUTREACH.md`](./SIGNED_AGENT_OUTREACH.md).

## How to adopt (and sign on, publicly)

- **Implement** the four requirements for your outbound agents (the spec shows how; we run a live reference at https://legatus.rupestelis.com/agent).
- **Sign on publicly:** open a pull request adding your organization to [`ADOPTERS.md`](./ADOPTERS.md). That PR is itself a public, verifiable endorsement — no mailing list, no spam, just a signature in the open.
- **Or push back:** open an issue. If you think this is wrong, say so in public. Opening the debate is the point.

## A note on how we are launching this

We could have emailed this to every company and journalist in Europe at once. We deliberately did not — because a standard against AI spam, launched by spamming everyone, refutes itself. We made a governed decision (recorded and signed in our own decision system) to launch this **in the open and by invitation, not by blast.** The method has to embody the standard, or there is no standard.

> **If we wouldn't accept it in our own inbox, we won't send it to yours.**

— Margelis.ai · the trust & governance layer for AI agents · operated by Rūpestėlis Holding UAB, Vilnius
