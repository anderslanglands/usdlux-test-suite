# USD Lux Test Suite

Goldeneye test suites for USD Lux and physically based light behavior. The checked-in fixtures and EXR references were copied from `typhoon-tests`.

## Prerequisites

- [Pixi](https://pixi.sh/latest/installation/) must be installed before using the repository's build, test, and viewing commands. Pixi manages the dependencies, build and execution environment.
- [GitHub CLI](https://cli.github.com/), logged in and authenticated for publishing updated reference archives to the repository.

## Quick Start

```bash
git submodule update --init --recursive
pixi run goldeneye download-references # download reference images
pixi run goldeneye build               # build web server
pixi run pytest                        # run test suites
pixi run goldeneye view                # run web server to view results
```

## Running Tests

Running tests using standard [`pytest`](https://docs.pytest.org/en/stable/).

To run all tests:
```bash
pixi run pytest
```

To run a particular section, or particular test fixture:
```bash
pixi run pytest section/subsection
pixi run pytest section/subsection/case.usda
```

To filter test runs by name use the `-k` flag:
```bash
# run all tests with "light" in the name
pixi run pytest -k light 
# run all tests with "light" or "material" in the name
pixi run pytest -k 'light or material' 
```

## Reference Images

### Getting reference images

Populate all reference directories after cloning or pulling a manifest update:

```bash
pixi run goldeneye download-references
```

Reference images are stored as immutable ZIP archives in GitHub Releases, with one archive per suite subsection. The committed `reference-releases.json` manifest records every archive, file, size, and SHA-256 checksum. Hydrated `reference/` directories are intentionally ignored by Git.

The command downloads only archives whose files are absent or outdated, verifies the archive and every extracted image, and records local hydration state. It refuses to overwrite locally edited references; use `--force` only when those edits should be discarded.

### Updating reference images

After adding or removing tests, adding or removing reference files, or using the report's **Update reference** action, publish the changed subsections:

```bash
pixi run goldeneye update-references
```

This command requires references hydrated from the current manifest. It creates an immutable GitHub release containing only changed subsection archives, updates `reference-releases.json`, and creates a Git commit containing the manifest and associated suite changes. Unrelated files outside suite directories are not included. Use `--dry-run --no-commit` to inspect the detected changes without publishing.
