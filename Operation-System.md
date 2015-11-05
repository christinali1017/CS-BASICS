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
  * **Solution to starvation: increases priority with age**
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


###Thrashing
---
http://stackoverflow.com/questions/19031902/what-is-thrashing-why-does-it-occur

In operating systems that implement a virtual memory space the programs allocate memory from an address space that may be much larger than the actual amount of RAM the system possesses. The OS is responsible for deciding which programs "memory" is in actual RAM. It needs a place to keep things while they are "out". This is what is called "swap space", as the OS is swapping things in and out as needed. **When this swapping activity is occurring such that it is the major consumer of the CPU time, then you are effectively thrashing**. You prevent it by running fewer programs, writing programs that use memory more efficiently, adding RAM to the system, or maybe even by increasing the swap size.


###Mutex vs Semaphore
---
http://www.geeksforgeeks.org/mutex-vs-semaphore/

Consider the standard producer-consumer problem. Assume, we have a buffer of 4096 byte length. A producer thread collects the data and writes it to the buffer. A consumer thread processes the collected data from the buffer. Objective is, both the threads should not run at the same time.

**Using Mutex**:

A mutex provides mutual exclusion, either producer or consumer can have the key (mutex) and proceed with their work. As long as the buffer is filled by producer, the consumer needs to wait, and vice versa.

**At any point of time, only one thread can work with the entire buffer**. The concept can be generalized using semaphore.

**Using Semaphore**:

A semaphore is a generalized mutex. In lieu of single buffer, we can split the 4 KB buffer into four 1 KB buffers (identical resources). A semaphore can be associated with these four buffers. The consumer and producer can work on different buffers at the same time.

Strictly speaking, **a mutex is locking mechanism** used to synchronize access to a resource. Only one task (can be a thread or process based on OS abstraction) can acquire the mutex. It means there is ownership associated with mutex, and only the owner can release the lock (mutex).

**Semaphore is signaling mechanism** (“I am done, you can carry on” kind of signal). For example, if you are listening songs (assume it as one task) on your mobile and at the same time your friend calls you, an interrupt is triggered upon which an interrupt service routine (ISR) signals the call processing task to wakeup.









