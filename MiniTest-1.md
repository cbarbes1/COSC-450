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
---
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
        - Program Counter(PC)\- save address of next instruction (virtual address)
        - Stack pointers - address of top of stack for currently running process 
        - Program status word(psw) \- save control information for each process (condition bits, cpu priority, the mode..)
- The operating system must know the content of each register for a process. (a process works for different jobs)
- When a process stop running by changing state (three states: running, ready, block) from running to ready or running to block, os saves content of each register (snapshot of contents of cpu) for the process in process table (or process control block) which need to be used to finish its job
- A CPU performance can be improved by using pipelined design for fetch, decode and execute process. since fetching data takes more than execution
- A CPU may have multiple cores. A CPU chip with multiple calculation units.
---
## Interrupts
- WHen a I/O device is ready to recieve or send data through bus, it interrupts operating system by sending signal
     - IO operation, the device driver load a instruction (read or write) to device controllers instruction register.
     - Controller start transfer of data from device to its local buffer (read: transfer data from bus to local buffer)
     - once complete check any error then the device controller informs the device driver that ready to transfer.
     - then device driver gives control to other parts of op
- Hardware interrupt any time through signal to CPU by the system bus
- Key part of Operating systems and hardware interact
- when cpu interrupted, stops current task and transfers execution to fixed location that the service routine for interrupt is located
- Interrupt service routine executes, when done, cpu resume interrupted task
- operating system maintain a table of pointers (interrupt vector) in low memory  to hold address of interrupt service routine
- cpu hardware has Interrupt request line that senses after executing every CPU instruction
- when cpu detects that a controller has triggered a signal on the line it reads the interrupt number and jumpts to the interrupt handler routine, it uses the interrupt number as an index in the interrupt vector
- A interrupt handler starts execution and might create output and return the cpu to the exection state prior to the interrupt
    1. device controller raised an interrupt by asserting a signal on the interrupt request line
    2. the cpu catches the interrupt and dispatches it to the interrrupt handler
    3. the interrupt handler clears the interrupt by servicing the device
    4. return the state prior to interrupt
- Cpus have 2 interrupt request lines 
    - non-maskable interrupt line - reserved for event such as unrecoverable hardware error
    - maskable interupt line 0 used by device controllers to request service
- intel processor event-vector table
     - starting section for hardware error conditions
     - end section for device generated interrupts

- TO wrap, interrupts are used throughout modern operating systems to handle asynchronous events
- Device controllers and hardware faults raise interrupts
- to prioritize work there is interrupt priorities.
- efficient interrupt handling is needed for good system performance, time-sensitive
---
## Memory
