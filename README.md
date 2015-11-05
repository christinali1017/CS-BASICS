##Operation System

####IPC

Inter process communication.
- Shared memory
- Message passing

Message passing may be either blocking or non-blocking. Blocking is considered synchronous. Non-blocking is considered asynchronous.



####Latency and Throughput

- **Latency** is the time required to perform some action or to produce some result.

- **Throughput** is the number of such actions executed or results produced per unit of time. 

Example: Suppose there is a factory which takes 8 hours to produce a car and it can produce 100 cars per day. Then the latency is 8 hours. Throughput is 100 cars/day.


####Process and process table

http://courses.cs.vt.edu/csonline/OS/Lessons/Processes/index.html

A **process** is an instance of program in execution. For example a Web Browser is a process, a shell (or command prompt) is a process.

The operating system is responsible for managing all the processes that are running on a computer and allocated each process a certain amount of time to use the processor. In addition, the operating system also allocates various other resources that processes will need such as computer memory or disks. To keep track of the state of all the processes, the operating system maintains a table known as the **process table**. Inside this table, every process is listed along with the resources the processes is using and the current state of the process.

Processes can be in one of three states: running, ready, or waiting. The running state means that the process has all the resources it need for execution and it has been given permission by the operating system to use the processor. Only one process can be in the running state at any given time. The remaining processes are either in a waiting state (i.e., waiting for some external event to occur such as user input or a disk access) or a ready state (i.e., waiting for permission to use the processor). In a real operating system, the waiting and ready states are implemented as queues which hold the processes in these states. 






