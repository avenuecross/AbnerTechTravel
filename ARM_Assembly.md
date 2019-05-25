Sometimes we need to read even write ARM assembly code. I put some universal instructs here for reference.

**ldr** load memory data to register
**str** store register data to memory

```markdown
mov r1, r2
mov r0, #0xFF
mov r0, r1, lsl #3 // r0 = r1*8
ldr r1, [r2]
ldr r1, [r2, #4]
ldmia r1!, {r2-r7, r12}  // load {...} register data into the memory based on address which r1 stores
stmfd sp!, {r2-r7, lr}
```
instruct suffix<br>
**B** operate length becomes 8-bit<br>
**H** operate length becomes 16-bit<br>
**S** signed or change CPSR flag<br>

and 逻辑与<br>
orr 逻辑或<br>
eor 逻辑异或<br>
bic 位清除  // bic r0, r0, #0x1

CPSR需要特别的指令<br>
```markdown
mrs r0, cpsr
bic r0, r0, #0x1f
msr cpsr, r0
```

