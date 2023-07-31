## Challenge 1 - Logical

This repository contains an assembly program that involves logical operations in a RISC-V processor. During the testing process, two specific lines of code, `15855` and `25584`, encountered errors due to illegal operands. As a result, these lines were commented out, and the `make` function now works correctly.

### Issues and Resolutions

1. Error in Line 15855:
   The instruction `s7, r4, z4` raised an error due to using `z4` as an operand, which is not a valid register in the RISC-V architecture. As a result, the instruction cannot be executed, and an error is returned.

   **Resolution:** To fix this error, the code must be updated to use a valid register or a constant instead of `z4` in the instruction.

2. Error in Line 25584:
   The instruction `andi s5, t1, s0` raised an error because the `andi` instruction performs bitwise AND between the two operands, but it expects the third operand (i.e., `s0`) to be an immediate constant rather than a register.

   **Resolution:** To fix this error, the code needs to replace `s0` with an immediate constant, or alternatively, the line can be commented out if it is not needed for the intended logical operation.
