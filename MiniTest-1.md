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
- The CPU can load instructions only from RAM, so any program must first be loaded into memory from the secondary memory to run
- Storage hierarchy
    - Registers in CPU (volatile) valed
    - Cache memory - volatile
    - Main memory volatile - RAM (random access memory)
        - DRAM (dynamic ram) - build with capacitors
        - SRAM (static ram) - build with logic gates
    - secondary memory (non-volatile)
        - HDD(Hard Disk Drive) - rigid metal or glass platters covered with magnetic recording material
        - SSD(solid state drive) - floating point transistors
        - magnetic tapes
        - usb
## Input / output device 
- large amount of op is managing i/o devices, important for reliability, performance of a system 
- the form of interrupt-driven I/O fine for small data but high overhead when used on bulk data movement.
- The solution: DMA (Direct Memory Access). DMA controller can handle I/O independent from the cpu
- DMA capability provided by some computer bus architectures that allows data to be sent directly form an attached device (s.a a disk drive) to the memory
- CPU is freed from involvement with the data transfer, thus speeding up overall computer operation.
- Operating System controls all I/O devices by
    - Issue commands (read/write) to devices
    - Catch interrupts from devices - when devices are ready to send or recieve data.
    - Handle Error
- OS also provide interface between the devices and the rest of the system.
- Most of I/O devices consist of a mechanical component, an electronic component and device driver.
    - **Mechanical Components** - device itself
    - **Electrical Components**
         - Device Controller (adapter)
         - on personal computer, it takes the form of a chip on the parent board or a printed circuit card that can be inserted into a pci exansion slot.
    - **Device Driver (Software)** - THe standard interface between device controller and operating system
## Buses
- The bus in a PC is the common pathway between the CPU and peripheral devices
    - **Parallel buses** use slots on the motherboard and provide multiple lines for data (32 bits, 64 bits) between the cpu and peripheral card. cards plug into the bus inside the cabinet.
    - **Serial Buses** have external ports, and the cable that plugs into them can connect to multiple devices
### Parallel Buses
- Advantage and Disadvantage of parallel buses
    - Advantage - Fast data comm between devices
    - Disadvantage - It supports short distance comm due to crosstalk between the parallel line. cost more due to multi line and more pins
- Parallel Buses:
    - Peripheral Component Interconnect (PCI) - is available in 32 and 64 bit versions, most popular bus architecture
    - Accelerated Graphics Port (AGP) - designed for faster screen display one agp slot on motherboard
### Serial Buses
- **Advantages and disadvantages** of serial buses
    - Disadvantage - it offers slower data communication between device
    - advantages - support long distance comm. it cost less than parallel buses
- **Serial Buses**
    - **Universal serial bus(USB)** - one usb port connects up to 127 peripherals the first version of USB was designed for low speed connections
    - **FireWire (IEEE 1394)** - FireWire connects up to 63 peripheral devices and has been mostly used for digital camera connection
### Single Processor Systems - Single Core one CPU
- Core - the component ro execute instruction and registers for storing data locally.
- special purpose processor - limited instruction set, not run processes, specific for a device?
- Os manage special purpose processor by sending info about their next task and monitor their status Ex) DMA, A processor in the keyboard to convert the key strokes into code to be sent to CPU
### MultiProcessor Systems
- The primary advantage of multiprocessor systems is increased throughtput. we expect to get more work done in less time by increasing the number of processors.
- THe speedup ratio with n processors is less than N, bc of poss extra overhead for communicating between cpu for any calculation
- Def has evolved: multiprocessor now include multicore system, multi cores reside on one chip
- multicore systems can be more efficient than multiple chips with single cores: on chip comm is faster than off chip
- one chip uses significantly less power than multiple single core chips important issue for mobile devices and laptops
- Multiprocessor System Types
- Symmetric multiprocessing (smp) - "One BIG Memory"
    - cpu has own set of registers and cache memory, perform tasks with os functions and user processes. All processors share a common physical memory over the system bus
    - Virtuall all modern os support multicore smp systems
    - adding cpu to a multiprocessor systsem will increase computing power then after too many added then the system bus becomes a bottleneck.
- Non-Uniform memory access (NUMA) "One physical memory shared"
    - Each cpu has own local memory that is accessed via small fast local bus
    - cpu connected to shared system interconnect, so that all cpus share one physical address space
    - The advantage: when a cpu accesses its local memory, not only fast, no contention over the system interconnect
    - A potential drawback: increased latency when a cpu must access remote memory across the system interconnect, creating a possible performance penalty os need careful cpu scheduling and memory management to reduce overhead
- Clusterd Systems
    - Two or more individual systems are connected locally (LAN) an run as one system - loosely coupled
    - Clustering used to provide high availability service- continue even if one fail
    - High availability can be obtained by adding a level of redundancy in the system
        - A layer of cluster software runs on the cluster nodes.
        - Each node can monitor one or more of the other (over the network)
        - if the monitored machin fails, the monitoring machin can take ownership of its storage and restart the applications that were running on the failed machine
    - symmetric clustering - each machine run same thing and monitor neighbor one machine take over the job that fails
    - Asymmetric clustering - one machine is in hot-standby mode to watch the others
    - 
