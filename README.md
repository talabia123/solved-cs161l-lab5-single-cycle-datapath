Download Link: https://assignmentchef.com/product/solved-cs161l-lab5-single-cycle-datapath
<br>
<h1></h1>

In this lab, you will be building a single cycle version of the MIPS datapath. The datapath is composed of many components interconnected. They include an ALU, Registers, Memory, and most importantly the Program Counter (PC). The program counter is the only clocked component within this design and specifies the memory address of the current instruction. Every cycle the PC will be moved to the location of the next instruction. ​<strong>The MIPS architecture is BYTE ADDRESSABLE</strong>​. Remember this when handling the PC, and the memory (which is WORD ADDRESSABLE).

<strong>         </strong>

<h1>Pre-lab</h1>

You will need to submit several tests for your prelab. These must be submitted on ilearn prior to coming to the lab (check online for due dates). These tests will each consist of an ​init.coe​, a corresponding ​.asm​ file and a ​processor_tb.v​ file for each.your test file (​init.coe​ a corresponding ​.asm​ file and a​ processor_tb.v​). The tests you should write are:




<table width="864">

 <tbody>

  <tr>

   <td width="432">individualInstructions.asm lw $v0, X($zero) lw $v1, Y($zero) add $a0, $v0, $v1 addi $a0, $v0, Z… Where X and Y are the address of data you have placed in your .coe file and Z is the immediate you are using. The numbers corresponding to the register numbers are in a table at the end of the document.</td>

   <td width="432">program.asm# An entire program where each instruction# has an effect on the final outcome.# The result will be verified through# inspection of the write_reg_data value during# execution of the last instruction (see below)</td>

  </tr>

  <tr>

   <td width="432">individualInstructions.coe100011 00000 00010 XXXXXXXXXXXXXXXX100011 00000 00011 YYYYYYYYYYYYYYYY000000 00010 00011 00100 00000 000000001000 00010 00100 ZZZZZZZZZZZZZZZZThe spaces are added for clarity and should be removed before running. The X’s, Y’s, and Z’s should also be replaced with there corresponding values.</td>

   <td width="432">program.coeMachine language translation of the program from above.</td>

  </tr>

  <tr>

   <td colspan="2" width="864">See testbench example files below.</td>

  </tr>

 </tbody>

</table>




Your ​init.coe​ should demonstrate that you have read through the lab specifications and understand the goal of this lab. You do not need to begin designing yet, but this testbench will be helpful during the lab while you are designing.

The component connections (shown below) are outlined in the CS161 notes.

<h1>Recommended Iterative Development</h1>

Step 1:

Count up the PC and check that each instruction is correct (​instr_opcode​, ​reg1_addr​, ​reg2_addr​, ​write_reg_addr​) Modules:

<ul>

 <li>Instruction memory* (​v​)</li>

 <li>PC Register (​v​)</li>

 <li>PC adder (optional)</li>

</ul>

Step 2:

Verify that the control signals are still correct on the ​control_unit​ from the previous lab. Verify that you can read values from the registers (at this point they will most likely be all 0’s). You should now be able to get defined values for all debug signals (including reg1_data​, ​reg2_data​, ​write_reg_data​). The data values will most likely be all 0’s since no data manipulation is being done yet.

Step 3:

Add the ​alu_control​ from the previous lab as well as the ALU. There won’t be any change in the debug signals yet, but verify that the ALU output is defined.

Step 4:

Connect the Data Memory* to the ALU and the CPU registers. At this point your data signals (reg1_data, reg2_data, write_reg_data) should be correct for all non-branch instructions.

* Data and Instruction memory are unified for our processor. The CPU_memory module is a dual-port memory unit that allows simultaneous reads of instructions as well as a read/write of data through separate ports. In step 1 you will only have the instruction ports connected, now you’ll connect the rest of them.

Step 5:

Add the modules for the branching hardware. This may involve breaking some connections from step 1 to insert the proper hardware for branching. You should not have any undefined signal before this step, so it shouldn’t be too difficult to trace down any introduced high Z or undefined signals.

<h1>Deliverables</h1>

For the turn-in of this lab, you should have a working ​<strong>single-cycle datapath</strong>​. The ​<em>true</em>​ inputs to the top module (​processor.v​) are only a ​clk​, and ​rst​ signals, although you will need to have the debug signals correctly connected as well. The datapath should be programmed by a “​.coe​” file that holds MIPS assembly instructions. This file is a paramter to the top module, but defaults to

“​init.coe​”.




For this lab, you are not required to build all the datapath components (in black in the image above) but you are required to connect them together in the datapath template provided (​processor.v​). You will be connecting this datapath and your ​alu_control.v and ​control_unit.v​ from Lab 03 in the top-level module (​processor.v​). All of the files can be found in the zip file for this lab. If you need more functionality you will have to build the components yourself. To use the given components you only need to copy the given Verilog files into your project. By default, the architecture’s memory loads data from an “​init.coe”​ file. The programming occurs when the ​rst​ signal is held high. A sample ​init.coe​ file is given but ​<strong>does not fully test the datapath</strong>​. You will have to extend it. For convenience, the assembly for the ​init.coe​ file can be found​ ​in the zip file.  The last instruction of the program is a lw​ to load the final value from memory into register ​$t0​ and is used to verify correct functionality in the test bench (see below). If you add a similar line to your own program it will make testing easier.


