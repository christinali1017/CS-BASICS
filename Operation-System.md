###Processor
---
- Fetch next instruction
- decode
- execute

###Memory Hierarchy

- Registers
- Cache
- Main memory
- Hard disk
- ...

###Process and process table
---

http://courses.cs.vt.edu/csonline/OS/Lessons/Processes/index.html

**A process is an instance of program in execution**. For example a Web Browser is a process, a shell (or command prompt) is a process.

**To keep track of the state of all the processes**, the operating system maintains a table known as the **process table**. Inside this table, every process is listed along with the resources the processes is using and the current state of the process.

**Processes states**: 
- new
- running
- ready
- waiting
- terminated

The running state means that the process has all the resources it need for execution and it has been given permission by the operating system to use the processor. 

Only one process can be in the running state at any given time. The remaining processes are either in a waiting state (i.e., waiting for some external event to occur such as user input or a disk access) or a ready state (i.e., waiting for permission to use the processor). **CPU switches back & forth among processes(Pseudo-parallelism)**. In a real operating system, **the waiting and ready states are implemented as queues which hold the processes in these states.** 

**A process consists of(at least)**: (**Process Control Block** PCB)

- Process state
- Program counter
- CPU registers
- CPU scheduling information eg: priority
- Memory management information
- Accounting information
- I/O status
- ....

**Process identifiers**: PID, is global to the system.

###Schedule
---
**no-preemptive vs preemptive**

- No-preemptive: once process gets the cpu, it doesn't release it until the process terminates or switches to waiting.

- preemptive: Using a timer, the OS can preempt the CPU even it the thread doesn’t relinquish it voluntarily.

**Scheduling methods**:

- First come first served
- Shortest job first
- Shortest remaining time first
- Priority scheduling. Pick process with highest priority
  * **Possible issues of priority scheduling**: **Starvation**: With an endless supply of high priority jobs, low priority processes may never execute
  * Solution to starvation: increases priority with age
- Round-robin scheduling 


###Thread
---
http://www.personal.kent.edu/~rmuhamma/OpSystems/Myos/threads.htm

Processes are used to group resources together and threads are the entities scheduled for execution on the CPU.

A thread is a single sequence stream within in a process. Because threads have some of the properties of processes, they are sometimes called lightweight processes. 

In a process, threads allow multiple executions of streams. **In many respect, threads are popular way to improve application through parallelism. The CPU switches rapidly back and forth among the threads giving illusion that the threads are running in parallel**. Like a traditional process i.e., process with one thread, a thread can be in any of several states (Running, Blocked, Ready or Terminated). **Each thread has its own stack.** Since thread will generally call different procedures and thus a different execution history. This is why thread needs its own stack. An operating system that has thread facility, the basic unit of CPU utilization is a thread. **A thread has or consists of a program counter (PC), a register set, and a stack space.** **Threads are not independent of one other like processes as a result threads shares with other threads their code section, data section, OS resources  also known as task, such as open files and signals.**

**Re-entrant**: able to handle a second call while not
done with previous one


###Thread vs Process
---
Why Threads? (**Cheaper and may faster**)

- Simpler programming model for concurrent activities
- Easier/faster to communicate between threads than
processes
- Easier/cheaper to create/destroy than processes since they have no resources attached to them
- With good mix of CPU and I/O bound activities, better performance
- Even better if you have multiple CPUs
- Context switching are fast when working with threads. The reason is that we only have to save and/or restore PC, SP and registers. **But this cheapness does not come free - the biggest drawback is that there is no protection between threads.**


###Deadlocks and necessary conditions
---

**Deadlock** is a situation or condition when two or more processes are holding some resources and trying to acquire some more resources, and they can not release the resources until they finish there execution.

**Necessary conditions**:
- **Mutual Exclusion**: There is s resource that cannot be shared.
- **Hold and Wait**: A process is holding at least one resource and waiting for another resource which is with some other process.
- **No Preemption**: The operating system is not allowed to take a resource back from a process until process gives it back.
- **Circular Wait**:  A set of processes are waiting for each other in circular form.


###Virtual Memory
---
https://en.wikipedia.org/wiki/Virtual_memory

Virtual memory is a memory management technique which maps memory addresses used by a program(**Virtual addresses**) into physical addresses in computer memory. 

Memory management unit(MMU) automatically translates virtual addresses to physical addresses.

Software within the operating system may extend these capabilities to provide a **virtual address space that can exceed the capacity of real memory and thus reference more memory than is physically present in the computer**

The primary benefits of virtual memory include freeing applications from having to manage a shared memory space, increased security due to memory isolation, and being able to conceptually use more memory than might be physically available, using the technique of **paging**.



###IPC
---

Inter process communication.
- Shared memory
- Message passing

Message passing may be either blocking or non-blocking. Blocking is considered synchronous. Non-blocking is considered asynchronous.



###Latency and Throughput
---

- **Latency** is the time required to perform some action or to produce some result.

- **Throughput** is the number of such actions executed or results produced per unit of time. 

Example: Suppose there is a factory which takes 8 hours to produce a car and it can produce 100 cars per day. Then the latency is 8 hours. Throughput is 100 cars/day.








