# keystone-trade-slippage-mesh

`keystone-trade-slippage-mesh` treats trading systems as a local verification problem. The Zig implementation is intentionally narrow, but the fixtures and notes make the behavior explicit.

## Keystone Trade Slippage Mesh Checkpoints

Treat the compact fixture as the contract and the extended examples as a scratchpad. The code should stay boring enough that a change in behavior is obvious from the test output.

## Useful Pieces

- Includes extended examples for fills, including `surge` and `degraded`.
- Documents portfolio pressure tradeoffs in `docs/operations.md`.
- Runs locally with a single verification command and no external credentials.
- Stores project constants and verification metadata in `metadata/project.json`.
- Adds a repository audit script that checks structure before running the language verifier.

## What This Is For

The goal is to capture the core behavior in code and make the surrounding assumptions obvious. A reader should be able to run the verifier, open the fixtures, and understand why each decision was made.

## Project Layout

- `src`: primary implementation
- `fixtures`: compact golden scenarios
- `examples`: expanded scenario set
- `metadata`: project constants and verification metadata
- `docs`: operations and extension notes
- `scripts`: local verification and audit commands

## Architecture Notes

The core is a scoring model over demand, capacity, latency, risk, and weight. That keeps order state, risk checks, and fills in one explicit decision path. The threshold is 180, with risk penalty 4, latency penalty 3, and weight bonus 4. The Zig version uses compile-time constants and native test blocks for fast local checks.

## Local Workflow

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/verify.ps1
```

This runs the language-level build or test path against the compact fixture set.

## Case Study

`examples/extended_cases.csv` adds six named cases. I kept the names plain so failures are easy to read in a terminal: baseline, pressure, surge, degraded, recovery, and boundary.

## Quality Gate

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/audit.ps1
```

The audit command checks repository structure and README constraints before it delegates to the verifier.

## Scope

The fixture set is deliberately small. That keeps the review surface clear, but it also means the model should not be treated as a complete domain simulator.

## Expansion Ideas

- Split the scoring constants into a typed configuration object and validate it before use.
- Add a comparison mode that shows how decisions change when one signal is adjusted.
- Add a loader for `examples/extended_cases.csv` and promote selected cases into the language test suite.
- Add one more trading systems fixture that focuses on a malformed or borderline input.

## Tooling

Use a normal shell with Zig available on `PATH`. The verifier is written as a PowerShell script because the portfolio was assembled on Windows.
