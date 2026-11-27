# Reference Architecture

## 1. Overview

The system is a local-first, human-in-the-loop organism:

- a **home core** owns orchestration, policy, routing and audit;
- one or more **terminals** provide intent, display and approval;
- an optional **mobile edge** carries a session and runs platform-specific tools;
- a **physical body** provides sensors, camera, microphone, speaker and UI actions;
- a **memory layer** stores canonical artifacts and evidence;
- a **heavy compute** node handles expensive local work;
- an **external brain** is used only for approved, desensitized work;
- a **human** remains the final approver.

The architecture is hub-and-spoke. Nodes do not bypass the core's policy.

## 2. Planes

### Data plane

```
capture -> edge filter -> core -> memory -> artifact
```

- Capture devices emit typed events with source, time, consent scope, schema version and hash.
- Edge filtering performs VAD, keyframes, OCR, transcription and redaction where possible.
- The core normalizes, routes and records provenance.
- Canonical artifacts live in the memory layer; edge caches are transient.

### Control plane

- Identity and session leases.
- Task capsules with scope, deadline and data references.
- Capability registry with schemas, constraints and status.
- Policy engine with L0-L3 permissions and human approvals.
- Audit log and kill switch.

## 3. Deployment variants

### A. Home core + terminals

The core is always-on and local. Terminals connect over a private overlay or a local network. Best for privacy and simplicity.

### B. Home core + mobile edge

A portable cloud desktop acts as a session carrier, platform-specific tool host and rendezvous. It is a thin edge, not the brain. Single-session handoff is required.

### C. Dedicated edge capture

A school- or site-approved edge device captures and preprocesses locally, then sends only approved events or summaries. Best where the main computer is locked or shared.

## 4. Single-session handoff

When the mobile edge allows only one interactive session:

1. Terminal A works; the background agent runs as a service or out-of-band worker.
2. Terminal A disconnects; the session is suspended, not destroyed.
3. The core keeps processing; artifacts are stored in memory.
4. Terminal B connects; it receives the latest capsule and resumes.
5. No dual interactive login is required or allowed.

## 5. Failure behavior

- Network loss: queue at the edge, retry with backoff, reconcile on reconnect.
- Core offline: the edge may run a leased shadow agent with L0/L1 tools only; L2 waits for human approval.
- Validation failure: return a draft with explicit gaps; do not fabricate.
- Policy denial: stop and ask the human; do not route around the policy.

## 6. Non-goals

This is not a product, a hosted service or a security certification. Implementations must add their own threat model, compliance review and operational controls.
