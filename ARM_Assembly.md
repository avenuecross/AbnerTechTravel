This page lists some ARM assembly usage. Put some universal knowledge here for reference.

# ARM Assembly Call Interface
ATPCS(ARM-Thumb Procedure Call Standard) and AAPCS(ARM Archtecture Procedure Call Standard)
AAPCS is the improvement version of ATPCS.
## Register
R0-R3 for 4 input parameters and R0(plus R1 for u64 type) for return value
R4-R11 for local variants.
R12 Call temp register
R13 Stack pointer
R14 Link register
R15 PC

参数个数可变子程序参数传递规则
对于参数个数可变的子程序，当参数个数不超过4个时，可以使用寄存器R0～R3来传递参数；当参数超过4个时，还可以使用堆栈来传递参数。
在传递参数时，将所有参数看作是存放在连续的内存字单元的字数据。然后，依次将各字数据传递到寄存器R0，R1，R2和R3中。如果参数多于4个，则将剩余的字数据传递到堆栈中。入栈的顺序与参数传递顺序相反，即最后一个字数据先入栈。
参数个数固定子程序参数传递规则
如果系统不包含浮点运算的硬件部件，浮点参数会通过相应的规则转换成整数参数（若没有浮点参数，此步省略），然后依次将各字数据传送到寄存器R0～R3中。如果参数多于4个，将剩余的字数据传送堆栈中，入栈的顺序与参数顺序相反，即最后一个字数据先入栈。在参数传递时，将所有参数看作是存放在连续的内存字单元的字数据。

## Stack
Full Descending满递减堆栈
ATPCS规定,堆栈操作8字节对齐,经常使用的指令有STMFD和LDMFD.

# Instruction
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
## Instruct Suffix
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
orr 逻辑或  ORR R0, R0, #3<br>
eor 逻辑异或<br>
bic 位清除  // bic r0, r0, #0x1

b 直接跳转<br>
bl 保存lr返回的跳转<br>
bx 切换到ARM模式，一般用于异常处理的跳转<br>
```markdown
swp r1, r1, [r0] //交换register和memory的内容
```
合法立即数-移位后非零部分可用8位表示，主要是用在纯指令场合，伪指令不会有这个问题

CPSR需要特别的指令<br>
```markdown
mrs r0, cpsr
bic r0, r0, #0x1f
msr cpsr, r0
```

mrc-读取CP15中的寄存器<br>
mcr-写入CP15中的寄存器<br>

Keil MDK的ABI要求在函数调用时，系统必须保证堆栈指针8byte对齐，即每次进栈或者出栈的寄存器数目必须为偶数。<br>
这是为了能够更加高效的使用STM与LDR指令对“double”或者“long long”类型的数据进行访问。<br>
1.在每个汇编文件的开头，添加PRESERVE8<br>
2.代码一次性将5个寄存器压栈，由于ARM的指令寄存器宽度为32位，即4byte，显然5个寄存器入栈之后，堆栈指针不能够满足64位，8byte对齐。<br>
为了解决这种情况，我们可以将另外一个并不需要压栈的寄存器R12，同时压栈，这样当6个32位寄存器进栈之后，堆栈就能满足64位对齐了。<br>
STMFD sp!, {r0-r3, lr}<br>
STMFD sp!, {r0-r3, r12, lr}<br>

Reference Document: https://beginners.re/RE4B-CN-partial/html/RE4B-CN-partial.html
