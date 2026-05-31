# Verification

How a recipient (or a third party) verifies a Signed Agent Outreach message.

## Trust model

1. The **operator** publishes a signing **public key** (Ed25519) on a domain it controls (HTTPS).
2. Each message — or a per-message record — is **signed** with the corresponding private key over a **canonical payload**.
3. The public **Mandate Page** (HTTPS, operator's domain) ties that key and agent to a named **legal entity** and a **mandate**.

So a valid signature proves *the message came from the holder of that key*; the Mandate Page proves *whose key it is and what it is allowed to do*. The two together give origin + accountability.

## What a verifier checks

1. **Disclosure** — the message states it is an AI agent.
2. **Signature validity** — the Ed25519 signature verifies against the published key over the canonical payload.
3. **Key binding** — the `key_fingerprint` matches the operator's published key (`verification.public_key_url`).
4. **Mandate** — the action falls within `allowed_actions` and not in `forbidden_actions`.
5. **Status** — the manifest is not `revoked` and not past `expires_at`.

If any check fails, the message MUST NOT be treated as a verified agent message.

## Steps

```text
1. Extract the reference from the signature block link:
   https://<operator>/agent?ref=<message_id>
2. Fetch the agent manifest (e.g. /.well-known/agent-manifest.json) and the
   per-message record at the verify_url.
3. Recompute the canonical payload hash for the message.
4. Verify the Ed25519 signature (signature.value) against the operator's
   published public key over that payload.
5. Confirm key_fingerprint == published key fingerprint.
6. Confirm the action is within the mandate and the manifest is not revoked/expired.
```

## Example (Ed25519, conceptual)

```python
import base64
from nacl.signing import VerifyKey   # pip install pynacl

# 1. Operator's published signing public key (from verification.public_key_url)
public_key = VerifyKey(base64.b64decode(PUBLISHED_PUBLIC_KEY_B64))

# 2. Canonical payload for this message + the signature from the record
payload = canonical_bytes(message_record)         # operator-documented canonicalization
signature = base64.b64decode(record["signature"]["value"])

# 3. Verify — raises nacl.exceptions.BadSignatureError if invalid
public_key.verify(payload, signature)
print("signature OK — message originates from", manifest["legal_entity"]["name"])
```

## Reference implementation

The live agent exposes a per-message reference at
`https://legatus.rupestelis.com/agent?ref=<message_id>` and signs via **Sigillum**
(Ed25519, append-only stamp chain). A public per-message verification endpoint and a
`/.well-known/` public key are on the v0.1 → v0.2 path.

## Notes

- Canonicalization MUST be deterministic and documented by the operator (e.g. sorted-key JSON, UTF-8). A verifier and a signer that disagree on canonicalization will disagree on the signature.
- Key rotation: operators SHOULD publish current and recently-retired key fingerprints so older signed messages remain verifiable.
