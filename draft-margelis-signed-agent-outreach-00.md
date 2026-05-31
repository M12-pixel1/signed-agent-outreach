---
title: "Signed Agent Outreach: Disclosure, Signing, Mandate, and Accountability for Outbound AI Agents"
abbrev: "Signed Agent Outreach"
docname: draft-margelis-signed-agent-outreach-00
category: info
ipr: trust200902
area: Security
workgroup: Independent Submission
keyword: [AI agents, agent identity, accountability, Ed25519, transparency, EU AI Act]
stand_alone: yes
pi: [toc, sortrefs, symrefs]
author:
 -
    ins: T. Margelis
    name: Tomas Margelis
    organization: Margelis.ai / Rūpestėlis Holding UAB
    email: tomas@rupestelis.com
    country: Lithuania
normative:
  RFC2119:
  RFC8174:
  RFC8032:   # EdDSA / Ed25519
  RFC8615:   # Well-Known URIs
informative:
  RFC8259:   # JSON
  EU-AI-ACT:
    title: "Regulation (EU) 2024/1689 (Artificial Intelligence Act)"
    target: "https://eur-lex.europa.eu/eli/reg/2024/1689/oj"
--- abstract

This document specifies Signed Agent Outreach (SAO), a method by which an
autonomous software agent that initiates contact with a person on behalf of an
organization (a) discloses that it is an AI agent, (b) cryptographically signs
each message or a verifiable per-message record, (c) publishes a machine- and
human-readable mandate describing what the agent may and may not do, and (d)
names a legal entity accountable for the agent's actions within that mandate.
SAO is designed to make agent-initiated communication verifiable, bounded, and
accountable, and to support transparency obligations for AI systems that
interact with people.

--- middle

# Introduction

Autonomous agents increasingly initiate contact by email, messaging, and voice.
The prevailing practice conceals that the sender is an agent and imitates a
human. This erodes trust, enables impersonation and fraud, and is in tension
with emerging transparency obligations for AI systems that interact with people,
including those in {{EU-AI-ACT}}.

Signed Agent Outreach (SAO) defines the opposite default: an agent that
discloses, signs, and operates within a published, accountable mandate. SAO does
not standardize the agent's task or content; it standardizes how the agent
identifies itself, proves origin, bounds its behavior, and ties that behavior to
an accountable legal entity.

# Terminology

The key words "MUST", "MUST NOT", "SHOULD", "MAY" in this document are to be
interpreted as described in BCP 14 {{RFC2119}} {{RFC8174}} when, and only when,
they appear in all capitals.

Agent:
: an autonomous software process that initiates contact with a person.

Operator:
: the legal entity that deploys the Agent and is accountable for it.

Mandate:
: the published, human- and machine-readable definition of what the Agent may
  and may not do.

Manifest:
: the structured document describing the Agent, its Operator, its Mandate, and
  its signing key ({{manifest}}).

# Requirements

A conforming outbound Agent:

1. MUST clearly disclose, in every message, that it is an AI agent. It MUST NOT
   impersonate a human or imply that it is one.
2. MUST cryptographically sign each message, or produce a verifiable per-message
   record, using a published public key, so a recipient can confirm the message
   originated from the Operator.
3. MUST link to a public Mandate, served over HTTPS on a domain the Operator
   controls.
4. MUST name a real legal entity, with jurisdiction and a contact/escalation
   address, accountable for the Agent's actions within the Mandate.
5. MUST operate within its published Mandate; actions outside the Mandate are
   not authorized.
6. SHOULD require recorded human approval before sending outreach to individuals.
7. SHOULD enforce and publish rate limits.
8. MUST provide a low-friction opt-out / report path, and SHOULD honor opt-outs
   within 24 hours.

# The Agent Manifest {#manifest}

The Operator publishes a Manifest, a JSON {{RFC8259}} object. The Manifest
SHOULD be available at the well-known URI "/.well-known/agent-manifest.json"
(see {{iana}}). Required members: agent_id, agent_name, legal_entity,
public_mandate_url, allowed_actions, forbidden_actions, signature, verification,
issued_at. The full schema is published with this specification.

# Signature and Verification

Signatures MUST use a published public key. Ed25519 {{RFC8032}} is RECOMMENDED.
The signed payload MUST be canonicalized deterministically; the Operator MUST
document its canonicalization. A verifier (a) obtains the Operator's published
public key, (b) recomputes the canonical payload, (c) verifies the signature,
(d) confirms the key fingerprint matches the published key, and (e) confirms the
action is within the Mandate and the Manifest is not revoked or expired.

# Mandate and Accountability

The Mandate is the boundary of accountability. The Operator is accountable for
the Agent's actions within the Mandate, as a principal is responsible for an
authorized representative acting within delegated, published authority. Actions
outside the Mandate are unauthorized and outside the scope of that accountability.
SAO does not confer legal personhood on the Agent.

# Security Considerations

SAO's primary security goal is origin authenticity and non-impersonation.
Threats include: signing-key compromise (mitigated by key rotation and published
fingerprints), replay (mitigated by per-message records and timestamps), and
spoofing of the disclosure/signature block (mitigated by out-of-band
verification against the published key on the Operator's domain). SAO does not
by itself establish a lawful basis for the underlying contact.

# Privacy Considerations

SAO increases transparency to recipients (disclosure, opt-out). Operators MUST
NOT include unnecessary personal data in the Manifest. The Mandate and Manifest
describe the Agent, not recipients.

# IANA Considerations {#iana}

This document requests registration of the well-known URI suffix
"agent-manifest.json" in the "Well-Known URIs" registry per {{RFC8615}}.

--- back

# Example Manifest

~~~
{
  "agent_id": "urn:sao:example:agent-1",
  "agent_name": "ExampleAgent",
  "legal_entity": { "name": "Example Ltd", "jurisdiction": "EU",
                    "contact_email": "contact@example.com" },
  "public_mandate_url": "https://example.com/agent",
  "allowed_actions": ["Send disclosed, signed B2B outreach within rate limits"],
  "forbidden_actions": ["Impersonate a human", "Contact opted-out recipients"],
  "signature": { "algorithm": "Ed25519", "method": "ed25519" },
  "verification": { "method": "ed25519", "verify_url": "https://example.com/agent" },
  "issued_at": "2026-01-01T00:00:00Z"
}
~~~

# Implementation Status

A live reference implementation (disclosure block, Ed25519/Sigillum signing,
public mandate page, opt-out path) operates at
https://legatus.rupestelis.com/agent . The open specification, JSON schema, and
verification method are published at
https://github.com/M12-pixel1/signed-agent-outreach .
