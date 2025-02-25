Download Link : https://programming.engineering/product/systems-and-networks-homework-2-getting-started-with-the-lc-22/

# CS-2200-Systems-and-Networks-Homework-2-Getting-Started-with-the-LC-22-
Systems and Networks Homework 2 (Getting Started with the LC-22)



    Problem 1: Getting Started with the LC-22

In this homework, you will be using the LC-22 ISA to complete a Tower of Hanoi move-counting function. Before you begin, you should familiarize yourself with the available instructions, the register conventions and the calling convention of LC-22. Details can be found in the section, Appendix A: LC-22 Instruction Set Architecture, at the end of this document.

The assembly folder contains several tools for you to use:

    assembler.py: a basic assembler that can take your assembly code and convert it into binary instruc-tions for the LC-22.

    lc22.py: the ISA definition file for the assembler, which tells assembler.py the instructions supported by the LC-22 and their formats.

    lc22-sim.py: A simulator of the LC-22 machine. The simulator reads binary instructions and emulates the LC-22 machine, letting you single-step through instructions and check their results.

To learn how to run these tools, see the README.md file in theassembly directory.

Before you begin work on the second problem of the homework, try writing a simple program for the LC-22 architecture. This should help you familiarize yourself with the available instructions.

We have provided a template, mod.s, for you to use for this purpose. Try writing a program that performs the mod operation on the two provided arguments. A correct implementation will result in a value of 2.

You can use the following C code snippet as a guide to implement this function:

int mod ( int a , int b ) {

int x = a ;

while ( x >= b ) {

x = x – b ;

}

return x ;

}

There is no turn-in for this portion of the assignment, but it is recommended that you attempt it in order to familiarize yourself with the ISA.

Homework 2 CS 2200 – Systems and Networks

    Problem 2: Tower of Hanoi

For this problem, you will be implementing the missing portions of the program that calculates the minimum number of moves to solve the Tower of Hanoi problem for n disks.

Tower of Hanoi involves three vertical rods and a set of varying sized disks, which can slide onto any rod. The disks are initially stacked on one of the rods in ascending order of size, with the largest disk on the bottom and the smallest on top, thus making a conical shape. The objective of this puzzle is to migrate the tower of disks completely to another rod, under the rule that only individual disks may be moved at once, and no disks may be placed on smaller disks.

You will be finishing a recursive implementation of the Tower of Hanoi minimal moves calculator program that follows the LC-22 calling convention. Recursive functions always obtain a return address through the function call and return to the callee using the return address.

You must use the stack pointer ($sp) and frame pointer ($fp) registers as described in the textbook and lecture slides.

Here is the C code for the Tower of Hanoi minimal moves calculator you have been provided:

int m i n i m u m H a n o i ( int n ) {

if ( n == 1)

return 1;

else

return (2 * m i n i m u m H a n o i ( n – 1) ) + 1;

}

Note that this C code is just to help your understanding and does not need to be exactly followed. However, your assembly code implementation should meet all of the given conditions in the description.

Open hanoi.s file in the assembly directory. This file contains an implementation of the Tower of Hanoi minimal moves calculator program that is missing significant portions of the calling convention. Near the bottom of the hanoi.s we have provided multiple numbers that you can use to test your homework. They are located at labels testNumDisks1, testNumDisks2, testNumDisks3. Be sure to use these provided integers by loading them from the labels into registers. None of the numbers provided and tested will be lower than 1.

Complete the program by implementing the various missing portions of the LC-22 calling convention. Each location where you need to implement a portion of the calling convention is marked with a TODO label as well as a short hint describing the portion of the calling convention you should be implementing.

Please note that we will be testing your implementation for multiple different instances, so please do not attempt to hardcode your solutions.

    Problem 3: Short Answer

Please answer the following question in the file namedanswers.txt:

    The LC-22 instruction set contains an instruction called jalr that is used to jump to a location while saving a return address. However, this functionality could be emulated using a combination of other instructions available in the ISA. Describe a sequence of other instructions in the LC-22 ISA that you may use to accomplish the functionality of jalr.

For the purpose of this question, you may assume the target address is represented with the label <target> which can be accessed using the 20 bits reserved for an offset or immediate value in the LC-22 ISA.

Homework 2 CS 2200 – Systems and Networks

    Deliverables

        hanoi.s: your assembly code from Section 2

        answers.txt: your answer to the problem from Section 3 Submit these files toGradescope before the assignment deadline.

The TAs should be able to type python assembler.py -i lc22 –sym hanoi.s and then python lc22-sim.py hanoi.bin to run your code. If you cannot do this with your submission, then you have done something wrong.

Homework 2 CS 2200 – Systems and Networks

    Appendix A: LC-22 Instruction Set Architecture

The LC-22 is a simple, yet capable computer architecture. The LC-22 combines attributes of both ARM and the LC-2200 ISA defined in the Ramachandran & Leahy textbook for CS 2200.

The LC-22 is a word-addressable, 32-bit computer. All addresses refer to words, i.e. the first word (four bytes) in memory occupies address 0x0, the second word, 0x1, etc.

All memory addresses are truncated to 16 bits on access, discarding the 16 most significant bits if the address was stored in a 32-bit register. This provides roughly 64 KB of addressable memory.

5.1 Registers

The LC-22 has 16 general-purpose registers. While there are no hardware-enforced restraints on the uses of these registers, your code is expected to follow the conventions outlined below.

Table 1: Registers and their Uses

            Register Number
            	

            Name
            	

            Use
            	

            Callee Save?
            			

            0
            	

            $zero
            	

            Always Zero
            	

            NA

            1
            	

            $at
            	

            Assembler/Target Address
            	

            NA

            2
            	

            $v0
            	

            Return Value
            	

            No

            3
            	

            $a0
            	

            Argument 1
            	

            No

            4
            	

            $a1
            	

            Argument 2
            	

            No

            5
            	

            $a2
            	

            Argument 3
            	

            No

            6
            	

            $t0
            	

            Temporary Variable
            	

            No

            7
            	

            $t1
            	

            Temporary Variable
            	

            No

            8
            	

            $t2
            	

            Temporary Variable
            	

            No

            9
            	

            $s0
            	

            Saved Register
            	

            Yes

            10
            	

            $s1
            	

            Saved Register
            	

            Yes

            11
            	

            $s2
            	

            Saved Register
            	

            Yes

            12
            	

            $k0
            	

            Reserved for OS and Traps
            	

            NA

            13
            	

            $sp
            	

            Stack Pointer
            	

            No

            14
            	

            $fp
            	

            Frame Pointer
            	

            Yes

            15
            	

            $ra
            	

            Return Address
            	

            No

    Register 0 is always read as zero. Any values written to it are discarded. Note: for the purposes of this project, you must implement the zero register. Regardless of what is written to this register, it should always output zero.

    Register 1 is used to hold the target address of a jump. It may also be used by pseudo-instructions generated by the assembler.

    Register 2 is where you should store any returned value from a subroutine call.

    Registers 3 – 5 are used to store function/subroutine arguments. Note: registers 2 through 8 should be placed on the stack if the caller wants to retain those values. These registers are fair game for the callee (subroutine) to trash.

    Registers 6 – 8 are designated for temporary variables. The caller must save these registers if they want these values to be retained.

    Registers 9 – 11 are saved registers. The caller may assume that these registers are never tampered with by the subroutine. If the subroutine needs these registers, then it should place them on the stack and restore them before they jump back to the caller.

    Register 12 is reserved for handling interrupts. While it should be implemented, it otherwise will not have any special use on this assignment.

Homework 2 CS 2200 – Systems and Networks

    Register 13 is the everchanging top of the stack; it keeps track of the top of the activation record for a subroutine.

    Register 14 is the anchor point of the activation frame. It is used to point to the first address on the activation record for the currently executing process.

    Register 15 is used to store the address a subroutine should return to when it is finished executing.

5.2 Instruction Overview

The LC-22 supports a variety of instruction forms, only a few of which we will use for this project. The instructions we will implement in this project are summarized below.

Table 2: LC-22 Instruction Set

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

            ADD
            	

            0000
            	

            DR
            	

            SR1
            	

            unused
            	

            SR2

            NAND
            					

            0001
            	

            DR
            	

            SR1
            	

            unused
            	

            SR2

            ADDI
            					

            0010
            	

            DR
            	

            SR1
            	

            immval20
            	

            LW
            					

            0011
            	

            DR
            	

            BaseR
            	

            offset20
            	

            SW
            					

            0100
            	

            SR
            	

            BaseR
            	

            offset20
            	

            BR
            					

            0101
            	

            unused
            	

            offset20
            	

            JALR
            					

            0110
            	

            RA
            	

            AT
            	

            unused
            	

            HALT
            					

            0111
            			

            unused
            	

            BLT
            					

            1000
            	

            SR1
            	

            SR2
            	

            offset20
            	

            BGT
            					

            1001
            	

            SR1
            	

            SR2
            	

            offset20
            	

            LEA
            					

            1010
            	

            DR
            	

            unused
            	

            PCoffset20
            	
            					

5.2.1 Conditional Branching

Branching in the LC-22 ISA is a bit different than usual. We have a set of branching instructions including BR, an unconditional branch, as well as BLT and BGT, which offer the ability to branch upon a certain condition being met. The BLT and BGT instructions use comparison operators, comparing the values of two source registers. If the comparisons are true (for example, with the BGT instruction, if SR1 > SR2), then we will branch to the target destination of incrementedPC + offset20.

Note: The conditional branch instructions make use of the BrSel signal. Think about ways that you can use this signal to implement conditional logic.

Homework 2 CS 2200 – Systems and Networks

5.3 Detailed Instruction Reference

5.3.1
	

ADD
										

Assembler Syntax
										

ADD
	

DR, SR1, SR2
										

Encoding
										

31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10
	

9
	

8
	

7
	

6
	

5
	

4
	

3
	

2
	

1
	

0
			
			

Homework 2
	

CS 2200 – Systems and Networks
	

													

5.3.3
	

ADDI
												

Assembler Syntax
												

ADDI
	

DR, SR1, immval20
												

Encoding
												

31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10
	

9
	

8
	

7
	

6
	

5
	

4
	

3
	

2
	

1
	

0
	

Homework 2
	

CS 2200 – Systems and Networks
	

													

5.3.5
	

SW
												

Assembler Syntax
												

SW
	

SR, offset20(BaseR)
												

Encoding
												

31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10
	

9
	

8
	

7
	

6
	

5
	

4
	

3
	

2
	

1
	

0
	

Homework 2 CS 2200 – Systems and Networks

5.3.7 JALR

Assembler Syntax

JALR RA, AT

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Homework 2 CS 2200 – Systems and Networks

5.3.10 BGT

Assembler Syntax

BGT SR1, SR2, offset20

Encoding

31302928272625242322212019181716151413121110 9 8 7 6 5 4 3 2 1 0

Operation

DR = PC + SEXT(PCoffset20);

Description

An address is computed by sign-extending bits [19:0] to 32 bits and adding this result to the incremented PC (address of instruction + 1). It then stores the computed address into register DR.
