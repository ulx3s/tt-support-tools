[![GDS Hardening Tests](../../actions/workflows/test-harden.yaml/badge.svg)](../../actions/workflows/test-harden.yaml)
[![Precheck Tests (gf180mcu)](../../actions/workflows/test-precheck-gf180mcu.yaml/badge.svg)](../../actions/workflows/test-precheck-gf180mcu.yaml)
[![Precheck Tests (sky130)](../../actions/workflows/test-precheck-sky130.yaml/badge.svg)](../../actions/workflows/test-precheck-sky130.yaml)
[![Mypy Type Checking](../../actions/workflows/mypy-check.yaml/badge.svg)](../../actions/workflows/mypy-check.yaml)
[![Python Lint](../../actions/workflows/lint-check.yaml/badge.svg)](../../actions/workflows/lint-check.yaml)
[![Run Pytest Tests](../../actions/workflows/test.yaml/badge.svg)](../../actions/workflows/test.yaml)

# Tiny Tapeout tools

Tools used mostly by the Tiny Tapeout GitHub Actions

## Setup

```
pip install -r requirements.txt
pre-commit install
```

On macOS, some third-party libraries are required:

```
brew install libpng qhull cairo
```

## Documentation

* checks that basic fields are present in the info.yaml
* create a PDF data sheet for this one design
* create SVG and PNG renders of the project's GDS

## Reports

* routing & utilisation
* yosys warnings
* standard cell usage and summary

## Configuration

* creates a little TCL shim that tells LibreLane where the source is and the name of the top module
* makes sure the top module is not called 'top'
* if you have LibreLane installed locally, then you can harden the design with --harden
