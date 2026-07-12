# USD Lux Test Suite

Goldeneye test suites for USD Lux and physically based light behavior. The checked-in fixtures and EXR references were copied from `typhoon-tests`.

## Development

```bash
pixi run pytest --collect-only -q
pixi run pytest usdlux --goldeneye-dry-run -s
pixi run pytest physlight --goldeneye-dry-run -s
pixi run pytest
```

Goldeneye is used from the editable sibling checkout at `../goldeneye`.

```bash
pixi run goldeneye download-references
pixi run goldeneye update-references --dry-run
pixi run goldeneye extract-failures
pixi run goldeneye view
```
