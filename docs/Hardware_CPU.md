### ISA

Probably the first confusing thing is instruction set architecture, so we start from a table below.

|ISA|Design|Bits|Begins|
|---|---|---|---|
|x86|CISC|16, 32, 64|1978|
|ARM|RISC|32|1983|
|ARM64|RISC|64|2011|
|RISC-V|RISC|32, 64, 128|2010|
|MIPS|RISC|32, 64|1981|

### ARM64

10 years after, we have many ARM64 computer, and we heard RISC many times, which makes CISC sounds out. But there is really no absolute superiority anyway.
In short,
- CISC: The CISC approach attempts to minimize the number of instructions per program but at the cost of an increase in the number of cycles per instruction. 
- RISC: Reduce the cycles per instruction at the cost of the number of instructions per program. 

In long,
|CISC|RISC|
|----|----|
|Uses both hardwired and microprogrammed control unit|Focus on software	Focus on hardware|Uses only Hardwired control unit|
|Several-cycle instruction|Single-cycle instruction|
|Efficient use of RAM|Heavy use of RAM|
|Large number of instruction|Small number of fix-lenght instruction|

### CPI

Clock per instruction is a simple mearsument of the CPU speed, basicly the smaller the better.

CPU time = Instruction count x CPI / clock rate

For a RISC CPU, in university, its instruction usually falls into 5 groups,
- Instruction fetch cycle (IF).
- Instruction decode/Register fetch cycle (ID).
- Execution/Effective address cycle (EX).
- Memory access (MEM).
- Write-back cycle (WB).

And in factory, its groups extends much more, see [A64](https://developer.arm.com/documentation/ddi0602/2021-12/Base-Instructions?lang=en)(now we have A64, A32, T32 :sweat_smile:)

So if we want our program runs fast, we really have three ways,
- make the program code less, meaning smarter algorithm so inst count less
- make CPI smaller, meanning smarter ISA or shorter pipeline
- make clock frequency higher

### assembly

Before to try asm, we first should know which isa we want to use, so we have to learn the relationship.
|ARM family|ARM architecture|
|---|---|
|ARM7|	ARM v4|
|ARM9|	ARM v5|
|ARM11|	ARM v6|
|Cortex-A|	ARM v7-A|
|Cortex-R|	ARM v7-R|
|Cortex-M|	ARM v7-M|

asm is composed of instructions which are the main building blocks.
ARM instructions are usually followed by one or two operands and generally use the following template: `MNEMONIC{S}{condition} {Rd}, Operand1, Operand2`

The meaning,
~~~
MNEMONIC     - Short name (mnemonic) of the instruction
{S}          - An optional suffix. If S is specified, the condition flags are updated on the result of the operation
{condition}  - Condition that is needed to be met in order for the instruction to be executed
{Rd}         - Register (destination) for storing the result of the instruction
Operand1     - First operand. Either a register or an immediate value 
Operand2     - Second (flexible) operand. Can be an immediate value (number) or a register with an optional shift
~~~

Operand2 fields are closely tied to the CPSR,
~~~
#123                    - Immediate value (with limited set of values). 
Rx                      - Register x (like R1, R2, R3 ...)
Rx, ASR n               - Register x with arithmetic shift right by n bits (1 = n = 32)
Rx, LSL n               - Register x with logical shift left by n bits (0 = n = 31)
Rx, LSR n               - Register x with logical shift right by n bits (1 = n = 32)
Rx, ROR n               - Register x with rotate right by n bits (1 = n = 31)
Rx, RRX                 - Register x with rotate right by one bit, with extend
~~~

### Instruction Count

```
$ cat e3.s
// e3.s
.text
.globl main

main:
  add w0, w0, #1   // w0 ← w0 + 1
  ret              // return from main

$ gcc -c -g e3.s
$ gcc -o e3 e3.o
```

:question: is one line one instruction?

In C, there are three kinds of instruction: declare, arithmetic and contorl.
For control, there are four kinds:
|||
|----|----|
|Sequentail|Order|
|Decision|If..Else statement or If..Else If..Else statement|
|Loop|While loop or Do/While loop or For loop statement|
|Case|Switch Case statements|







<a href="#top">Back to top</a>
