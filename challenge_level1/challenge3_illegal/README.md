## Challenge 3 - Illegal

This repository contains an assembly program that involves handling illegal instruction exceptions in a RISC-V processor. The program includes an illegal instruction, `.word 0`, which triggers an exception. The `mtvec` (Machine Trap Vector) is set to handle exceptions using the `mtvec_handler`.

### Exception Handling Process

When executing the `.word 0` instruction, the current Program Counter (PC) is stored in the `mepc` (Machine Exception Program Counter) register, and control is transferred to the `mtvec_handler`.

Inside the `mtvec_handler`, we check whether the cause of the exception is an illegal instruction using the `mcause` (Machine Cause) register. In the RISC-V ISA, the code "2" represents an illegal instruction.

**Incorrect Handling:**
Currently, if the exception is not caused by an illegal instruction, the program jumps to `fail`. However, if it is an illegal instruction, the program enters an infinite loop by using `mret` to return back to the instruction that caused the exception, which happens to be the same illegal instruction (`j fail`).

### Correct Exception Handling

To handle the illegal instruction exception correctly, we should modify the `mtvec_handler` as follows:

```assembly
mtvec_handler:
  li t1, CAUSE_ILLEGAL_INSTRUCTION
  csrr t0, mcause
  bne t0, t1, fail             # If not an illegal instruction, jump to fail
  csrr t0, mepc
  addi t0, t0, 4               # Increase the PC by 4 to skip the illegal instruction
  csrw mepc, t0                # Write the updated PC to the mepc
  mret                         # Return to the next instruction after the illegal one
```

With this modification, when the `mtvec_handler` identifies an illegal instruction exception, it increments the PC by 4 to skip the illegal instruction and then writes the updated PC to `mepc`. By doing so, the program will resume execution at the next valid instruction after the illegal one.