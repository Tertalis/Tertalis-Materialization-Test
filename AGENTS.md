# AI development entry point — Materialization Test

This repository contains the Materialization Test AppPack alongside
a pinned Tertalis platform snapshot. Use the same setup commands
as human contributors. This file is navigation only and does not
replace the canonical coordination protocol.

## Required orientation

1. Read [README.md](README.md) and [SETUP.md](SETUP.md) to establish
   what currently works and how to prepare the platform.
2. Read the application source and tests under
   `first-party/applications/materializationTest/` and
   `tests/first_party/materializationTest/`.
3. Read the canonical
   [ai-workflow index](https://github.com/Tertalis/Tertalis/blob/integration/ai-workflow/index.txt)
   and
   [coordination protocol](https://github.com/Tertalis/Tertalis/blob/integration/ai-workflow/coordination-protocol.txt)
   on the `actant-integration` ref.
4. Review the current Materialization Test STATE, handoff and inbox
   on that canonical ref. The copies inside this repository are
   historical snapshots and are NOT independent authoritative inboxes.
5. Verify ownership and authorization before changing the code,
   importing platform updates or changing any accepted revision.
   A new repository does not mean an additional Coordinator.

## Boundaries and verification

- Root `setup.bat` and `setup.ps1` prepare Tertalis internals only.
  Do not alter root setup to initialize this application.
- The application currently has `run.py`, not its own `setup.bat`
  or `run.bat`. Do not invent commands for nonexistent files.
- The default local Python is `python-embedded/python.exe`, with
  `-X frozen_modules=off` for the present embedded runtime.
- AppPack-owned files and tests are distinct from the shared
  Tertalis `backend/` and reusable first-party Packs.
- Do not publish a newer platform dependency until an authorized
  integration has succeeded and required checks have passed.
- Preserve Git history, accepted state and real evidence. Do not
  delete branches, run destructive tests or publish releases without
  the required authorization.

Basic development checks after root setup:

```powershell
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests/first_party/materializationTest
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests
```

Never claim a check passed unless it was actually executed.
Follow the canonical coordination finish barrier and report
exact refs, results and unresolved work.

## Shared ai-workflow boundary

Every assistant, implementer, integrator, coordinator and design thread must
read the current canonical ai-workflow instructions at
[Tertalis/Tertalis integration](https://github.com/Tertalis/Tertalis/blob/integration/ai-workflow/index.txt)
before working. This repository's `ai-workflow/index.txt` is only a local
routing stub; its `integration` branch is the application's development
branch, not a coordination authority. All operational inboxes, messages,
workstream state and repository-location registry are maintained only in
`Tertalis/Tertalis` on `integration`. Do not create a local inbox or rely
on copied historical mail. For other applications, consult Tertalis's
canonical registry rather than recording their addresses here.
