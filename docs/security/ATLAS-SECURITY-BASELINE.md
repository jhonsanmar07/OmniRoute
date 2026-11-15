# ATLAS ecosystem security integration note — OmniRoute

Status: QA integration note. OmniRoute's existing SECURITY.md and upstream security controls remain authoritative for its own implementation. This note does not replace them or certify them.

For ATLAS integration, treat OmniRoute as an untrusted external model-routing provider behind the ecosystem's five-layer model and fourteen controls: STRIX, RATE_LIMIT, SECRET_VAULT, DATABASE_GUARD, AUDIT_TRAIL, SECURITY_AUDITOR, ZERO_TRUST, WAF_API_SHIELD, IDENTITY_GUARD, SUPPLY_CHAIN_DEFENSE, THREAT_RESPONSE, DISASTER_RECOVERY, AI_GUARD and RUNTIME_SANDBOX.

## Integration boundary
1. Keep OmniRoute disabled for production ATLAS routing until its exact deployed version, security baseline, license, authentication and cost posture are verified.
2. Use a dedicated, least-privilege credential; never reuse user or production admin credentials.
3. Route only through an authenticated, HTTPS endpoint with explicit host allowlisting and bounded timeouts.
4. Send only the minimum prompt/context needed; redact secrets and personal data before provider dispatch.
5. Treat all model output as untrusted data. It cannot modify system policy, authorize tools or bypass Quality Gate.
6. Keep tool execution in ATLAS-controlled allowlisted workers; do not grant provider runtime access to production secrets, filesystem or arbitrary network.
7. Audit provider/version, policy decision, request correlation ID, cost and outcome without recording secret prompt content.
8. Revalidate license, upstream advisories, dependency state and zero-cost evidence on every version change.

## Activation gate
No provider activation until independent runtime tests, authentication/authorization tests, egress tests, license review, cost evidence and incident/revocation procedures are verified. Missing evidence means disabled. This note does not claim the upstream project has been audited by ATLAS.
