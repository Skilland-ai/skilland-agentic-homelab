# CONSTRAINTS

## Budget
- Not stated.
- Hardware is not a strategic constraint. If the current VPS creates a real bottleneck, the stated direction is to measure, test, and scale to another VPS/server when justified.

## Time
- No hard deadline stated.
- Source documents are dated 2026-06-21.
- Work should progress through short microhitos rather than a large architecture phase.

## Tooling Limits
- Do not assume Node/npm or any runtime as globally final. Verify the real environment before using it as a foundation.
- Do not work outside a concrete repo for normal development.
- Do not use root for daily work. Root/admin access is for punctual administration.
- Do not connect Gmail, Drive, CRM, WhatsApp, Telegram, or other external channels before Hermes/Codex basics are understood.
- Do not install accessory services without a capacity-driven reason.
- The current harness expects compact context files under `02_context/`, one active spec in `03_specs/now/`, outputs under `04_outputs/`, and scratch under `05_scratch/`.

## Human Approval Constraints
- Raúl keeps product direction, priority, risk tolerance, and approval authority.
- Actions with external or sensitive effects require explicit command or approval from Raúl in the relevant microhito.
- Approval-sensitive actions include external emails, WhatsApps, client contact, publishing, irreversible deletion, moving secrets, critical infrastructure changes, and touching real production CRM/commercial systems.

## Non-Negotiables
- HomeLab starts as an internal YOLO laboratory, but not as unmanaged chaos.
- Hermes is the first strong focus and must be understood before building heavily on top.
- Codex acts as resident technical operator, not a passive assistant.
- Do not close technical architecture prematurely.
- Do not solve meta-harness at the start.
- Do not productize for Divi-DClick before HomeLab has robust, sober learnings.
- Do not copy inbox dumps verbatim into context files.
- Document learning, failures, provisional decisions, and next steps.

## Tone and Culture
- Ambitious, playful, technical, fast, free, documented, and useful.
- Prefer learning fast, breaking cheaply, and documenting well over overcontrolled agent cages.
- Avoid dead documentation, tool enthusiasm without use case, and PowerPoint architecture.

## Brand/Product Boundaries
- HomeLab belongs to the broader Skilland Agentic OS vision.
- Divi-DClick is a downstream beneficiary, not the governing scope.
- Client-facing systems require a more controlled posture than the internal HomeLab.
