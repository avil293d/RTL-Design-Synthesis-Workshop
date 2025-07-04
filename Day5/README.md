## If-Else Statements in Verilog

If-else statements allow conditional execution inside procedural blocks such as `always`, `initial`, tasks, or functions.

### Syntax

```verilog
if (condition) begin
    // Code if condition is true
end else begin
    // Code if condition is false
end
```

- `condition` evaluates to true or false.
- `begin ... end` groups multiple statements.
- `else` is optional.

#### Nested If-Else

```verilog
if (condition1) begin
    // Code if condition1 is true
end else if (condition2) begin
    // Code if condition2 is true
end else begin
    // Code if no conditions are true
end
```

---

## Inferred Latches in Verilog

A latch is inferred when a combinational logic block does not assign a variable on all execution paths.

### Example

```verilog
module ex (
    input wire a, b, sel,
    output reg y
);
    always @(a, b, sel) begin
        if (sel == 1'b1)
            y = a; // No else branch
    end
endmodule
```

**Issue:** When `sel` is 0, `y` is not assigned, so a latch is inferred.

**Solution:** Add an else or default assignment.

```verilog
module ex (
    input wire a, b, sel,
    output reg y
);
    always @(a, b, sel) begin
        case(sel)
            1'b1 : y = a;
            default : y = 1'b0;
        endcase
    end
endmodule
```

## For Loops in Verilog

For loops repeat a block of code multiple times inside procedural blocks. The iteration count must be fixed at compile time.

### Syntax

```verilog
for (initialization; condition; increment) begin
    // Statements
end
```


## Generate Blocks in Verilog

Generate blocks create hardware at compile time. Commonly used for repetitive structures.
```verilog
genvar i;
generate
    for (i = 0; i < 4; i = i + 1) begin : gen_loop
        and_gate and_inst (.a(in[i]), .b(in[i+1]), .y(out[i]));
    end
endgenerate
```