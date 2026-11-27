# Loops

The architecture closes three loops. They are intentionally separate so that data, authority and presentation can be audited independently.

## 1. Data loop

```
physical/edge capture
  -> typed event
  -> edge filter (VAD, keyframes, OCR, transcript, redaction)
  -> home core
  -> memory / artifact store
  -> approved presentation
```

Rules:

- Send events, transcripts and keyframes before raw media.
- Keep raw media local or encrypted; upload on demand.
- Every artifact carries provenance, consent scope and a content hash.
- Canonical artifacts live in the memory layer; edge caches are transient.

## 2. Logic loop

```
identity -> session lease -> task capsule -> policy
  -> routing -> execution -> validation -> delivery -> audit -> revoke
```

- A task capsule contains intent, scope, deadline, data references, permissions and expected output.
- The core selects capabilities from a registry; it does not improvise raw shell access.
- Validation includes schema checks, source citations, confidence and policy checks.
- Irreversible actions require human approval and a rollback plan.
- The session lease and task capsule expire; access is revoked explicitly.

## 3. Mapping loop

- Any terminal can be a window.
- A user can move between terminals; the session capsule follows.
- Role lenses present different views of the same system to different people.
- Guest access is scoped, time-limited and revocable.
- The canonical state remains in the core and memory, not in the terminal.

## 4. Fallback loop

If the core is unreachable:

- the edge may run a leased shadow agent;
- only L0/L1 tools are allowed;
- tasks are queued, not silently executed;
- L2 actions wait for a human;
- on reconnect, the edge reconciles with the core and discards stale leases.

## 5. Service objectives

Define and measure:

- capture-to-event latency;
- task turnaround time;
- validation pass rate;
- human intervention rate;
- artifact completeness;
- restore/replay success.

Do not promise "real time" without a measured objective.
