# Mini Test 2
## The Process
- A program becomes a process when executable file is loaded into memory. A process is a program in execution.
- When a program start to run, OS keep its status in a process table (process control block) until its termination
- The memory layout of a process is typically divided into four sections
    - Text Section - The executable code (fixed)
    - Data Section - Global and static variables, (fixed)
    - Heap - used for dynamic memory allocation (change size during execution)
    - Stack Section - Temporary data storage for local variables when a function is called ( function parameters, return addresses, and local varibles) ( change size during exection)
- The stack and heap grow toward one another, the operating system must ensure they do not overlap one another
- Just now we assume that there is  only one CPU (with single core) in our system.
- Multiprogramming - several jobs are loaded in memory, operating system simulate Pseudo Parallelism (virtual)
- OS scheduling the CPU times for processes by switches from one process to another based on the scheduling algorithm and process state(by short-term scheduler).
- We can consider processes as two different point of view.
    - Real Model - Multiprogramming (processes are sharing resources)
    - Conceptual (Virtual) Model - each process has its own virtual CPU (ALU, PC, registers, stack pointer) and RAM
    - Check the following Concept
        - Virtual Machine - each os run on its own Memory
        - Virtual Memory - Each process has its own memory
        - Virtual Process Model - each process run on its  own machine 
## The Process Model
## The Process Creation
## Process Termination
## Process States
## Process Table (Process Control Block)
## Process with Multiple-Threads
## Process Scheduling 
### Scheduling Queues
## CPU Scheduling 
## Context Switch
## Process Creation in Linux
## Process Termination in Linux
## Android Process Hierarchy
