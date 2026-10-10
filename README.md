
# SCL Memory Cut Tapeout — SPICE Simulation & Validation

This repository documents SPICE-based functional simulations of the **C2S0155 control signals** and two SCL single-port SRAM (SPRAM) configurations: **64 × 32** and **16 × 4**.

The simulation report includes schematic testbenches, transient waveform analysis, and memory read/write test cases.

## Project Overview

The work focuses on functional evaluation of memory macros and associated control signals as part of an SCL memory-cut tapeout project.

### Simulation Summary

| Block | Simulation Period | Description |
|---|---|---|
| C2S0155 | 200 ns | Chip-select and enable signal simulation |
| SPRAM 64 × 32 | 800 ns | Memory read simulation |
| SPRAM 16 × 4 | 800 ns | Memory write and read simulations |

## 1. C2S0155 SPICE Simulation

The testbench applies manually controlled voltage sources to the chip-select inputs and observes the corresponding output signals.

### Signal Mapping

| Input Signal | Output Signal |
|---|---|
| `CSB1_in` | `CSB1_out` |
| `CSB2_in` | `CE_out` |

**Simulation Duration:** 200 ns

The transient waveforms are documented in the simulation report.

## 2. SPRAM 64 × 32 Simulation

SPRAM 64 × 32 is a single-port SRAM configuration with:

- Memory depth: 64 words
- Data width: 32 bits
- Simulation duration: 800 ns

### Read Operation

The documented read test selects memory address `0`.

| Parameter | Value |
|---|---|
| Address | `0` |
| Expected data slice | `1010` |
| Observed output | `Out_mem[7:4]` |
| Reported result | `1010` |

The simulation report contains waveform screenshots and the schematic testbench used for this memory configuration.

## 3. SPRAM 16 × 4 Simulation

SPRAM 16 × 4 is a single-port SRAM configuration with:

- Memory depth: 16 words
- Data width: 4 bits
- Simulation duration: 800 ns

### Write Cycle

During write operations:

- `WEB_in = 0` — Write enabled
- `OEB_in = 1` — Output disabled

| Address | Written Data |
|---|---|
| `0` | `1010` |
| `1` | `0101` |

### Read Cycle

During read operations:

- `WEB_in = 1` — Write disabled
- `OEB_in = 0` — Output enabled

| Address | Reported Read Data |
|---|---|
| `0` | `1010` |
| `1` | `0101` |

### Control Signal Summary

| Operation | WEB_in | OEB_in |
|---|---|---|
| Write | LOW | HIGH |
| Read | HIGH | LOW |

The documented waveforms show the reported data values during the memory read operations.

**Important:** The original simulation report notes that the SPRAM 16 × 4 vector file mistakenly used a 1.0 V input stimulus. This must be corrected and the test rerun before using the results for final validation.

## 4. Simulation and Verification Methodology

The documented approach includes:

1. Preparing the memory testbench schematic.
2. Applying control and input stimuli.
3. Running SPICE transient simulations.
4. Monitoring memory control signals and output data.
5. Examining waveform behavior for the selected operations.
6. Comparing observed output data with the intended test values.

## 5. Simulation Documentation

The complete simulation report contains:

- C2S0155 transient waveforms
- SPRAM 64 × 32 read-operation waveforms
- SPRAM 64 × 32 testbench schematic
- SPRAM 16 × 4 testbench schematic
- SPRAM 16 × 4 write-operation waveforms
- SPRAM 16 × 4 read-operation waveforms

**[View the Complete Simulation Report](C2S0155_Chip_In.docx)**

## 6. Repository Structure

```text
Memory_Cut_SCL_Tapeout/
│
├── README.md
│
└── C2S0155_Chip_In.docx
```

## 7. Verification Scope

The results document selected functional tests of the control signals and SRAM macros.

They do not establish complete verification across all memory addresses, process corners, voltage conditions, or temperature conditions.

The underlying simulation decks, models, and proprietary design libraries are not included in this documentation-only repository.

## Project Focus

- SRAM macro functional simulation
- SPICE transient waveform analysis
- Memory read/write control verification
- Schematic-based simulation
- Memory-cut tapeout documentation

GitHub: [@deba0272](https://github.com/deba0272)

---

**Note:** This repository documents selected memory simulation results. Foundry PDK files, proprietary memory models, and other confidential design materials are not uploaded as per NDA norms.
