## Level 2, Challenge 1 Instructions 

### Introduction

This repository contains a RISC-V test generation and execution program for Level 2, Challenge 1. The goal is to generate random RISC-V instructions using AAPG (Automated Assembly Program Generator) based on the configurations stored in `rv32i.yaml`.

### Issue Encountered

Upon running the `make` command, it was observed that some instructions that are not supported in RV32I (basic without extensions) were being randomly generated through AAPG. This caused errors during compilation, as unsupported instructions, such as `divw`, were present in the generated assembly code.

### Solution

After investigating the issue, it was discovered that the problem arose from the generation of RV64M instructions. To resolve this, the `rv32i.yaml` configuration file needed modification.

The option `rel_rv64m` in `rv32i.yaml` at line 66 was initially set to `10`. By changing it to `0`, no RV64M instructions are generated, and the issue with unsupported instructions is resolved.

