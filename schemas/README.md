# Canonical identity, registry, policy, and audit schema

`identity-registry-policy-audit.schema.json` is the versioned contract for a
single authorization-domain export. It is a JSON Schema Draft 2020-12 document.

## Document shape

Every document declares `schemaVersion: "1.0"` and contains four arrays:

- `identities` defines users, services, and groups. Identity IDs are the stable
  references used everywhere else in the document.
- `registry` defines resources and their owning identity.
- `policies` holds ordered rule sets. Each rule has an explicit `allow` or
  `deny` effect, subjects, resources, and actions.
- `auditEvents` records an actor, action, target, timestamp, and outcome. An
  event can optionally identify the policy that determined its outcome.

The schema validates shape and local values only. Consumers must resolve
identity, registry, and policy references against their corresponding arrays;
this keeps the document suitable for partial or incrementally produced exports.

## Compatibility

Additive, backwards-compatible changes should retain the `1.x` document shape.
Breaking changes require a new `schemaVersion` value and schema document. Keep
extensions in the explicitly provided `attributes`, `conditions`, and
`metadata` objects rather than adding undeclared fields to canonical records.
