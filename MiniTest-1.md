# Mini Test 1
## Lecture Note 1
### Operating System
`A protected software provided interface between hardware and software`

*Macroscopic View* - Processor, Memory, io devices
Physical Devices - Chips, wires, etc
Micro architecture - groups of physical devices that form functional units
Machine Language - Execute some set of instructions
**Von Neumann Bottleneck** - The processor and memory are seperate. since the speed of transfer is slower than calculation speed there is a bottleneck. This would be a throughput limitations. Throughput is how much data can be transferred in a certain amount of time.

The Microprocessor's (CPU) main task is execute instructions.
The instruction cycle is needed to understand the function and operation of the microprocessor which is controlled by the os

#### Fetch Cycle
1. Reading the address of the instruction in (PC) to be executed from the memory
2. Loading it into the instruction register (IR)
3. Program Counter register (PC) is modified to point at the next valid instruction
#### Execute cycle
1. The contents of the IR are decoded and executed
2. The execution may result in a variety of actions depending on the type of instruction.
3. It may be self contained instruction, or it can involve interaction with memory and the ALU
#### What is an operating system?
We consider os as 
- an extended machine (computer users pov)
    - op is part of computer system (extended machine)
    - users can use the hardware without knowing messy detail.
- a resource manager (developer's pov)
    - computer consist of CPU, RAM, and I/O devices
    - Operating system manages these resources to implement app software through process management, memory management, file management, I/O management, and Deadlock Management.
**A computer system belongs to one of generation based on what technology is used to build the system.**
- Vacuum tubes
- Transistors
- IC (integrated circuit) 
- LSI or VLSI ( large scaled integrated circuit, very large scaled integrated circuit)
#### Multi-Programming
- Multiple jobs (processes) are loaded into RAM and run concurrently.
- Once CPU become available, one of job (from the ready queue) are selected by short term scheduler, load its current status (from its process table) to CPU and start to run.
- OS need keep each job's current status in process table (or called process control block)
#### Spooling
- Spooling is a kind of buffering mechanism or a process in which data is temporarily held as a file to be used and executed by a device, program or the system.
- Example: Network Printers
    - The process in which info to be printed is stored temporarily in a file, the printing being carried out later.
    - used to prevent slow printer from holding up the system and enable printer to be shared.
#### Operating System ZOO
- Mainframe op
- Server op
- Multiprocessor op
- Personal Computer op
- Real-time op
- Embedded OP
- Smart car op
- smart phone op
## Lecture Note 2
### Computer System Architecture
#### CPU
- The CPU is the brain of the computer
- each cpu has a specific instruction set that is used to execute each instruction.
- Since accessing RAM to get an instruction or data takes much longer than executing an instruction ( Fetch cycle is slower than execute cycle), all cpu contains set of registers and cache to hold instructions, key variables and temporary result.
     - PC (program counter), IR (instruction register), Data register, Stack pointer...
- It fetches instructions from memory and execute them.
- Basic instruction cycle executed by CPU
    1. Fetch a data (instruction or data) from memory to a register
    2. Decode the instruction
    3. Execute the instruction
- The instruction cycle is repeated until the program finishes
- **A CPU is composed with several components**
    - ALU (arithmetic logic unit)
    - Control unit 
    - Cache (depends on design, it might be outside)
    - Registers
        - General Registers
            - Instruction registers
            - Data Registers 
        -