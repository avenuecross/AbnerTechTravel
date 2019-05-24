在开发过程中经常会遇到一些Hardfault问题，需要去定位错误发生时的指令位置。ARM官方有一份相关文档，对调试这方面问题有很大帮助，在此整理一下。
来源文档Using Cortex-M3/M4/M7 Fault Exceptions(APNT209), 不贴链接了，可以去搜。

Cortex-M处理器有一套异常处理机制，它可以侦测以下的一些异常
* HardFault: is the default exception and can be triggered because of an error during exception processing, or because an exception cannot be managed by any other exception mechanism.
* MemManage: detects memory access violations to regions that are defined in the Memory Management Unit (MPU); for example, code execution from a memory region with read/write access only.
* BusFault: detects memory access errors on instruction fetch, data read/write, interrupt vector fetch, and register stacking (save/restore) on interrupt (entry/exit).
* UsageFault: detects execution of undefined instructions, unaligned memory access for load/store multiple. When enabled, divide-by-zero and other unaligned memory accesses are detected.

![Fault Priority](/Fault_Priority.PNG)
