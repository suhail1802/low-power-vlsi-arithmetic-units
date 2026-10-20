# low-power-vlsi-arithmetic-units
Verilog RTL implementation and verification of an NxN row-bypassing multiplier using hybrid prefix adders.
# Design and Implementation of NxN Multiplier Architecture Based on Row-Bypassing and Hybrid Adders

## Overview

This project presents a parameterizable unsigned NxN multiplier architecture implemented in Verilog HDL. It combines row-bypassing techniques, carry-save arithmetic, a hybrid adder architecture, and quadrant-based decomposition to explore improvements in switching activity, carry propagation, and hardware efficiency.

The project was developed as part of an internship at the Centre for Nanoelectronics and VLSI Design (CNVD), VIT Chennai.

## Objectives

- Design a parameterizable unsigned NxN multiplier using Verilog HDL.
- Implement row-bypassing logic to avoid unnecessary arithmetic operations when multiplier bits are zero.
- Integrate Han–Carlson, Weinberger, and Ling adder structures into a hybrid adder.
- Use quadrant-based decomposition for modular multiplier design.
- Verify functional correctness using simulation in Xilinx Vivado.

## Architecture

### 1. Row-Bypassing Multiplier

The multiplier uses partial-product generation and carry-save arithmetic with row-bypassing logic.

When a multiplier bit is zero, the corresponding partial-product row contributes no new arithmetic information. The bypass logic is designed to preserve the existing sum and carry information rather than performing unnecessary full-adder operations.

**Design objective:** Reduce unnecessary switching activity and improve dynamic power efficiency.

### 2. Hybrid Adder Architecture

The hybrid adder combines three 4-bit adder structures:

- **Han–Carlson adder:** Uses a prefix-based carry computation structure.
- **Weinberger adder:** Provides an alternative prefix carry-computation arrangement.
- **Ling adder:** Uses Ling-style carry generation to support efficient carry computation.

The 4-bit blocks are combined in a repeating pattern to construct a parameterizable N-bit hybrid adder.

### 3. Quadrant-Based Multiplier

The complete multiplier divides the input operands into high and low halves, producing four partial products:

- PR = A_low × B_low
- PS = A_low × B_high
- QR = A_high × B_low
- QS = A_high × B_high

The partial products are shifted according to their bit positions and combined using hybrid-adder stages to generate the final 2N-bit product.

This approach provides a modular structure for constructing larger multipliers from smaller multiplier blocks.

## Design Flow

1. Develop the row-bypass full-adder cell and multiplier architecture.
2. Implement the Han–Carlson, Weinberger, and Ling 4-bit adder modules.
3. Integrate the modules into a parameterizable hybrid adder.
4. Construct the quadrant-based multiplier and partial-product summation stages.
5. Verify the adder, row-bypassing multiplier, and complete multiplier using Verilog testbenches.
6. Compare simulated outputs against reference results.

## Tools and Technologies

- **HDL:** Verilog
- **Simulation and synthesis environment:** Xilinx Vivado
- **Design concepts:** Carry-save arithmetic, row bypassing, parallel-prefix addition, quadrant decomposition
- **Verification:** Testbenches with reference-result comparison

## Functional Verification

The project report documents the following simulation cases:

| Test stage | Input operands | Reported result |
|---|---|---|
| Hybrid adder | A = `0x0ABCD`, B = `0x01234`, Cin = 1 | Sum = `0x0BE02`, matching the expected result |
| Row-bypassing multiplier | A = `0x8037`, B = `0xDED1` | Product = `0x0ED6846B`, matching the reference |
| Complete NxN multiplier | A = `0xBEEF`, B = `0xCAFE` | Product = `0x97660722`, matching the reference |

The report states that the complete multiplier was functionally verified for N = 16.

These are functional simulation results reported by the project; they are not measurements of silicon performance.

## Results and Discussion

The project demonstrates the integration of row-bypassing arithmetic, hybrid carry computation, and quadrant decomposition into a modular multiplier architecture.

The intended benefits include:

- Avoiding unnecessary activity in inactive multiplier rows.
- Improving carry computation compared with conventional ripple-carry approaches.
- Supporting parameterizable operand widths.
- Enabling modular design and verification of individual arithmetic components.

Quantitative power, area, and propagation-delay improvements should be reported only when supported by the corresponding synthesis or implementation reports and a clearly defined baseline.

## Repository Structure

```text
.
├── README.md
├── rtl/
│   ├── csa_bypass_fa.v
│   ├── mulNxN_csa_row_bypass.v
│   ├── han_carlson_4bit.v
│   ├── weinberger_4bit.v
│   ├── ling_4bit.v
│   ├── hybrid_adder_nbit.v
│   └── mul_quadrant_rowbypass_hybrid.v
├── tb/
│   ├── tb_multiplier.v
│   └── tb_hybrid_adder.v
├── docs/
│   └── methodology.md
└── results/
    └── simulation/
```

## Future Improvements

- Perform quantitative power, area, and timing analysis against a defined baseline.
- Automate verification across multiple operand widths.
- Compare alternative hybrid-adder configurations.
- Document synthesis constraints, tool versions, and reproducible implementation results.

## Acknowledgment

This project was developed at the Centre for Nanoelectronics and VLSI Design (CNVD), VIT Chennai, as part of the B.Tech. Electronics and Communication Engineering internship project.



