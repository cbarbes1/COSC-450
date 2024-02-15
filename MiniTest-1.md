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
    - Clusters can provide a way to do high performance computing
    - To take advantage of this system, The program must be written correctly in the fashion that works best for clustering
## Multiprogramming
- Hold several processes in memory at the same time, provide concurrency for processes
- The operating system (short term scheduler) picks one of process in ready queue and let it use an available CPU to execute its job
- Eventaully, the process may have to wait for some task, such as an I/O operation, to complete
- Multiprogramming increases CPU utilization, as well as keeping users satisfied, by organizing programs so that the cpu always has one to execute
- Multitasking is a logica extension of multiprogramming
- Multitasking is allowing a user to perform more than one computer task at a time
- The operating system is able to keep track of where you are in these tasks and go from one to the other without losing information
- is it possible without multiprogramming?
## Dual - Mode and Multimode operation
- Since the os and its users share resources, an OS must ensure that malicious program cannot cause other programs to execute incorrectly
- In order to ensure the proper execution of the system, must distinguish between  the execution of OS code and user code (kernel mode and user mode)
- The approach taken by most computer systems is to provide hardware support that allows differentiation among various modes of execution
- A bit, called the mode bit, is added to the hardware of the computer indicate the current mode: kernel(0) or user(1)
- When a process request a service via system call, the system must change mode from user to kernel mode to fulfill the request
- The dual mode of operation provides us with the means for protecting the operating system from errant users (or hackers)
- This protection can be accomplished by designating some of the machine instructions (may cause harm as privileged instructions) to be executed only in kernel mode
- The concept of modes can be extended to more than two modes
- ex) intel processors have four seperate protection rings
    - Ring 0: kernel mode
    - Ring 1 and 2: used for various OS service rarely used
    - Ring 3: user mode
- System calls provide the means for a user program to ask the operating system to perform tasks reserved for the operating system  on the user programs behalf
- A system call usually is like a trap to a specific location in the interrupt vector. can be executed by a generic trap instruction, although some systems have a specific system call instruction to invoke a system call
- WHen a system call is called, control passes through the interrupt vector to a service routine in the operating system, the module bit is set to kernel mode.
- The system call service routine is a part of the operating system. The kernel examines the interrupting instruction to determine what system call has occurred: a parameter indicates what type of service the user program is requesting
- The kernel verifies that the parameters are correct and legal, executes the request, and returns control to the instruction following the system call
- System Call
    - Step 1~ 3: push parameters onto the stack
    - Step 4: actual function call
    - Step 5: fetch read instruction to IR in CPU
    - Step 6: (trap) change mode to kernel
    - Step 7: dispatch system call service routine (or handler) number (read)
    - Step 8: run system call service routine (or handler)
    - step 9, 10: changge mode to user result might be saved in a register
    - Step 11: clear stack by increment stack pointer
- Timer
    - Operating System maintain control over the cpu
    - A process cannot keep cpu as it need. Cpu is always assigned to a process with timer.
    - A timer can be set to interrupt the computer after a specified period. The period may be fixed or variable
    - When time period is expired before finishing its job, the process must wait for CPU time in ready queue
- OS as a Resource Manager
    - Process (& thread) management
    - Memory Management
    - File Managements
    - Input / Output System Management
    - Deadlock Managements
    - Cache Management
- **Process Management**
    - The operating System is responsible for the following activities for process management:
        - Creating and deleting both user and system processes
        - Scheduling Processes (and threads) on the CPUs
        - Suspending and Resuming processes (and threads)
        - Providing Mechanisms for process synchronization ( semaphore, mutex, conditional variables,..)
        - Providing mechanisms for process communication (PIPE, Message Queue, Shared Memory, FIFO, Socket, ..)
- **Memory Management**
    - For a program to be executed, it must be mapped to absolute addresses and loaded into memory
    - As the program executes, it accesses program instructions and data from memory by generating these absolute addresses
    - The CPU reads instruction from main memory during the instruction-fetch cycle and both reads and writes data from main memory during the data-fetch cycle (on a von neumann architure).
    - Eventually, Thre program terminates, its memory space is declared available, and the next program can be loaded and executed.
    - The operating system is responsible for the following activities for memory management:
        - Keeping track of which parts of memory are currently being used and which process is using them (for supporting multiprogramming)
        - Allocating and deallocating memory space as needed
        - Deciding which processes (or parts of processes) and data to move into and out of memory(virtual memory)
     
- **File Management**
    - OPerating system provides a uniform, logical view of information storage for user to save a file. A file is a collection of related information defined by its creator.
    - The operating system implements the abstract concept of a file by managing mass storage media and the devices that control them
    - In addition, files are normally organized into directories to make them easier to use
    - If a system support mulit-user, OS need control which user may access a file and how that user may access it( for example, read, write, append).
    - The operating system is responsible for the following activities for file management
        - Creating and Deleting Files
        - Creating and Deleting directories to organize files
        - Supporting primitives for file manip
            - Read, write, open, lseek
        - Mapping files onto mass storage (HDD, SSD, USB, Tape)
        - Backing up files on stable (nonvolatile) storage media
- **Mass-Storage Management**
    - Modern Computer System use multiple types of secondary storages (HDD, SSD, USB, Magnetic Tape)
    - The operating system is responsible for the folling activities for secondary storage management
        - Mounting and Unmounting
        - Free-space management
        - Storage Allocation
        - Disk Scheduling (in HDD)
        - Partitioning
        - Protections
- **Cache Management**
    - Cache is a hardware or software component that stores data which might be used again soon. the data stored in a cache might be the result of an earlier computation of a copy of data stored elsewhere
    - A cache hit occurs when the requested data can be found in a cache, while a cache miss occurs when it cannot.
    - Because caches have linited size, cahce managemment is an important design problem
    - Careful selection of the cache size and of a replacement policy (with cache miss) can result in greatly increased performance.
    - The movement of information between levels of a storage hierarchy may be either explicit or implicit, depending on the hardware design and the controlling operating system software
        - For instance, data transfer from cache to CPU and registers is usually a hardware function, with no operating system intervention
        - Data transfer of data from disk to memory is usually controlled by the operating system
- **Deadlock Management**
    - Deadlocks between processes happen from limited number of resources which must be shared between processes
    - Processes are sharing resources for finishing their job
    - Some processes might need more than one resources hold to finish its job ( copy data fromm disk to usb drive)
    - Resources Allocation Graph
        - There are two processes P1 and P2. There are two resources R1 and R2
        - Both P1 and P2 need resources R1 and R2 to finish their job
    ```mermaid
        graph TD;
            P1-->R1;
            P2-->R2;
            R3-->P3;
            R4-->P4;
            R5-->P5;
            R6-->P6;
            P5-->R6;
            P6-->R5;
    ```
    - Ex)
    - There are two processes P1, P2 working on their job
    - There are one CD recorder, and CD ROM, P1 and P2 need two resources to finish its job
        1. T1: P1 request CCD ROM and granted
        2. T1: P2 request CD recorder and granted
        3. T2: P1 request CD recorder without release CD ROM. Since CD recorder is hold by P2. P1 be waiting state (block state) waiting for CD recorder leased by P2
        4. T3: P2 request CD ROM but it is not released by P1, P2 go to waiting state(block state)
        5. P1 and P2 will stay in block state forever!
    - Four Strategies fro dealing with Deadlock
        1. Just ignore
        2. Detection and recover (detection algorithm)
        3. Dynamic Avoidance by careful allocation (bankers algorithm)
        4. Provention - by negating one of the four conditions necessary for deadlock
            1. Mutual exclusion
            2. Circular Wait
            3. Hold and Wait
            4. No Preemptive
- **Input / Output**
- - Operating System manages all kinds of I/O devices such as keyboards, monitors, printers, and so on
    - Operating System has I/O subsystems for managing I/O devices
    - I/O subsystems consist of
        - A memory-management components - Buffering, Spooling and Caching
        - General Device Drivers interface
        - Drivers fro specific hardware
        - Processor for specific hardware
    - Operating System Controls all I/O devices by
        - Issue commands to devices (read/Write)
        - Catch interrupts from devices (when device is ready to read or write)
        - OS also provide interface between the devices and the rest of the system
- **Structure of Operating System**
    - Operating system structure
        - Monolithic
            - Written collection of procedures, each can call any other ones whenever it needs it
            - Each procedure in the system has a well defined interface in terms of parameters and results and each on eis free to call any other one, if the latter provides some useful computation that the former needs
            - possible to have structure for a monolithic system
            - Possible Structure for a monolithic system
                - Main program - invoke service functions
                - Service functions - Carry out the system calls
                - Utility Functions - helps service functions
            - ```mermaid
              graph TD;
                  MP --> SP1;
                  MP --> SP2;
                  MP --> SP3;
                  MP --> SP4;
                  MP --> SP5;
                  SP1-->UP1;
                  SP1-->UP2;
                  SP2-->UP2;
                  SP2-->UP3;
                  SP3-->UP4;
                  SP3-->UP5;
              ```
        - Layered system
             - Operating System is divided into several layers and each layer works for different rule.
                  - Layer 0 - Process management
                  - Layer 1 - memory management
                  - Layer 2 - Inter-process communication
                  - Layer 3 - Input / Output Management
                  - Layer 4 - Deadlock Management
                  - Layer 5 - User Program
                  - Layer 6 - System operator process
        - Microkernels
            - With the layered approach, the designers have a choice where to draw the kernel-user boundary
            - Traditionally, all the layers went in the kernel, but it is not necessary since one bug in kernel might cause entire system down
            - Various researchers studied the number of bugs (logical) per 1000 lines  of code
            - About 5 million lines of codes for layered kernel likely to contain 10000 to 50000 kernel bugs
            - Not all of bugs are fatal
            - The basic idea is this: To achieve high reliability by splitting the operating system up into small well-defined module
            - only one of module (micro kernels) run in kernel mode and the rest run as users mode
            - Ex) I/O device driver becomes part of OS which might cause system down
                - A bug in the audio driver will cause the sound to be garbled or stop, but not crash the computer
        - Virtual Machine
            - Virtual machine monitor(hypervisor) runs on the bare hardware and does multiprogramming, by providing several virtual machines..
            - Each virtual machines are exact copies of the bare hardware, including kernel/user
        - Client-Server Module
        - ExoKernels
