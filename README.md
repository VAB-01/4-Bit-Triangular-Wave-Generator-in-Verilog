# 4-Bit Triangular Wave Generator in Verilog

## Overview

This project implements a **4-bit Triangular Wave Generator** using Verilog HDL.

The design generates a digital triangular waveform by continuously increasing and decreasing a 4-bit output value. A direction control flag determines whether the counter is moving upward or downward.

The project is intended as a beginner-friendly exercise in:

* Sequential logic design
* Verilog HDL programming
* Counter implementation
* Waveform generation
* Simulation and verification

---

## Design Description

The triangular waveform is generated using a 4-bit register (`out`) and a direction control register (`direction`).

### Up-counting Mode

When `direction = 0`:

* The output value increments on every positive clock edge.
* Counting continues until the upper limit is reached.

### Down-counting Mode

When `direction = 1`:

* The output value decrements on every positive clock edge.
* Counting continues until the lower limit is reached.

### Direction Reversal

The direction flag changes state whenever:

* The output reaches the maximum count value.
* The output reaches the minimum count value.

This causes the waveform to repeatedly rise and fall, creating a triangular pattern.

---

## Inputs and Outputs

| Signal  | Width  | Description            |
| ------- | ------ | ---------------------- |
| `clk`   | 1 bit  | System clock           |
| `reset` | 1 bit  | Asynchronous reset     |
| `out`   | 4 bits | Triangular wave output |

---

## Module Declaration

```verilog
module triangular(
    input wire clk,
    input wire reset,
    output reg [3:0] out
);
```

---

## Internal Registers

### Direction Register

```verilog
reg direction;
```

| Value | Meaning    |
| ----- | ---------- |
| 0     | Count Up   |
| 1     | Count Down |

---

## Waveform Behavior

Example output sequence:

```text
0 → 1 → 2 → 3 → 4 → 5 → 6 → 7
→ 8 → 9 → A → B → C → D → E
→ D → C → B → A → 9 → 8 → 7
→ 6 → 5 → 4 → 3 → 2 → 1 → 0
→ 1 → 2 → ...
```

Graphically:

```text
15 |        /\ 
   |       /  \
   |      /    \
   |     /      \
   |    /        \
 0 |___/          \____
          Time →
```

---

## Reset Operation

When reset is asserted:

```verilog
if(reset)
```

the circuit:

* Clears the waveform generation process
* Sets the counting direction to upward mode
* Initializes the output value

---

## Simulation

### Compile

```bash
iverilog -o triangular_sim triangular.v triangular_tb.v
```

### Run

```bash
vvp triangular_sim
```

### View Waveforms

```bash
gtkwave triangular.vcd
```

---

## Expected Results

The simulation waveform should show:

* Output increasing from the lower limit
* Output decreasing after reaching the upper limit
* Continuous repetition of the process

The resulting waveform resembles a digital triangular wave.

---

## Learning Concepts

This project demonstrates:

* Edge-triggered sequential logic
* State control using flags
* Up-down counters
* Verilog procedural blocks
* Digital waveform generation

---

## Known Limitations

This version was developed as a learning exercise and may require further refinement for synthesis and production use. Possible improvements include:

* Cleaner state-transition logic
* Fully synchronous design
* Parameterized counter width
* Configurable amplitude limits
* Adjustable waveform frequency

---

## Author

Created as part of Verilog HDL practice for digital design and waveform generation.
