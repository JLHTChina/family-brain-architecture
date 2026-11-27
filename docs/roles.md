# Roles and SOPs

## 1. Why roles

A single model asked to "be ten experts" produces inconsistent output. A role is a bounded worker with:

- a scope and a non-goal;
- input and output schemas;
- allowed tools;
- a step-by-step SOP;
- validation gates;
- failure behavior;
- a handoff target.

## 2. SOP template

```yaml
role: <name>
scope: <what this role owns>
inputs:
  - <schema or source>
outputs:
  - <schema or artifact>
tools:
  - <registered capability>
steps:
  - <deterministic step>
validation:
  - <schema check>
  - <source/citation check>
  - <policy check>
failure:
  - <retry / degrade / escalate>
handoff:
  - <next role or human>
```

## 3. Cross-cutting roles

These roles are mandatory before domain roles:

- **Intake**: normalizes capture, consent, provenance and schema.
- **Fact-check**: verifies claims and citations independently.
- **Privacy and rights**: checks consent, personal data, copyright and retention.
- **Editor**: integrates sections, resolves conflicts, enforces style.
- **Producer**: manages deadlines, budgets, resource contention and handoff.
- **Archivist**: stores canonical artifacts and audit metadata.

## 4. Domain roles

Examples: education, art, music, criticism, journalism, documentary. Each domain role should add its own terminology, evaluation rubric, tools and references. Domain roles do not bypass fact-check, privacy or editor gates.

## 5. Orchestration

Independent roles may run in parallel. Dependent roles run as a directed acyclic graph. The core enforces concurrency and budget limits; it does not run every role at maximum concurrency.

## 6. Quality gates

A role output is not "done" until:

- the schema validates;
- sources and confidence are present;
- privacy and rights checks pass;
- the editor accepts the handoff;
- the human approves any L2 action.
