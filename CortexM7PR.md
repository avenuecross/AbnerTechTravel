Some tips about Cortex-M7, more details can get from ARM official documnet. This blog is referring to DUI0646B(ARM Cortex-M7 Devices Generic User Guide).

## Processor mode and privilege levels for software execution
The processor modes:<br>
* Thread mode --> Used to execute application software. The processor enters Thread mode when it comes out of reset.<br>
* Handler mode --> Used to handle exceptions. The processor returns to Thread mode when it has finished all exception processing.<br>

The privilege levels for software execution:<br>
* Unprivileged --> 1. Has limited access to the MSR and MRS instructions, and cannot use the CPS instruction<br>
                   2. Cannot access the system timer, NVIC, or system control block.<br>
                   3. Might have restricted access to memory or peripherals.<br>
* Privileged --> The software can use all the instructions and has access to all resources. Privileged software executes at the privileged level.

In Thread mode, the CONTROL register controls whether software execution is privileged or unprivileged, see CONTROL register on page 2-9.
In Handler mode, software execution is always privileged.
Only privileged software can write to the CONTROL register to change the privilege level for software execution in Thread mode.
Unprivileged software can use the SVC instruction to make a supervisor call to transfer control to privileged software.

## Stack
M7 uses a full descending stack.<br>
The processor implements two stacks, the main stack and the process stack, with a pointer for each held in independent registers.
In Thread mode, bit[1] of the CONTROL register indicates the stack pointer to use: 0 -- MSP(reset is 0) 1 -- PSP.
On reset, the processor loads the MSP with the value from the implementation-defined address 0x00000000.


On reset, the processor sets the LR value to 0xFFFFFFFF.

The Cortex-M7 processor only supports execution of instructions in Thumb state.
The following can clear the T bit to 0:<br>
• Instructions BLX, BX, LDR pc, [], and POP{PC}.<br>
• Restoration from the stacked xPSR value on an exception return.<br>
• Bit[0] of the vector value on an exception entry or reset.<br>
Attempting to execute instructions when the T bit is 0 results in a fault or lockup.<br>

Cortex-M7 speculative access:
https://developer.arm.com/docs/ddi0489/f/memory-system/speculative-accesses.

