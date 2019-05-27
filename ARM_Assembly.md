Sometimes we need to read even write ARM assembly code. I put some universal instructs here for reference.

**ldr** load memory data to register
**str** store register data to memory

```markdown
mov r1, r2
mov r0, #0xFF
mov r0, r1, lsl #3 // r0 = r1 * 8
ldr r1, [r2]
ldr r1, [r2, #4]
ldmia r1!, {r2-r7, r12}  // load {...} register data into the memory based on address which r1 stores
stmfd sp!, {r2-r7, lr}^ // ^将spsr写入cpsr，一般从异常模式返回
```
##Instruct Suffix<br>
**B** operate length becomes 8-bit<br>
**H** operate length becomes 16-bit<br>
**S** signed or change CPSR flag<br>

For ldm,stm<br>
**ia** 先传输再地址+4<br>
**ib** 先地址+4再传输<br>
**da** 先传输再地址-4<br>
**db** 先地址-4再传输<br>
**fd** 满递减堆栈<br>
**ed** 空递减堆栈<br>
**fa** 满递增堆栈<br>
**ea** 空递增堆栈<br>

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

b 直接跳转<br>
bl 保存lr返回的跳转<br>
bx 切换到ARM模式，一般用于异常处理的跳转<br>
```markdown
swp r1, r1, [r0] //交换register和memory的内容
```
合法立即数-移位后非零部分可用8位表示，主要是用在纯指令场合，伪指令不会有这个问题

mrc-读取CP15中的寄存器<br>
mcr-写入CP15中的寄存器<br>
