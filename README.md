Download Link: https://assignmentchef.com/product/solved-comp4300-lab-2
<br>
<span class="kksr-muted">Rate this product</span>

This lab develops the first building block for the MIPS datapath, the ALU. It will be combined with the other data path components from later labs, resulting in a complete MIPS by Lab 4.

Instructions

Develop VHDL for the following MIPS component. You should define an architecture for the ALU entity given below. You should test your architecture by developing simulation files for the entity. Your architecture should implement the functionality described in this document. To make the simulation results more readable, we will use a 32-bit datapath (both addr and data buses), not 64 bit.

You should use the types from the package “dlx_types” (available on the files section of Canvas) and the conversion routines from the package “bv_arithmetic” in files bva.vhd, and bva-b.vhd on Canvas. The propagation delay through the ALU should be 5 nanoseconds for any operation.

We will only implement a subset of the MIPS ALU operations. We will not implement any floating point operations. We will not implement any byte or half-word operations. We will only implement the following 32-bit ALU operations.

ADD ADDU ADDI ADDIU SUB SUBI SUBU SUBIU

MUL MULU AND ANDI OR SLT

However, the ALU should take a 4-bit operation input that tells which of sixteen functions to implement. The codes to use are

ADD = 0 (used for ADD, ADDU, ADDI, ADDIU) SUB = 1 (used for SUB, SUBI, SUBU, SUBIU) AND = 2 (used for AND, ANDI)OR =3 (usedforOR)

XOR = 4 (not used) unused = 5SLL = 6 (unused)SRL = 7 (unused)SRA = 8 (unused)SEQ = 9 (unused)SNE = a (unused)SLT = b (used for SLT) SGT = c (unused) unused = d

MUL = e (used for MUL, MULU) DIV = f (unused)

Note that the unsigned and signed versions of an operation have the same function code.

For the codes that I haven’t asked you to implement, return zero as the result of the ALU operation (or for 10 points extra credit, implement all sixteen ALU operations). Googling will tell you semantics (what the instruction does) of each MIPS ALU operation.

There is an additional one-bit input “signed” that is set to 1 if the operation takes signed (32-bit two’s complement) inputs and set to 0 if the operation takes unsigned (32-bit positive binary integer) inputs. If the operation makes no sense when the inputs are signed (i.e. SRL, SLL, AND, OR, XOR), the signed bit is ignored. The ALU also returns a 4-bit condition code, of which the only conditions we will use are

0000 = no error0001 = over/underflowThe entity declaration should look like:

entity alu is

port(operand1, operand2: in dlx_word; operation: in alu_operation_code;

signed: in bit;

result: out dlx_word; error: out error_code); end entity alu;