# Tertalis Materialization Test

**Status: experimental application and development harness, not a stable release.**

Materialization Test is an AppPack used to exercise Tertalis's model-assisted
workflow, persistence and evidence handling. It is not an end-user AI assistant.
This repository currently contains the application's source and a complete
working snapshot of the Tertalis platform revision it adopted. That platform
snapshot is part of the checkout, but remains Tertalis-owned source.

## Is this useful to try?

Developers testing Tertalis workflows, saved application state and the
materialization process can inspect and run the existing application.
Real model execution requires compatible external llama.cpp binaries, an
available model, and appropriate configuration. This is an experimental
test application with no one-click model installation or configured
out-of-the-box model.

The current entry point is a **Python script**, not an application
`setup.bat` or `run.bat`. Those application-specific Windows scripts
do not yet exist in this repository. Do not confuse the platform root
setup script with an application-specific installer.

## Get the repository running (Windows)

Clone and set up Tertalis internals:

```powershell
git clone https://github.com/Tertalis/Tertalis-Materialization-Test.git
cd Tertalis-Materialization-Test
.\setup.bat
```

Root `setup.bat` runs the Tertalis `setup.ps1` and prepares the
repository-local `python-embedded/` runtime and shared tooling. It
does not discover or set up applications. For the explicit 3.14 fallback,
see [SETUP.md](SETUP.md).

Before using the model-dependent workflow, review
`first-party/applications/materializationTest/config.json`. The runner
can load an optional sibling `config.local.json` for local overrides.
The base configuration has an empty model registry; you must provide
the necessary model definition and executable configuration before
real model execution. Do not commit local paths, model files or
private results.

### Inspecting the configured workflow

The `--describe` mode does not invoke model inference, although
application initialization and configuration still need to succeed:

```powershell
.\python-embedded\python.exe -X frozen_modules=off first-party/applications/materializationTest/run.py --new-application --describe
```

This mode may create and save application state under the default
`saves/` directory. Use a dedicated test checkout or explicitly
select `--saves-root` if you need to isolate generated state.

The run entry point also accepts `--application-id` for loading an
existing saved application. Running without `--describe` invokes
the model-driven workflow and then evidence export, so prepare
external configuration first.

## Development

The application lives under
`first-party/applications/materializationTest/`. Its focused tests
are in `tests/first_party/materializationTest/`; the full
platform and other shared tests live under `tests/`.

After root setup, from the repository root:

```powershell
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests/first_party/materializationTest
.\python-embedded\python.exe -X frozen_modules=off -m pytest tests
```

These are suggested commands, **not** a claim that the migrated
repository's tests have been executed during documentation work.
Some runtime tests may depend on their documented environment
or external tools. Further developer setup details are in
[SETUP.md](SETUP.md).

Read [AGENTS.md](AGENTS.md) before AI-assisted repository work.

## Shared AI coordination

This repository participates in the **same cooperative Tertalis
development workflow** as the platform and other applications.
It has no independent authoritative coordination inbox.
During the file-based transition, the canonical coordination
ref remains `integration` in
[EnterTheNameHere/Turnix](https://github.com/Tertalis/Tertalis/tree/integration).
The copied `ai-workflow/` here is a snapshot, not a new
active inbox; consult the canonical protocol and workstream
state before taking ownership of any work.

Integration of newer Tertalis revisions is explicit and
must succeed before this application's accepted platform
dependency is updated. An unsuccessful integration leaves
the previously functioning revision in place.

## Future direction

Tertalis intends a first-class PackageManager and CLI.
They are not present-day setup or launch commands for this
application.
