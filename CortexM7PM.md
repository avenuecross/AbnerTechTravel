Some tips about Cortex-M7, more details can get from ARM official documnet. This blog is referring to DUI0646B(ARM Cortex-M7 Devices Generic User Guide).

## Processor mode and privilege levels for software execution
The processor modes:<br>
* Thread mode --> Used to execute application software. The processor enters Thread mode when it comes out of reset.<br>
* Handler mode --> Used to handle exceptions. The processor returns to Thread mode when it has finished all exception processing.<br>

The privilege levels for software execution:<br>
* Unprivileged --> 1. Has limited access to the MSR and MRS instructions, and cannot use the CPS instruction
                   2. Cannot access the system timer, NVIC, or system control block.
                   3. Might have restricted access to memory or peripherals.
* Privileged --> The software can use all the instructions and has access to all resources. Privileged software executes at the privileged level.

In Thread mode, the CONTROL register controls whether software execution is privileged or unprivileged, see CONTROL register on page 2-9.
In Handler mode, software execution is always privileged.
Only privileged software can write to the CONTROL register to change the privilege level for software execution in Thread mode.
Unprivileged software can use the SVC instruction to make a supervisor call to transfer control to privileged software.

## Stack
M7 uses a full descending stack.

