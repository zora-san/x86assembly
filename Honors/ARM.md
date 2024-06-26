# Lab: Assembly language for ARM processors

## Tasks
Perform the following tasks:  
1. Research and find out how different assembly language is for ARM processors compared to Intel processors.
2. The following assembly code is written for an Intel 32-bit processor. Convert the code for the ARM processor, and execute it.
3. Based on your research, will you be able to quantify the efficiency of running an assembly code on Intel & ARM processors?


**1. How different is assembly language for ARM processors compared to Intel processors?**

The assembly language utilized for ARM processors stands in great contrast to the assembly language of Intel processors. We will dive into the variations across instruction set architecture (ISA), syntax, register usage, and addressing modes.

&nbsp;&nbsp;&nbsp;&nbsp;In terms of the Instruction Set Architecture (ISA), ARM processors operate under a RISC (Reduced Instruction Set Computing) architecture, while Intel processors function on a CISC (Complex Instruction Set Computing) architecture. RISC architectures, exemplified by ARM, uses a simpler and more standardized instructions compared to the more complex CISC architectures of Intel. ARM's instruction set is also more finely tuned for efficient task execution, resulting in a more streamlined array of instructions.  
&nbsp;&nbsp;&nbsp;&nbsp;ARM assembly and Intel assembly have different syntax, such as for instructions and directives. Additionally, nuances in comments and formatting conventions are also not the same. It's important to recognize that assembly code designed for Intel processors necessitates substantial modifications for seamless adaptation to ARM processors, given the distinct architectural and instructional disparities. Between ARM processors and Intel processors, the register usage also varies - ARM processors use a narrower selection of general-purpose registers when compared to Intel processors. ARM assembly language often adopts register labels like R0, R1, etc., while Intel assembly language uses designations such as EAX, EBX, etc.  
&nbsp;&nbsp;&nbsp;&nbsp;Compared to Intel assembly, ARM assembly language extends support to a reduced set of addressing modes. Addressing modes in assembly language define how instructions specify the location of operands (data) in memory or registers. The prevalent use of load/store architecture in ARM assembly means operations occur predominantly between registers rather than directly accessing memory. In ARM assembly, the addressing modes available for accessing data from memory or specifying operands in instructions are fewer in number compared to Intel assembly. This limitation in addressing modes can influence the way programmers write code and perform memory operations in ARM assembly language.  

**2. Convert the Intel 32-bit processor assembly code to ARM processor assembly code, and execute.**  
$var4 = (var1+var2)*var3$

```assembly
section .text
    global _start

_start:
    mov eax,[var1]
    add eax,[var2]
    mov dl,[var3]
    mul dl
    mov [var4],eax
    
    mov eax,1
    int 0x80

section .data
    var1 DD 5 ; var1 is assigned 5
    var2 DD 2 ; var2 is assigned 2
    var3 DD 3 ; var3 is assigned 3
    
segment .bss
    var4 resb 1
```

**Share the source code and write down the commands used to make the source code executable.**
```assembly
.section .text
    .global _start

_start:
    ldr r1, =var1      @ load var1 into r1 (ldr = load register)
    ldr r2, [r1]        @ load the value at memory location var1 into r2 (use brackets to access mem location)
    ldr r3, =var2      @ load var2 into r3
    ldr r4, [r3]        @ load the value at memory location var2 into r4
    add r5, r2, r4      @ add var1 and var2, result in r5 (result first, additions after)
    
    ldrb r6, =var3     @ load var3 into r6 (using load register byte, specifically for loading a single byte from                         @ memory to register)
    ldrb r7, [r6]       @ load the value at memory location var3 into r7 (using byte load)
    mul r5, r5, r7      @ multiply var1+var2 by var3
    
    ldr r8, =var4      @ load var4 into r8
    str r5, [r8]        @ store the result into memory location var4
    
    mov r7, #1          @ prepare to make an exit syscall
    swi 0x0             @ exit program

.section .data
var1:    .word 5       @ var1 is assigned 5
var2:    .word 2       @ var2 is assigned 2
var3:    .byte 3       @ var3 is assigned 3

.section .bss
var4:    .skip 4       @ reserve 4 bytes for var4
```
**3. Based on your research, will you be able to quantify the efficiency of running an assembly code on Intel & ARM processors?**

- **Architecture Differences**:
  - Intel and ARM processors have distinct architectures, including differences in instruction set architecture (ISA), register layout, and pipeline design.
  - Efficiency depends on how well the code utilizes specific features and optimizations of each architecture.

- **Performance Characteristics**:
  - Intel processors are often designed for high-performance computing tasks, boasting higher clock speeds, larger cache sizes, and more advanced instruction sets.
  - ARM processors prioritize power efficiency and are commonly used in mobile and embedded systems.
  - ARM instructions are typically fixed-length (32 bits) and often operate directly on registers, while Intel instructions can vary in length and may require more memory accesses.
  - ARM's load-store architecture offers more predictable memory access patterns than Intel's more complex schemes.

- **Optimization Strategies**:
  - Assembly code can be optimized differently for Intel and ARM processors to leverage their respective strengths.
  - Techniques include instruction selection, register allocation, loop unrolling, and memory access optimizations.

- **Benchmarking and Profiling**:
  - Benchmarking and profiling tools are essential for measuring code execution under different workloads and identifying performance bottlenecks.
  
- **Compiler Optimizations**:
  - Different compilers may produce varying results, and optimization flags can significantly impact performance.
  - Considerations such as data types and alignment requirements can affect efficiency, particularly regarding memory access.

- **System Calls**:
  - System call overheads may differ between ARM and Intel architectures, depending on the method used and the OS's handling of system calls.

- **Conclusion**:
  - Assessing efficiency comprehensively requires considering various factors such as architecture differences, optimization strategies, compiler behavior, memory access patterns, and system call overheads.
  - Direct quantification may be complex and may vary across different scenarios and hardware configurations.


**Create and share a video that explains the process of assembling, linking, running, and debugging the source code.**
