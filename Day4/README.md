## Gate-Level Simulation (GLS)

**Gate-Level Simulation (GLS)** is an essential step in digital design verification. It ensures that the synthesized netlist works correctly after RTL synthesis.

**Why perform GLS?**

-  **Synthesis Validation:** Verifies that synthesis tools correctly translated RTL to netlist.
-  **Timing Verification:** Checks for timing violations using realistic delays (SDF).
-  **Testability:** Ensures scan chains and other test structures work post-synthesis.

### When to perform GLS?

- **After Synthesis:** When RTL is converted into a gate-level netlist.
- **Before Physical Design:** To catch issues early.

### Types of GLS

- **Functional GLS:** Logic-only simulation (zero/unit delays).
- **Timing GLS:** Uses annotated timing data to check real-world behavior.

## Synthesis-Simulation Mismatch

A **synthesis-simulation mismatch** happens when the RTL simulation results do not match the post-synthesis gate-level simulation or actual silicon.

### Common causes:

-  Non-synthesizable constructs (`initial` blocks, delays).
-  Incomplete/ambiguous RTL (missing `else`, incomplete sensitivity lists).
-  Tool interpretation differences.


## Blocking vs. Non-Blocking Assignments in Verilog

Verilog uses two assignment types:

### Blocking (=)

- Executes immediately, sequentially.
- Used for combinational logic (`always @(*)`).

```verilog
always @(*) y = a & b;
```

### Non-Blocking (<=)

- Executes concurrently, scheduled at end of timestep.
- Used for sequential logic (`always @(posedge clk)`).

```verilog
always @(posedge clk) q <= d;
```