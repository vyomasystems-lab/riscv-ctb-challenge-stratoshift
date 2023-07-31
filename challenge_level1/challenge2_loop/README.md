Sure, let's further improve the README for better clarity and organization:

## Challenge 2 - Loop

When running the test program, it gets stuck in a loop, preventing the program from completing successfully. To resolve this issue, we need to add an exit condition to the loop. The test program, defined in the "test.S" assembly file, performs a series of memory tests by checking if the sum of two numbers loaded from memory equals a third number. The goal is to exit the loop after verifying all three test cases.

### Test Logic in test.S

The assembly code "test.S" contains the following test logic:

```assembly
loop:
  lw t1, (t0)
  lw t2, 4(t0)
  lw t3, 8(t0)
  add t4, t1, t2
  addi t0, t0, 12
  beq t3, t4, loop        # check if the sum is correct
  j fail
```

### Issue and Solution

Currently, the test program lacks an exit condition for the loop, causing it to become an infinite loop, which prevents successful completion of the test. To resolve this, we need to add a counter to keep track of the number of test cases executed. Let's add an additional register, `t5`, to store the end address of the third test case.

```assembly
# Set up the end address of the third test case
la t5, end_of_testcases
```

Before jumping to the `loop`, we check whether the current address (`t0`) matches the end address (`t5`). If they match, it means all three test cases have been successfully checked, and we can exit the loop. The modified code looks like this:

```assembly
beq t0, t5, test_end  # Exit the loop after verifying all test cases
```

### How the Program Works

The test program uses a loop to iterate through three test cases, performing memory tests on each iteration. It loads three numbers from memory and calculates the sum of the first two. Then, it compares this sum with the third number to check if they are equal. If the sum is correct, it proceeds to the next test case. If any test case fails, the program will jump to the `fail` label, indicating that the tests were unsuccessful. Otherwise, after successfully verifying all three test cases, the program jumps to the `pass` label.
