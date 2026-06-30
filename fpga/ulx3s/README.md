# ULX3S Files for Tiny Tapeout GitHub actions.

Various unedited versions of the ECP5 Constraint Files from [emard/ulx3s/doc/constraints](https://github.com/emard/ulx3s/tree/master/doc/constraints).

- `tt_fpga_top_ulx3s.v` reference example of the ULX3S FPGA "top" module as a wrapper for the respective TT project top module.
- `ulx3s_v316.lpf` - for v3.16, v3.17, v3,18: the most recent PCF file for most ULX3S purchased recently.
- `ulx3s_v314.lpf` - for v3.14
- `ulx3s_v20.lpf` - for versions 2.x .. 3.07
- `ulx3s_v17patch.lpf` - for version 1.7

Specify in the Tiny Tapeout step using the `with` keyword and `lpf` parameter. Values such as `tt/fpga/ulx3s/ulx3s_v20.lpf`, where `tt` is typically the already-cloned directory name of the `tt-support-tools` repo in the action.

```yaml
name: fpga

on:
  push:
  workflow_dispatch:
  
jobs:
  fpga-ulx3s:
    runs-on: ubuntu-24.04
    steps:
      - name: checkout repo
        uses: actions/checkout@v6
        with:
          submodules: recursive

      - name: FPGA bitstream for TT ASIC Sim (ULX3S ECP5)
        uses: gojimmypi/tt-gds-action/fpga/ulx3s@ulx3s
        with:
          ecp5-device: 85k
          lpf: tt/fpga/ulx3s/ulx3s_v20.lpf
```

For use in a Makefile:

```makefile
# See https://github.com/ulx3s/ulx3s/tree/master/doc/constraints
ifeq ($(ULX3S_BOARD_VERSION),v20)
    # This is also the default for v307
    LPF := ulx3s_v20.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v17)
    # Note the reference file name
    LPF := ulx3s_v17patch.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v17patch)
    LPF := ulx3s_v17patch.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v307)
    # v307 and v20 use the same constraint file
    LPF := ulx3s_v20.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v314)
    LPF := ulx3s_v314.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v316)
    LPF := ulx3s_v316.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v317)
    # v317 and v316 use the same constraint file
    LPF := ulx3s_v316.lpf
else ifeq ($(ULX3S_BOARD_VERSION),v318)
    # v318 and v316 use the same constraint file
    LPF := ulx3s_v316.lpf
else
    # some specific versions of boards use a common LPF file, grouped here in parenthesis:
    $(error Unsupported ULX3S_BOARD_VERSION "$(ULX3S_BOARD_VERSION)". Use (v17, v17patch), (v20, v307), (v314), or (v316, v317, v318))
endif
```
