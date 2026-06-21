# STACK

Default: docs-first HomeLab workspace.

## Current Runtime

- No project runtime is established yet.
- Do not assume Node/npm, Python, Docker, or Hermes state without verifying the real VPS.

## Known VPS Tooling To Verify

Inbox sources mention:
- `git`
- `curl`
- `rsync`
- `jq`
- `rg`
- `tmux`
- `htop`
- `tree`
- `unzip`
- `gcc`
- `make`
- `pipx`
- `docker`
- `docker compose`

## Project Layout

- `00_inbox/`: raw source material, not rewritten during normal work
- `01_harness/`: always-on rules, stack, and taskflow
- `02_context/`: distilled HomeLab context
- `03_specs/now/`: one active spec at a time
- `03_specs/backlog.md`: one-line future work
- `03_specs/decisions.md`: decision log
- `04_outputs/`: final deliverables
- `05_scratch/`: working reports and temporary notes
