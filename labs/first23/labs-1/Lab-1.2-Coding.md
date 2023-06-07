# Lab 1.2 - Coding

> This lab is designed to provide instructor assistance. After you have finished the lab exercises, there will be a walk-through session. All code used in this lab will also be shared with you on instructor’s GitHub.

 

*Take a snapshot of your VM at this point so you can revert to it if needed.* 

## 1.0 Template
> Use this template to get started in all coding activities for labs in this workshop.
 

Following code is the basic structure for a 64-bit assembly program. You can use this to get started with your code and build upon it. Read comments for more details on the code itself. 

```bits 64
default rel 
section .data
    ; Declare your data variables here

section .text
global main

main:
    ; Your code goes here

    ; Exit the program
    mov     rax, 60        ; System call number for exit
    xor     rdi, rdi       ; Exit status (0 for success)
    syscall                ; Invoke the system call

```

## 1.2 Printing 

**Exercise**

*Write code in x86-64 assembly that prints the string “JMP RSP” as output, using NASM. Use the template provided in section in 1.0 of this lab.*

----
You can use the following code for this section of the lab. 

**Step 1**

1. Copy the code over to your SASM instance, part by part.

1. Make sure you read the code every time you copy it to SASM and try to understand the purpose of the code. 

Part 1:
```
bits 64
default rel
```

Part 2:
```
segment .data
msg db "JMP RSP", 0xd, 0xa, 0
```

Part 3:
```
segment .text
global main
extern ExitProcess
extern printf
```
Part 4:
```main:
    push    rbp
    mov     rbp, rsp
    sub     rsp, 32

    lea     rcx, [msg]
    call    printf
```
Part 5:
```
xor     rax, rax
    call    ExitProcess
```

**Step 2:**

Build and run the code.

**Step 3:**

Verify the output. It should be “JMP ESP” printed to the screen. 

***You have now completed this section of the lab.*** 


## 1.3 Printing - MASM
**Exercise**

*Write code in x86-64 assembly that prints the string “JMP RSP” as output, using MASM. Use the template provided in section in 1.0 of this lab.* 

**Step 1**

Change the Assembler to MASM is ‘Settings’. 

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.3-1.png)

**Step 2**

1. Copy the code over to your SASM instance.
1. Make sure you read the code every time you copy it to SASM and try to understand the purpose of the code. 


```
.386
.model flat, stdcall
option casemap :none
include \masm32\include\masm32.inc
include \masm32\include\kernel32.inc
include \masm32\macros\macros.asm
includelib \masm32\lib\masm32.lib
includelib \masm32\lib\kernel32.lib
.code
start:
      print "Jump!"
      exit
end start
```

3. Check the output. It should be “Jump!”

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.3-2.png)

## 1.4 Addition

**Step 1**

Change the settings back to NASM

**Step 2**

Write code in the IDE to Add two values (you can copy the code provided below)

 
```
%include "io64.inc"

section .text
    global main
    extern system

main:
    mov rbp, rsp
    
    mov rbx, 1
    mov rcx, 0
    and rbx,rcx
    
    xor rax, rax
    ret 
```
    
    
**Step 3**

Put Breakpoints as shown in the image below (just click on the code line numbers on the side).

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-1.png)

**Step 4**

1. Click on ‘Debug’ from the main Menu and click on ‘Debug’ option (or hit F5). This will start the debugging. 

1. Once the first BP has been reached, the debugging will pause. 

1. At this time, go back to the Debug menu and make sure the options for ‘Show Registers’ and ‘Show Memory’ are checked in (turn them ON). 

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-4.png)

4. Run the program in the Debugger by pressing F5. 

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-3.png)

**Step 5**

Memory section in the debugger: 
![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-5.png) 

1. In the Memory section that appears when debugging, add the register rbx in the ‘Variable’ section. You can do this by double-clicking in that space and then typing in $rbx.


![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-6.png)

**Note** the value for ```rbx``` currently.

2. Leave the other options as default for now.

**Step 6**

Repeat the above steps to add ```$rcx``` as a variable.

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-7.png)

**Step 7**

Hit F5 again (or just run from the menu).

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-8.png)

**Check** the value of ```rbx``` again - it should be 1.


**Step 8**

Hit run again and this time check the value of ```$rcx```  - it should now change to '0'.

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-9.png)

Value for ```rcx``` changes to 0:

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-10.png)

**Step 9**

Hit run again.

Check the value of ```rbx```. 

The addition operation is now complete.

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-11.png)

Value of ```rbx``` is now '0':

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.4-12.png)

**Step 10** (Optional)

Record your findings and notes in the Lab Notes document.


## 1.5 XOR Operation

**Step 1**

Make sure the assembler is set to NASM before you start this lab. 

**Step 2**

Write code in the IDE that performs a XOR operation (you can copy the code provided below)

```
%include "io64.inc"

section .text
    global main
    extern system

main:
    mov rbp, rsp
    
    mov rbx, 1
    mov rcx, 1
    xor rbx,rcx
    
    xor rax, rax
    ret 
```

**Step 3** 

Repeat steps from the previous lab all the way to ‘ret’. 

Place BPs on these lines: 8, 10, 11, 12, 15 

**Step 4** (Optional)

Record your findings and notes in the Lab Notes document. 

## 1.5 JMP Operation

**Step 1**

Make sure the assembler is set to NASM before you start this lab. 

**Step 2**

Write code in the IDE that performs a simple JMP operation (you can copy the code provided below)

```
%include "io64.inc"

section .data
    msg db 'JUMP!', 0
    
section .text
    global main

main:
    mov rbp, rsp
    
    jmp print
    
    mov rbx, 1
    mov rcx, 1
    xor rbx,rcx
    
    xor rax, rax
    ret 
    
print:
    PRINT_STRING msg 
    NEWLINE 
    xor rax, rax 
    ret
``` 


**Step 3**

Repeat steps from the previous lab all the way to ‘```ret```’. 

> Add BPs: 10, 12, 14  - you should not hit the BP at 14!

**Step 4** (Optional)

Record your findings and notes in the Lab Notes document. 

## 1.6 Conditional JMP Operations

### Part 1

**Step 1**

Make sure the assembler is set to NASM before you start this lab. 

**Step 2**

Write code in the IDE that performs a JNZ operation (you can copy the code provided below)
```
%include "io64.inc"

section .data
    msg db 'JUMP!', 0
    
section .text
    global main

main:
    mov rbp, rsp
    
    
    
    mov rbx, 1
    mov rcx, 0
    cmp rbx,rcx
    jnz print
    
    xor rax, rax
    ret 
    
print:
    PRINT_STRING msg 
    NEWLINE 
    xor rax, rax 
    ret 
```
**Step 3** 

Repeat steps from the previous lab all the way to ‘ret’. 

> Add BPs: 16 and 19. You should not hit 19!

**Step 4**

Record your findings and notes in the Lab Notes document. 

### Part 2

[Replace JNZ with JZ](https://) 

Repeat all steps and record findings. 

> Add BPs: 16 and 19. You should hit 19!

## 1.7 Push and Pop

**Step 1**

Make sure the assembler is set to NASM before you start this lab. 

**Step 2**

Write code in the IDE that demonstrates PUSH and POP operations (you can copy the code provided below)
```
%include "io64.inc"

section .data
var dq 100
    
section .text
global main

main:
    mov rbp, rsp
    
    mov rbx, 200
    push rbx
    push qword[var]
    
    pop rcx
    pop qword[var] 
    
    xor rax, rax
    ret 
```
**Step 3**

Add the variable var to the watch list:

![](https://malienist.github.io/TRAIN/images/labs-images/1.2-1.6-1.png)

Now repeat steps from the previous lab (examine the values at BPs) all the way to ```ret```. 

> Add BPs: 13, 14, 16, 17 and 19. 

**Step 4** (Optional)

Record your findings and notes in the Lab Notes document. 



**You have now completed the lab.**