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
- stack overflow
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
- With the CPU switching back and forth among the processes, a process can hold CPU during its time term
- The time term which assigned to each processes might not be uniform
- The time term for a process might need be calculated based on the types of jobs I/O bounded, CPU bounded or priority (usually CPU bounded job need more cpu time then I/O bounded job
- 
## The Process Creation
- System Initialization - When an OS is booted, several processes (or threads) are created and run concurrently
- A running process create a process by system call - running process request a system call to create one or more new processes - web server example
- A system user create by executing a program - in interactive system, users can start a program by typing a command or click icon
- Initiation of a batch job - mainframe computer
- Unix - system call fork create a new process
- In window - system call CreateProcess create a new process
- Once a child is created, both parent and child have their own distinct address - two process might need inter- process communication (for sharing resources)
## Process Termination
- A process terminate due to one of the following condition
    - Normal Exit - a process finish its job (voluntary)
    - Error Exit - The process itself discovers a fatal error - compiler try to compile a program, there is no such a file (voluntary)
    - Killed by another process - when a deadlock is discovered, OS terminate a process at a time to resolve the deadlock (involuntary)
## Process States
- A process must be in one of state
    - Running state - a process is currently being executed by using CPU
    - Block State (or waiting state) - The process is waiting for some event to occur (such as an I/O completion or reception of signal).
    - Ready State - a process is ready to use a CPU but it not currently available
 
    - 1. Process blocks for input
      2. Short-term scheduler picks a process since CPU become available
      3. A process time out its time term
      4. Input become available
## Process Table (Process Control Block)
- When a process is created, os stores its run time information in a process table (process control block)
- Process table contains information associated with a process
    - Process state - ready, running, or blocked
    - Program Counter - address of next instruction
    - Contents of CPU registers - snapshot of CPU
    - CPU scheduling information - priority, pointer to scheduling queue...
    - Memory Management information - page table, segment table, .. depends on memory method
    - Accounting information - the amount of CPU time used, cpu time limit, job number
    - I/O static information - list of i/o devices allocated, list of open files
## Process with Multiple-Threads
- Most modern operating systems have exteneded the process concept to allow a process to have multiple threads of execution and thus to perform more than one task at a time
- The feature is especially beneficial on multicore systems, where mulitple threads can run in parallel
- A multithread word processor could , for example, assign one thread to manage user input while another thread runs the spell checker
- on systems that support threads, the process table is expanded to include information for each thread.
## Process Scheduling 
### Scheduling Queues
- The objective of multiprogramming is to maximize CPU utilization
- WHen a CPU become available, short-term scheduler (cpu scheduler) select a process from the ready queue and let it use cpu
- Two types of queues which hold pointers to process table for processes in block state and ready state
    - Ready queue - Holds pointers to process tables for processes in ready queue
    - Wait queue - Holds pointers to process table for processes waiting for some events(i/o devices, child termination, interrupt, semaphores)
- This queue is generally stored in a linked list: header contains pointers to the first process table in a list, and each process table includes a pointer field that points to the next process table in the queue
- Once the process is allocated in CPU and is executing, one of several events could occur:
    - The process could issue an io request and then be placed in a I/O wait queue
    - The process could create a new child process and then be placed in a wait queue while it awaits the child’s termination.
    - The process could be removed forcibly from the core, as a result of an interrupt (preemptive scheduler) or having its time slice expire, and be put back in the ready queue.
    - The process tries down semaphore but semaphore value is 0, and be placed in a wait queue for the semaphore.
### CPU Scheduling 
- A process migrates to the ready queue from various wait queues throughout its lifetime
- The role of the short term scheduler (the cpu scheduler) is to select a process that are in the ready queue and allocate an available cpu
## Context Switch
- CPU must be idle
- interrupts cause the operating sytem to change a cpu from its current task and to run a kernel routine by context switch
- Context switch - performing a state save of the current process to its process table an da state load of a process from its process table
- Context switch time is pure overhead (cpu must be idle during context switch) since the sytem does not useful work while switching
- 
## Process Creation in Linux
- a process may create several new proceses, each of these new processes may create other processes, forming a treee of processes
- Most op identify using id numbers (ie pid) typically integer
- unix systemd is created pid = 1 and it becomes root parent process of all processes
- linux provide pstree command, displays tree of all processes in system. pstree -p
- when a process creates a child process, that child process need certain resources (cpu time, memory, files, i/o devices) to accomplish its task
- A child process may be able to obtain its resources directly from the operating system, or it may be constrained to a subset of the resources of the parent process
- The parent may have to partition its resources amond its children, or it may be able to share some resources (such as memory or files) among several of its children
- 
## Process Termination in Linux
- WHen a process creates an
## Android Process Hierarchy


# Note 7

## Preview
- Scheduler
    - Long-Term, Short-Term(CPU), Memory
- Scheduling Criteria
- CPU Scheduling (Short-Term Scheduler)
    - FCFS
    - Shortest job first
    - round robin
    - Priority Queue
    - Guarenteed Scheduling
    - Lottery Scheduling
## CPU Scheduling 
- In a system with a single CPU, only one process can run at a time
- If CPU is busy for serving

- Objective of multiprogramming is to have some process running at all times, to maximize cpu utilization
- CPU scheduler will select a process from ready queue by scheduling algorithm
- Save pointer to process tables for ready state processes
- Level of Scheduler
    - Long-Term Scheduler: Select process form job queue and place into memory
    - Short-Term Scheduler
    - Memory Scheduler
 
## Process Scheduling
- Once the process is allocate din the memory and executing on CPU, one of several events could occur:



## Preemptive vs. Nonpreemptive Scheduling


## Scheduling Criteria
- many criteria
- CPU utilization - try to make cpu as busy as possible
- Throughput - try to finish as many as pos
- turnaround time - process start run and starting time and waiting time.
- waiting time - Until finish job how long until finish
- Response time

## Process Scheduling
A process migrates to the ready queue from various wait queues throughout its lifetime


## FCFS
- non-preemptive
- easily managed with FIFO
- when process enter the ready queue, its process table (process control block) is linked onto the tall of the queue
- when cpu is free, it is allocated to the process at the head of the queue. the running process is then removed from the queue
- Drawbacks:
    - Average wait time could be long
 
## Shortest job first
- Shortest job first algo
- when cpu available, assigned to the process that has shorted burst time
- if next cpu burst of two processes are the same, FCFS sheduling is used to break the tie

# Inter-Process Communication
- Race Condition
- Critical Section( or region)
- Solutions for mutual exclusion in a critical section
    - With Busy Waiting
        - disabling instructions
 
- Three issues in interprocess communication
- how one process can pass info to another with IPCS
- How to make sure two or more processes do not get into the critical section
- Syncronization
## Race Condition
- Race condition
    - when two or more proesses are reading and writing some shared data and the final result depends on who runs precisely
    - Critcal Section (critical region)
- Mutual Exclusion

_ how to avoid race condition
    - Mutual exclusion some way of making sure that if one process is using a shared variable or file the other processes will be exluded from doing the same thing
- Solution
    1. No two processes may be simultaneously inside their critical regions - mutual exclusion
    2. No process running outside its critical region may bloack other processes
    3. no process should have to wait forever to enter critical region
    4. No assumptions may be made about speeds or the number of cpus
Non deterministic polynomial time (NP)
never can have solution if we hace certain speed of cpu or certain number of cpu
Two approaches for mutual exclusion solutions
    - Busy wait: A process wil wait until resource become available o
    - Sleep and wakeup:
Run => Ready => Run
block => Ready

## Mutual Exclusion with Busy waiting
- Each process has time term. a process keep checking the possibility to get into into critical section
- Mutual Exclusion with Busy Waiting
    - Disabling Interrupts - non
 
## Disabling Interrupt - Nonprimitive kernel
- Once a process get into the critical section, interrupts set the disable
- Other process cannot get CPU time until the process finish its job in the critical section
## Loack Variable
- There are variable called "Lock"
    - A process can enter in its critical section when Lock = 0
    - Lock = 0 means no process is currently running in the critical section
- Strict Alternation

## Peterson's Solution
- instead of having 1 control variable we have 3 control variable
- Only works on two processes that alternate between their critical sections
- THe processes are numbered P0 and P1

## Test and Set Lock - Hardware Solution
- SInce TSL instruction is a hardware instruction. the operations of reading the lock and storing into register are guarenteed to be invisible
- Instruction Test and set lock
    - Read the content of the memory address of lock into register RX
## Memory Barriers 
- Two general models
    - Strongly ordered memory - all processes see when memory modified by another proces
    - Weakly ordered memory - may not be visible to other process
- Provide instructions that can force any hcangeds in memory 
- such instructions are known as memory barriers or memory fences
force an ordering constraint on memory operations issued before and after the barrier isntruction
## Atomic variable
- all threads or processes see actions occurring instantaneously
# priority inversion Problem
- We find solution
- what if short term scheduler use priority
- That cause problem
- what if pl is on critical section
