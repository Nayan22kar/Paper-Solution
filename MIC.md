Solutions to Microprocessor Question Papers
This document provides detailed solutions to all questions from six question papers for the "Microprocessor" course (Papers: 21222, 12223, 22232, 23124, 23242, 12425). Each paper is solved comprehensively, including explanations, assembly language programs (ALPs), and text-based diagrams where applicable. The solutions cover 8086 architecture, ALPs, addressing modes, directives, and more.

Question Paper: 21222 (Pages 1–4)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Draw the format of flag register of 8086 microprocessor.
Answer:
15 14 13 12 11 10  9  8  7  6  5  4  3  2  1  0
 -  -  -  - OF DF IF TF SF ZF  - AF  - PF  - CF

(b) Differentiate between TEST and AND instruction.

TEST: Bitwise AND, sets flags, no result stored.
AND: Bitwise AND, stores result, sets flags.

(c) State the function of editor and assembler.

Editor: Creates .asm file (e.g., Notepad).
Assembler: Converts .asm to .obj (e.g., MASM).

(d) Differentiate between NEAR and FAR procedure.



Feature
NEAR
FAR



Segment
Same CS
Different CS


Call Size
2 bytes
4 bytes


(e) Write an ALP to perform addition of two 8-bit numbers.
.MODEL SMALL
.DATA
    NUM1 DB 25H
    NUM2 DB 15H
    SUM  DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, NUM1
    ADD AL, NUM2
    MOV SUM, AL
    MOV AH, 4CH
    INT 21H
END

(f) Describe immediate addressing mode with example.

Immediate: Operand is a constant.MOV AX, 1234H



(g) Describe the function of DAA instruction.

DAA: Adjusts AL for BCD after addition.ADD AL, 09H
DAA



Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) Describe the following assembler directives used for procedure: PROC, ENDP, NEAR, FAR.

PROC: Starts procedure.
ENDP: Ends procedure.
NEAR: Same segment.
FAR: Different segment.

(b) Describe the function of the following pins of 8086: BHE, ALE, READY, RESET.

BHE: Enables high byte transfer.
ALE: Latches address.
READY: Inserts wait states.
RESET: Resets CPU.

(c) Describe any four assembler directives with example.

DB: NUM DB 25H
DW: DATA DW 1234H
EQU: SIZE EQU 10
SEGMENT: CODE SEGMENT

(d) Describe the function of DAS instruction with example.

DAS: Adjusts AL for BCD after subtraction.MOV AL, 47H
SUB AL, 29H
DAS



Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Describe memory segmentation in 8086.

Physical Address = (Segment × 16) + Offset.CS: 1234H << 4 = 12340H
IP:         + 5678H
Physical Address: 179B8H



(b) Write an ALP to multiply two 16-bit numbers.
.MODEL SMALL
.DATA
    NUM1 DW 1234H
    NUM2 DW 5678H
    RESULT DD ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM1
    MUL NUM2
    MOV WORD PTR RESULT, AX
    MOV WORD PTR RESULT+2, DX
    MOV AH, 4CH
    INT 21H
END

(c) Write an ALP to count odd numbers in an array of 10 numbers.
.MODEL SMALL
.DATA
    ARRAY DB 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    COUNT DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CX, 10
NEXT:
    MOV AL, [SI]
    TEST AL, 1
    JZ SKIP
    INC COUNT
SKIP:
    INC SI
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

(d) Using macro write an ALP to perform division of 32-bit number by 16-bit number.
.MODEL SMALL
.MACRO DIV_32_16 NUM_L, NUM_H, DIVISOR, QUOT, REM
    MOV AX, NUM_L
    MOV DX, NUM_H
    DIV DIVISOR
    MOV QUOT, AX
    MOV REM, DX
.ENDM
.DATA
    NUM_L DW 3456H
    NUM_H DW 0001H
    DIVISOR DW 0020H
    QUOTIENT DW ?
    REMAINDER DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    DIV_32_16 NUM_L, NUM_H, DIVISOR, QUOTIENT, REMAINDER
    MOV AH, 4CH
    INT 21H
END

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Explain how 20-bit physical address is generated in 8086.

Physical Address = (Segment × 16) + Offset.

(b) Write an ALP to find largest number in an array of 5 numbers.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H
    MAX   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CL, 5
    MOV AL, [SI]
NEXT:
    INC SI
    CMP AL, [SI]
    JAE SKIP
    MOV AL, [SI]
SKIP:
    DEC CL
    JNZ NEXT
    MOV MAX, AL
    MOV AH, 4CH
    INT 21H
END

(c) Write an ALP to count number of zeros in a 16-bit number.
.MODEL SMALL
.DATA
    NUM   DW 0A5A5H
    COUNT DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM
    MOV CX, 16
NEXT:
    ROR AX, 1
    JC ONE
    INC COUNT
ONE:
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

(d) Write an ALP to perform subtraction of two 8-bit BCD numbers.
.MODEL SMALL
.DATA
    NUM1 DB 47H
    NUM2 DB 29H
    DIFF DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, NUM1
    SUB AL, NUM2
    DAS
    MOV DIFF, AL
    MOV AH, 4CH
    INT 21H
END

Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Calculate physical address for given DS=1245H, SI=0A13H, and CS=1357H, IP=0B24H.

DS:SI = 1245H × 10H + 0A13H = 12450H + 0A13H = 12E63H
CS:IP = 1357H × 10H + 0B24H = 13570H + 0B24H = 14094H

(b) Explain program development and debugging steps in assembly language programming.

Write code in .asm using editor.
Assemble to .obj using MASM.
Link to .exe using LINK.
Debug using DEBUG.
Execute on 8086/emulator.

(c) Describe addressing modes with example.

Immediate: MOV AX, 1234H
Register: MOV AX, BX
Direct: MOV AX, [5000H]
Register Indirect: MOV AX, [SI]
Based: MOV AX, [BX + 10H]
Indexed: MOV AX, [SI + 20H]
Based Indexed: MOV AX, [BX + SI + 30H]

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Write an ALP to compare two strings.
.MODEL SMALL
.DATA
    STR1 DB 'HELLO', 0
    STR2 DB 'HELLO', 0
    EQUAL DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, STR1
    LEA DI, STR2
    MOV CX, 6
    CLD
    REPE CMPSB
    JNZ NOT_EQUAL
    MOV EQUAL, 1
NOT_EQUAL:
    MOV AH, 4CH
    INT 21H
END

(b) Explain the following instructions:

MOVSB: Copies byte from DS:SI to ES:DI.
CMPSB: Compares bytes at DS:SI and ES:DI.
LODSB: Loads byte from DS:SI to AL.

(c) Write an ALP to concatenate two strings.
.MODEL SMALL
.DATA
    STR1 DB 'HI', 0
    STR2 DB 'WORLD', 0
    RESULT DB 20 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, STR1
    LEA DI, RESULT
    CLD
COPY1:
    LODSB
    STOSB
    CMP AL, 0
    JNE COPY1
    DEC DI
    LEA SI, STR2
COPY2:
    LODSB
    STOSB
    CMP AL, 0
    JNE COPY2
    MOV AH, 4CH
    INT 21H
END


Question Paper: 12223 (Pages 5–8)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Function of ALE, DT/R pins.

ALE: Latches address from AD0-AD15.
DT/R: High = transmit, low = receive.

(b) Instructions for:
(i) Divide AX by 50H: MOV BL, 50H; DIV BL(ii) Rotate BX left by 4: ROL BX, 4
(c) Directives for procedure.

PROC, ENDP, NEAR, FAR.

(d) Differences between FAR and NEAR procedure.



Feature
NEAR
FAR



Segment
Same
Different


Call Size
2 bytes
4 bytes


(e) Algorithm to sum a series.

Initialize sum = 0, counter = n.
Add number to sum.
Increment pointer, decrement counter.
Repeat until counter = 0.
Store sum.

(f) Use of REP in string instructions.

Repeats string operation CX times.MOV CX, 10
REP MOVSB



(g) Differentiate ROL and RCL.

ROL: Rotates left, MSB to CF/LSB.
RCL: Rotates left through carry.

Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) Procedure, re-entrant, recursive.

Procedure: Reusable code block.
Re-entrant: Safe for interrupts.
Recursive: Calls itself.Main: CALL FACT
FACT: PUSH AX
      CALL FACT
      POP AX
      RET



(b) Memory segmentation in 8086.

Physical Address = (Segment × 16) + Offset.

(c) Directives: DB, EQU, Segment, Assume.

DB: NUM DB 25H
EQU: SIZE EQU 10
Segment: CODE SEGMENT
Assume: ASSUME CS:CODE

(d) Functions of CALL and RET.

CALL: Pushes return address, jumps.
RET: Pops return address.

Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Register organization of 8086.

General: AX, BX, CX, DX.
Pointer: SP, BP, SI, DI.
Segment: CS, DS, SS, ES.
IP, Flags.

(b) ALP to add BCD numbers in array.
.MODEL SMALL
.DATA
    ARRAY DB 12H, 34H, 56H, 78H, 90H, 23H, 45H, 67H, 89H, 01H
    SUM   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CX, 10
    MOV AL, 0
NEXT:
    ADD AL, [SI]
    DAA
    INC SI
    LOOP NEXT
    MOV [SI], AL
    MOV AH, 4CH
    INT 21H
END

(c) Procedure to find factorial.
.MODEL SMALL
.DATA
    NUM   DB 5
    RESULT DW ?
.CODE
FACT PROC NEAR
    CMP AX, 1
    JBE DONE
    PUSH AX
    DEC AX
    CALL FACT
    POP BX
    MUL BX
DONE:
    RET
FACT ENDP
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, NUM
    XOR AH, AH
    CALL FACT
    MOV RESULT, AX
    MOV AH, 4CH
    INT 21H
END

(d) ALP for BCD to Hex conversion.
.MODEL SMALL
.DATA
    BCD_NUM DB 45H
    HEX_NUM DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, BCD_NUM
    MOV BL, AL
    AND AL, 0F0H
    SHR AL, 4
    MOV CL, 10
    MUL CL
    AND BL, 0FH
    ADD AL, BL
    MOV HEX_NUM, AL
    MOV AH, 4CH
    INT 21H
END

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Functional block diagram of 8086.
[BIU]
  |-> [Queue] -> [CS, DS, SS, ES, IP]
  |-> [Address] -> [20-bit Bus]
  |-> [Data Bus]
[EU]
  |-> [ALU] <-> [AX, BX, CX, DX, SI, DI, BP, SP]
  |-> [Flags]

(b) ALP to arrange numbers in ascending order.
.MODEL SMALL
.DATA
    ARRAY DB 24H, 10H, 05H, 17H, 02H
    SIZE  DB 05H
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV CX, SIZE
    DEC CX
OUTER:
    MOV BX, CX
    LEA SI, ARRAY
INNER:
    MOV AL, [SI]
    CMP AL, [SI+1]
    JBE NO_SWAP
    XCHG AL, [SI+1]
    MOV [SI], AL
NO_SWAP:
    INC SI
    DEC BX
    JNZ INNER
    LOOP OUTER
    MOV AH, 4CH
    INT 21H
END

(c) ALP to count 1’s in 16-bit number.
.MODEL SMALL
.DATA
    NUM   DW 0A5A5H
    COUNT DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM
    MOV CX, 16
NEXT:
    ROR AX, 1
    JNC ZERO
    INC COUNT
ZERO:
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

(d) ALP for X = (A + B) * (C + D) using macro.
.MODEL SMALL
.MACRO CALC_X A, B, C, D, RES
    MOV AL, A
    ADD AL, B
    MOV BL, C
    ADD BL, D
    MUL BL
    MOV RES, AL
.ENDM
.DATA
    A DB 2
    B DB 3
    C DB 4
    D DB 5
    X DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    CALC_X A, B, C, D, X
    MOV AH, 4CH
    INT 21H
END

Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Logical, effective address, physical address for CS=2135H, IP=3478H.

Logical: CS:IP.
Effective: Offset from addressing mode.
Physical: 2135H × 10H + 3478H = 247C8H.

(b) Function of assembler, linker, debugger.

Assembler: Converts .asm to .obj.
Linker: Creates .exe.
Debugger: Tests code.

(c) Addressing modes with example.

Immediate: MOV AX, 1234H
Register: MOV AX, BX
Direct: MOV AX, [5000H]
Register Indirect: MOV AX, [SI]
Based: MOV AX, [BX + 10H]
Indexed: MOV AX, [SI + 20H]
Based Indexed: MOV AX, [BX + SI + 30H]

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Branching instructions.

JZ: JZ EQUAL
JNC: JNC NO_CARRY
JMP: JMP LOOP

(b) Instructions: DAA, ADC, XCHG.

DAA: Adjusts BCD.
ADC: Adds with carry.
XCHG: Swaps operands.

(c) ALP to reverse a word in string.
.MODEL SMALL
.DATA
    STR DB 'HELLO', 0
    REV DB 10 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, STR
    LEA DI, REV
    MOV CX, 5
    ADD SI, CX
    DEC SI
    CLD
NEXT:
    MOV AL, [SI]
    STOSB
    DEC SI
    LOOP NEXT
    MOV BYTE PTR [DI], 0
    MOV AH, 4CH
    INT 21H
END


Question Paper: 22232 (Pages 9–12)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Functions of ALE, M/IO pins.

ALE: Latches address.
M/IO: High = memory, low = I/O.

(b) Function of STC, CMC.

STC: Sets CF.
CMC: Toggles CF.

(c) Program development steps.

Write .asm.
Assemble to .obj.
Link to .exe.
Debug.
Execute.

(d) Define macro with syntax.

Macro: Inline code expansion.MACRO_NAME MACRO
    ; Instructions
ENDM



(e) ALP to add two 16-bit numbers.
.MODEL SMALL
.DATA
    NUM1 DW 1234H
    NUM2 DW 5678H
    SUM  DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM1
    ADD AX, NUM2
    MOV SUM, AX
    MOV AH, 4CH
    INT 21H
END

(f) Examples of Immediate, Based Indexed addressing.

Immediate: MOV AX, 1234H, ADD BX, 50H.
Based Indexed: MOV AX, [BX + SI], MOV CX, [BP + DI + 10H].

(g) Use of OF, AF flags.

OF: Set on signed overflow.
AF: Set on nibble carry.

Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) Differentiate NEAR and FAR CALLs.



Feature
NEAR
FAR



Segment
Same
Different


Bytes
2
4


(b) Memory segmentation in 8086.

Physical Address = (Segment × 16) + Offset.

(c) Assembler directives, function of two.

Directives: DB, DW, EQU, SEGMENT.
DB: NUM DB 25H.
EQU: SIZE EQU 10.

(d) Addressing modes for:

MOV CL, 34H: Immediate.
MOV BX, [4100H]: Direct.
MOV DS, AX: Register.
MOV AX, [SI + BX + 04]: Based Indexed.

Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Pipelining in 8086.
Time: T1    T2    T3
BIU:  Fetch1 Fetch2 Fetch3
EU:   --    Exec1  Exec2

(b) ALP for block transfer of 10 numbers.
.MODEL SMALL
.DATA
    SRC DB 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    DST DB 10 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, SRC
    LEA DI, DST
    MOV CX, 10
    CLD
    REP MOVSB
    MOV AH, 4CH
    INT 21H
END

(c) ALP to subtract two BCD numbers.
.MODEL SMALL
.DATA
    NUM1 DB 47H
    NUM2 DB 29H
    DIFF DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, NUM1
    SUB AL, NUM2
    DAS
    MOV DIFF, AL
    MOV AH, 4CH
    INT 21H
END

(d) Re-entrant, recursive procedure.
Main: CALL FACT
FACT: PUSH AX
      CALL FACT
      POP AX
      RET

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Minimum vs. maximum mode.



Feature
Minimum
Maximum



Processors
Single
Multiple


Pins
ALE, DT/R
QS0, S0-S2


(b) ALP for sum of 5 numbers.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 20H, 30H, 40H, 50H
    SUM   DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CX, 5
    XOR AX, AX
NEXT:
    ADD AL, [SI]
    ADC AH, 0
    INC SI
    LOOP NEXT
    MOV SUM, AX
    MOV AH, 4CH
    INT 21H
END

(c) ALP to find largest number.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H, 30H, 15H, 28H, 19H, 11H
    MAX   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CL, 10
    MOV AL, [SI]
NEXT:
    INC SI
    CMP AL, [SI]
    JAE SKIP
    MOV AL, [SI]
SKIP:
    DEC CL
    JNZ NEXT
    MOV MAX, AL
    MOV AH, 4CH
    INT 21H
END

(d) Re-entrant, recursive procedure.

See Q3(d).

Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Logical, effective, physical address for CS=2135H, IP=3478H.

Physical: 2135H × 10H + 3478H = 247C8H.

(b) Directives: DB, DW, EQU, DUP, SEGMENT, END.

DB: NUM DB 25H
DW: DATA DW 1234H
EQU: SIZE EQU 10
DUP: ARRAY DB 5 DUP(0)
SEGMENT: CODE SEGMENT
END: END

(c) Instructions: DAA, AAM.

DAA: Adjusts BCD.
AAM: Adjusts after BCD multiply.

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Instructions for:

Rotate BX right 4: ROR BX, 4
Rotate AX left 2: ROL AX, 2
Add 100H to AX: ADD AX, 100H
Move 1234H to DX: MOV DX, 1234H
Multiply AL by 08H: MOV BL, 08H; MUL BL
Signed division AX/BL: CBW; IDIV BL

(b) Addressing modes with example.

See Q5(c) Paper 21222.

(c) ALP for block transfer with flowchart.
Start -> Initialize DS, ES -> Set SI, DI -> CX=10 -> CLD -> REP MOVSB -> End

.MODEL SMALL
.DATA
    SRC DB 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    DST DB 10 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, SRC
    LEA DI, DST
    MOV CX, 10
    CLD
    REP MOVSB
    MOV AH, 4CH
    INT 21H
END


Question Paper: 23124 (Pages 13–16)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Use of MN/MX, TEST pins.

MN/MX: High = minimum mode, low = maximum.
TEST: Waits for coprocessor.

(b) ALP tools.

Editor, Assembler, Linker, Debugger, Emulator.

(c) Bit manipulation instructions.

SHL, SHR, ROL, ROR.

(d) Use of AAM instruction.
MOV AL, 5
MOV BL, 6
MUL BL
AAM

(e) Advantages of pipelining.

Increased throughput.
Improved performance.

(f) Flag register format.
15 14 13 12 11 10  9  8  7  6  5  4  3  2  1  0
 -  -  -  - OF DF IF TF SF ZF  - AF  - PF  - CF

(g) Procedure definition and syntax.
PROC_NAME PROC NEAR
    RET
PROC_NAME ENDP

Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) Instructions: DAA, CMP, ADC, JNC.

DAA: Adjusts BCD.
CMP: Sets flags.
ADC: Adds with carry.
JNC: Jumps if CF = 0.

(b) Re-entrant, recursive procedure.

See Paper 12223 Q2(a).

(c) Pins: READY, ALE, TEST, DEN.

READY: Wait states.
ALE: Latches address.
TEST: Coprocessor sync.
DEN: Enables data bus.

(d) Model of ALP.
[CODE SEGMENT]
[DATA SEGMENT]
[STACK SEGMENT]

Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Memory segmentation, advantages.

Physical Address = (Segment × 16) + Offset.
Advantages: Large programs, relocation.

(b) ALP for 16-bit BCD addition.
.MODEL SMALL
.DATA
    NUM1 DW 1234H
    NUM2 DW 5678H
    SUM  DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM1
    ADD AX, NUM2
    DAA
    MOV SUM, AX
    MOV AH, 4CH
    INT 21H
END

(c) ALP to find largest number.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H
    MAX   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CL, 5
    MOV AL, [SI]
NEXT:
    INC SI
    CMP AL, [SI]
    JAE SKIP
    MOV AL, [SI]
SKIP:
    DEC CL
    JNZ NEXT
    MOV MAX, AL
    MOV AH, 4CH
    INT 21H
END

(d) CALL and RET instructions.

CALL: Pushes return address.
RET: Pops return address.

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Procedure vs. macros.



Feature
Procedure
Macro



Storage
Single copy
Inline


Execution
Stack
No stack


(b) ALP to find string length.
.MODEL SMALL
.DATA
    STR DB 'HELLO', 0
    LEN DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, STR
    XOR CX, CX
NEXT:
    CMP BYTE PTR [SI], 0
    JE DONE
    INC CX
    INC SI
    JMP NEXT
DONE:
    MOV LEN, CL
    MOV AH, 4CH
    INT 21H
END

(c) Directives: DB, SEGMENT, DUP, EQU.

DB: NUM DB 25H
SEGMENT: DATA SEGMENT
DUP: ARRAY DB 5 DUP(0)
EQU: SIZE EQU 10

(d) ALP to count 1’s in 8-bit number.
.MODEL SMALL
.DATA
    NUM   DB 0A5H
    COUNT DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AL, NUM
    MOV CX, 8
NEXT:
    ROR AL, 1
    JNC ZERO
    INC COUNT
ZERO:
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Logical, effective, physical address for CS=348AH, IP=4214H.

Physical: 348AH × 10H + 4214H = 38AB4H.

(b) Instructions for:

Multiply AL by 05H: MOV BL, 05H; MUL BL
Move 1234H to DS: MOV AX, 1234H; MOV DS, AX
Add AX, BX: ADD AX, BX
Signed division AX/BL: CBW; IDIV BL
Rotate AX left 4 through carry: RCL AX, 4
Load SP with FF00H: MOV SP, FF00H

(c) ALP for string concatenation with flowchart.
Start -> Copy STR1 until null -> Overwrite null -> Copy STR2 -> End

.MODEL SMALL
.DATA
    STR1 DB 'HI', 0
    STR2 DB 'WORLD', 0
    RESULT DB 20 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, STR1
    LEA DI, RESULT
    CLD
COPY1:
    LODSB
    STOSB
    CMP AL, 0
    JNE COPY1
    DEC DI
    LEA SI, STR2
COPY2:
    LODSB
    STOSB
    CMP AL, 0
    JNE COPY2
    MOV AH, 4CH
    INT 21H
END

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Functional block diagram of 8086.

See Q4(a) Paper 12223.

(b) Shift and rotate instructions.

SHL: SHL AX, 2
SHR: SHR AX, 1
SAR: SAR AX, 1
ROL: ROL AX, 1
ROR: ROR AX, 1
RCL: RCL AX, 1

(c) ALP for Z = (P + Q) * (R + S) using macro.
.MODEL SMALL
.MACRO CALC_Z P, Q, R, S, RES
    MOV AL, P
    ADD AL, Q
    MOV BL, R
    ADD BL, S
    MUL BL
    MOV RES, AL
.ENDM
.DATA
    P DB 2
    Q DB 3
    R DB 4
    S DB 5
    Z DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    CALC_Z P, Q, R, S, Z
    MOV AH, 4CH
    INT 21H
END


Question Paper: 23242 (Pages 17–18)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Four features of 8086.

16-bit architecture.
1 MB address space.
Pipelining.
Segmented memory.

(b) Two addressing modes with example.

Immediate: MOV AX, 1234H
Register Indirect: MOV AX, [SI]

(c) Function of assembler.

Converts .asm to .obj.

(d) Define macro with syntax.

See Paper 22232 Q1(d).

(e) Model of ALP.
[CODE SEGMENT]
[DATA SEGMENT]
[STACK SEGMENT]

(f) Four machine control instructions.

HLT, NOP, CLC, STC.

(g) Use of DAA in BCD addition.

Adjusts AL for BCD.

Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) NEAR vs. FAR procedure calls.



Feature
NEAR
FAR



Segment
Same
Different


Bytes
2
4


(b) Flag register format, two flags.

Format: See Paper 23124 Q1(f).
OF: Signed overflow.
ZF: Result zero.

(c) Two assembler directives.

DB: NUM DB 25H
DW: DATA DW 1234H

(d) Addressing modes for:

MUL AL, BL: Register.
MOV DX, 0040H: Immediate.
MOV BX, [SI]: Register Indirect.
MOV AX, [BX][SI]: Based Indexed.

Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Pipelining in 8086.

See Paper 22232 Q3(a).

(b) ALP for 16-bit signed multiplication.
.MODEL SMALL
.DATA
    NUM1 DW 1234H
    NUM2 DW 5678H
    RESULT DD ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM1
    IMUL NUM2
    MOV WORD PTR RESULT, AX
    MOV WORD PTR RESULT+2, DX
    MOV AH, 4CH
    INT 21H
END

(c) ALP to find largest number.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H, 30H, 15H, 28H, 19H, 11H
    MAX   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CL, 10
    MOV AL, [SI]
NEXT:
    INC SI
    CMP AL, [SI]
    JAE SKIP
    MOV AL, [SI]
SKIP:
    DEC CL
    JNZ NEXT
    MOV MAX, AL
    MOV AH, 4CH
    INT 21H
END

(d) ALP for P = X² + Y² using macro.
.MODEL SMALL
.MACRO CALC_P X, Y, RES
    MOV AL, X
    MUL AL
    MOV BX, AX
    MOV AL, Y
    MUL AL
    ADD AX, BX
    MOV RES, AX
.ENDM
.DATA
    X DB 3
    Y DB 4
    P DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    CALC_P X, Y, P
    MOV AH, 4CH
    INT 21H
END

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Functional block diagram of 8086.

See Q4(a) Paper 12223.

(b) ALP to sort in descending order.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H, 30H, 15H, 28H, 19H, 11H
    SIZE  DB 0AH
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV CX, SIZE
    DEC CX
OUTER:
    MOV BX, CX
    LEA SI, ARRAY
INNER:
    MOV AL, [SI]
    CMP AL, [SI+1]
    JAE NO_SWAP
    XCHG AL, [SI+1]
    MOV [SI], AL
NO_SWAP:
    INC SI
    DEC BX
    JNZ INNER
    LOOP OUTER
    MOV AH, 4CH
    INT 21H
END

(c) ALP to check odd/even.
.MODEL SMALL
.DATA
    NUM   DW 1234H
    STATUS DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM
    TEST AX, 1
    JZ EVEN
    MOV STATUS, 1
    JMP DONE
EVEN:
    MOV STATUS, 0
DONE:
    MOV AH, 4CH
    INT 21H
END

(d) ALP for Z = (A + B) * (C + D) using procedure.
.MODEL SMALL
.DATA
    A DB 2
    B DB 3
    C DB 4
    D DB 5
    Z DB ?
.CODE
CALC_Z PROC NEAR
    MOV AL, A
    ADD AL, B
    MOV BL, C
    ADD BL, D
    MUL BL
    MOV Z, AL
    RET
CALC_Z ENDP
    MOV AX, @DATA
    MOV DS, AX
    CALL CALC_Z
    MOV AH, 4CH
    INT 21H
END

Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Physical address for DS=73A2H, SI=3216H; CS=7370H, IP=561EH.

DS:SI = 73A20H + 3216H = 76C36H.
CS:IP = 73700H + 561EH = 78D1EH.

(b) Program development steps.

See Paper 22232 Q1(c).

(c) Instructions for:

Add 100H to AX: ADD AX, 100H
Rotate AX left 2: ROL AX, 2
Signed division AX/BL: CBW; IDIV BL

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Content of BX after:
MOV BX, 2050H
MOV CL, 05H
SHL BX, CL


BX = 2050H << 5 = 40A0H.

(b) Branching instructions.

JZ, JNC, JMP.

(c) ALP to add 5 numbers.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 20H, 30H, 40H, 50H
    SUM   DW ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CX, 5
    XOR AX, AX
NEXT:
    ADD AL, [SI]
    ADC AH, 0
    INC SI
    LOOP NEXT
    MOV SUM, AX
    MOV AH, 4CH
    INT 21H
END


Question Paper: 12425 (Pages 19–22)
Question 1: Attempt any FIVE (10 Marks, 2 marks each)
(a) Four general-purpose registers.

AX, BX, CX, DX.

(b) Function of assembler, linker.

Assembler: Converts .asm to .obj.
Linker: Creates .exe.

(c) Four assembler directives.

DB, DW, EQU, SEGMENT.

(d) Function of TEST instruction.
TEST AL, 01H
JZ EVEN

(e) Algorithm to add 8-bit BCD numbers.

Load first number to AL.
Add second number.
DAA.
Store result.

(f) Immediate addressing mode.
MOV AX, 1234H

(g) Use of DAA, DAS.

DAA: Adjusts BCD addition.
DAS: Adjusts BCD subtraction.

Question 2: Attempt any THREE (12 Marks, 4 marks each)
(a) Flag register format, two flags.

Format: See Paper 23124 Q1(f).
SF: Negative result.
CF: Carry/borrow.

(b) Memory segmentation.

See Paper 21222 Q3(a).

(c) Directives: DB, DW, SEGMENT, END.

DB: NUM DB 25H
DW: DATA DW 1234H
SEGMENT: CODE SEGMENT
END: END

(d) CALL and RET instructions.

See Paper 23124 Q3(d).

Question 3: Attempt any THREE (12 Marks, 4 marks each)
(a) Pipelining in 8086.

See Paper 22232 Q3(a).

(b) ALP to count positive and negative numbers.
.MODEL SMALL
.DATA
    ARRAY DW 10, -5, 20, -15, 0, 30, -25, 40, -10, 50
    SIZE  DW 10
    POS   DW 0
    NEG   DW 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV CX, SIZE
    LEA SI, ARRAY
NEXT:
    MOV AX, [SI]
    CMP AX, 0
    JL NEGATIVE
    JE SKIP
    INC POS
    JMP SKIP
NEGATIVE:
    INC NEG
SKIP:
    ADD SI, 2
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

(c) ALP to find smallest number.
.MODEL SMALL
.DATA
    ARRAY DB 10H, 24H, 02H, 05H, 17H, 30H, 15H, 28H, 19H, 11H
    MIN   DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    LEA SI, ARRAY
    MOV CL, 10
    MOV AL, [SI]
NEXT:
    INC SI
    CMP AL, [SI]
    JBE SKIP
    MOV AL, [SI]
SKIP:
    DEC CL
    JNZ NEXT
    MOV MIN, AL
    MOV AH, 4CH
    INT 21H
END

(d) ALP for 16-bit addition using procedure.
.MODEL SMALL
.DATA
    NUM1 DW 1234H
    NUM2 DW 5678H
    SUM  DW ?
.CODE
ADD_16 PROC NEAR
    MOV AX, NUM1
    ADD AX, NUM2
    MOV SUM, AX
    RET
ADD_16 ENDP
    MOV AX, @DATA
    MOV DS, AX
    CALL ADD_16
    MOV AH, 4CH
    INT 21H
END

Question 4: Attempt any THREE (12 Marks, 4 marks each)
(a) Functional block diagram of 8086.

See Q4(a) Paper 12223.

(b) ALP to count zeros in 16-bit number.
.MODEL SMALL
.DATA
    NUM   DW 0A5A5H
    COUNT DB 0
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV AX, NUM
    MOV CX, 16
NEXT:
    ROR AX, 1
    JC ONE
    INC COUNT
ONE:
    LOOP NEXT
    MOV AH, 4CH
    INT 21H
END

(c) ALP for 8-bit division using macro.
.MODEL SMALL
.MACRO DIV_8 NUM, DIVISOR, QUOT, REM
    MOV AL, NUM
    XOR AH, AH
    DIV DIVISOR
    MOV QUOT, AL
    MOV REM, AH
.ENDM
.DATA
    NUM     DB 50H
    DIVISOR DB 05H
    QUOTIENT DB ?
    REMAINDER DB ?
.CODE
    MOV AX, @DATA
    MOV DS, AX
    DIV_8 NUM, DIVISOR, QUOTIENT, REMAINDER
    MOV AH, 4CH
    INT 21H
END

(d) NEAR vs. FAR procedures.



Feature
NEAR
FAR



Segment
Same
Different


Bytes
2
4


Question 5: Attempt any TWO (12 Marks, 6 marks each)
(a) Logical, effective, physical address for DS=345AH, SI=13DCH.

Physical: 345A0H + 13DCH = 3597CH.

(b) Instructions: ADC, AAM, XCHG.

ADC: ADC AL, 20H
AAM: MUL BL; AAM
XCHG: XCHG AX, BX

(c) Addressing modes with example.

See Q5(c) Paper 21222.

Question 6: Attempt any TWO (12 Marks, 6 marks each)
(a) Shift and rotate instructions.

See Paper 23124 Q6(b).

(b) ALP to arrange array in ascending order with flowchart.
Start -> For i=0 to n-1 -> For j=0 to n-i-1 -> Swap if array[j] > array[j+1] -> End

.MODEL SMALL
.DATA
    ARRAY DB 24H, 10H, 05H, 17H, 02H
    SIZE  DB 05H
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV CX, SIZE
    DEC CX
OUTER:
    MOV BX, CX
    LEA SI, ARRAY
INNER:
    MOV AL, [SI]
    CMP AL, [SI+1]
    JBE NO_SWAP
    XCHG AL, [SI+1]
    MOV [SI], AL
NO_SWAP:
    INC SI
    DEC BX
    JNZ INNER
    LOOP OUTER
    MOV AH, 4CH
    INT 21H
END

(c) ALP to reverse string with flowchart.
Start -> Load string -> Find length -> Copy from end to start -> End

.MODEL SMALL
.DATA
    STR DB 'HELLO', 0
    REV DB 10 DUP(?)
.CODE
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX
    LEA SI, STR
    LEA DI, REV
    MOV CX, 5
    ADD SI, CX
    DEC SI
    CLD
NEXT:
    MOV AL, [SI]
    STOSB
    DEC SI
    LOOP NEXT
    MOV BYTE PTR [DI], 0
    MOV AH, 4CH
    INT 21H
END


