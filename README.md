# Signed Agent Outreach (SAO)

A proposed, vendor-neutral standard for outbound AI agents: **openly identified, cryptographically signed, and accountable to a named legal entity within a defined mandate.**

> Most AI outreach hides that it's AI. This standard does the opposite.

**Status:** Draft v0.1 · **Editors:** Margelis.ai (operated by Rūpestėlis Holding UAB, Vilnius, Lithuania) · **License:** CC-BY-4.0

## Why

As autonomous agents begin contacting people at scale, one question gets expensive fast: *when an agent acts, who approved it — and can you prove it?* The EU AI Act's transparency rules on AI–human interaction begin to apply on **2 August 2026**. SAO is a practical, implementable answer.

## The rule (one line)

> If an AI agent reaches out on your behalf — **disclose it, sign it, and define the mandate it is accountable within.**

## Documents

- [`SIGNED_AGENT_OUTREACH.md`](./SIGNED_AGENT_OUTREACH.md) — the normative standard
- [`agent-manifest.schema.json`](./agent-manifest.schema.json) — machine-readable manifest schema (JSON Schema 2020-12)
- [`verification.md`](./verification.md) — how to verify a signed agent
- [`legal-entity-accountability.md`](./legal-entity-accountability.md) — the mandate / accountability model
- [`examples/manifest.example.json`](./examples/manifest.example.json) — a real manifest

## Reference implementation

A live signed outreach agent with a public mandate page:

- Agent mandate page — https://legatus.rupestelis.com/agent
- Standard / announcement — https://margelis.ai/signed-agents

Signing uses **Sigillum** (Ed25519).

## Conformance, in one paragraph

An outbound agent conforms to SAO if every message (1) discloses it is an AI agent, (2) is cryptographically signed with a published key, (3) links to a public mandate page over HTTPS on the operator's domain, and (4) names a real legal entity accountable for the agent's actions within a defined mandate — with a working opt-out / escalation path.

## Status & contributions

This is a **proposal under active implementation**, not a finished standard. We invite review, issues, and PRs. We are **not claiming to be first** — we are claiming to be accountable, and proposing this as common practice.
