# keystone-trade-slippage-mesh

`keystone-trade-slippage-mesh` explores trading systems with a small Zig codebase and local fixtures. The technical goal is to design a Zig verification harness for slippage systems, covering protocol validation, framed sample traffic, and failure-oriented tests.

## Use Case

The project exists to keep a narrow engineering decision visible and testable. For this repo, that decision is how spread pressure and portfolio drift should influence a review result.

## Keystone Trade Slippage Mesh Review Notes

For a quick review, compare `spread pressure` with `portfolio drift` before reading the middle cases.

## Highlights

- `fixtures/domain_review.csv` adds cases for spread pressure and fill risk.
- `metadata/domain-review.json` records the same cases in structured form.
- `config/review-profile.json` captures the read order and the two review questions.
- `examples/keystone-trade-slippage-walkthrough.md` walks through the case spread.
- The Zig code includes a review path for `spread pressure` and `portfolio drift`.
- `docs/field-notes.md` explains the strongest and weakest cases.

## Code Layout

The core code exposes a scoring path and the added review layer uses `signal`, `slack`, `drag`, and `confidence`. The domain terms are `spread pressure`, `fill risk`, `portfolio drift`, and `quote width`.

The added Zig path is deliberately direct, with fixtures doing most of the explaining.

## Run The Check

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/verify.ps1
```

## Regression Path

That command is also the regression path. It verifies the domain cases and catches mismatches between the CSV, metadata, and code.

## Future Work

No external service is required. A deeper version would add more negative cases and a clearer boundary around invalid input.
