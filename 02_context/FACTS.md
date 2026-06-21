# FACTS

## Project Identity
- Fact: The inbox defines `skilland-agentic-homelab` as the HomeLab repo and laboratory for Skilland/Reboot.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`; `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: The current working path is `/home/skilland/workspaces/skilland-agentic-homelab`.
  Source: environment context for this session
  Confidence: high
- Fact: Root instructions identify this repo as Skilland Agentic HomeLab.
  Source: `README.md`; `AGENTS.md`; `CLAUDE.md`
  Confidence: high

## Strategic Context
- Fact: `skilland-agentic-north-star` is described as the strategic compass for the larger Skilland Agentic OS vision.
  Source: `00_inbox/01_northstar_handoff_to_homelab.md`; `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: Skilland Agentic OS is framed as a small company operable through resident AI agents working over repos, CRM, Drive, Gmail, GitHub, data, campaigns, and real deliverables.
  Source: `00_inbox/01_northstar_handoff_to_homelab.md`; `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: HomeLab is intended to convert that vision into explorable capabilities in the real VPS.
  Source: `00_inbox/01_northstar_handoff_to_homelab.md`; `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: HomeLab is explicitly not intended to start as a closed architecture, client product, or final productized system.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`; `00_inbox/01_homelab_operational_brief.md`
  Confidence: high

## Operators and Roles
- Fact: Raúl is identified as CEO, functional CTO, product owner, strategic operator, lab director, and final approver when needed.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: Codex is described as the first resident technical operator for HomeLab.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`; `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: Hermes is identified as the strong central target that HomeLab must understand and put at the heart of the lab.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: The initial working hypothesis is that Hermes coordinates, interprets, routes, and maintains agentic context, while Codex executes technical microhitos inside the VPS/repo.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: medium

## VPS and Tooling
- Fact: The daily SSH entry is documented as `ssh skilland-vps`.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: medium
- Fact: The daily user is documented as `skilland`.
  Source: `00_inbox/01_homelab_operational_brief.md`; environment context path
  Confidence: high
- Fact: Daily repo work should happen under `/home/skilland/workspaces/<repo>`.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: The documented operational paths include `/srv/skilland/apps`, `/srv/skilland/services`, `/srv/skilland/data`, `/srv/skilland/logs`, `/srv/skilland/backups`, `/srv/skilland/ops`, `/opt/skilland/tools`, and `/etc/skilland`.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: medium
- Fact: Known base tooling is documented as git, curl, rsync, jq, rg, tmux, htop, tree, unzip, gcc, make, pipx, Docker, and Docker Compose.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: medium
- Fact: Node/npm/runtimes must be verified at HomeLab startup and must not be assumed as final global stack.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: high

## Work Sequence
- Fact: The first strong microhito is Hermes Deep Research / Hermes Literacy.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: The second microhito is Hermes Intimacy: install, configure, break, observe, and document Hermes.
  Source: `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: External channels such as WhatsApp/Kapso and email/Gmail are later-stage work, after CLI/Codex/Hermes basics.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`; `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: Candidate early real repos include `RaulAM7/google-workspace-CLI-Experiment` and `RaulAM7/funnel-and-offer-academy`.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`; `00_inbox/01_homelab_operational_brief.md`
  Confidence: high
- Fact: `Skilland-ai/skilland-crm` is important but may be too risky or complex as the first real repo.
  Source: `00_inbox/01_homelab_foundation_manifesto_v2.md`
  Confidence: high
- Fact: The active spec folder is intentionally clear of prior package work before creating the Hermes Deep Research spec.
  Source: `03_specs/now/`
  Confidence: high

## Unknowns and Assumptions
- Unknown: Authoritative Hermes source list, official docs, community patterns, and reference repos.
- Unknown: Whether Hermes is already installed anywhere on the VPS.
- Unknown: Actual available RAM/CPU/disk and whether the current VPS has bottlenecks.
- Unknown: Current repo remote and whether a Git repository should be initialized or connected.
- Unknown: Exact first repo to operate after Hermes research.
- Unknown: Exact approval checklist for high-risk infrastructure operations.
