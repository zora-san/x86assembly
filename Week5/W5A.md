
# W5a - I came, I saw, I conquered

```assembly
section .text           ;  Contain executable instruction, start code 
        global _start   ;  Declare _start as entry point

_start:                 ;  Label to indicate the start of the program

        mov eax, 4      ;  System call number for sys_write (write)
        mov ebx, 1      ;  File descriptor for standard output (stdout)
        mov ecx, caesar ;  Pointer to the message to write
        mov edx, len    ;  Length of the message
        int 0x80        ;  Call kernel to perform the system call

        mov eax, 1      ;  System call number for sys_exit (exit)
        int 0x80        ;  Call kernel (perform the system call to exit)

section .data           ;  Start of the data section

caesar DB 'I came,', 0xa, 'I saw,', 0xa, 'I conquered.', 0xa    
                        ;  Define the message string with newlines

len equ $ - caesar      ;  Calculate the length of the message

```

## What were your challenges in performing the lab (from design to the implementation phases)?

I found designing this code was a fun first foray with Assembly code. The difficulties that I experienced were mainly related to understanding the new syntax and the necessary commands in order to get the code to work. I learned the purpose of section .text, start, and section .data, as well as the commands for sys_write, standard output, calling the kernel, and sys_exit! I also needed to make sure to calculate the length of the message. 



This first assembly code was all in all a pretty simple task. It is exciting to explore the possibilities of ASM and get closer to the computer!  


