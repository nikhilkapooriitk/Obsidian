
##### Common UNIX Commands
Chmod is used to change the mode(permission) for file or directory.
![[Pasted image 20250421201103.png]]
First place is used for user, then group, then others.
4 is used for read, 2 for write, 1 for execution. 
Ex: 765 means user has read write & execute, group has read & write, others has read & execute

##### Common Terms in OS
**Thread** -> Lightweight units of execution within a process. Multiple threads can exist in single process.
**Interrupt** -> Asynchronous event that tells the CPU to stop what it's doing and switch to a different task( of higher priority ) Ex: Mouse, keyboard interrupts, system calls, exceptions etc
**Interrupt Handling** -> Once interrupt occurs, CPU suspends the current thread's execution, saves its state, and jumps to an interrupt handler (also called ISR - Interrupt Service Routine)
**Interrupt Service Routing** -> ISR are specific code routine that handle the interrupt. They determine the source of interrupt and take its appropriate action such as reading data form device or handling error.
**Context** **Switching** -> The process of saving the state of the interrupted thread or process and loading the state of new thread that will handle the interrupt is called context switching. Allowing single core to appear to execute multiple threads concurrently.
**Core** -> Physical processing unit of CPU, capable of executing instructions independently. Runs threads or process.
**Interrupt** **Latency** -> Time taken from the occurrence of interrupt request to the beginning of corresponding ISR. Low interrupt latency of important for RTOS. RTOS has low interrupt latency and low context switching time. Affected by hardware, interrupt handling mechanisms, system load etc.
**Context** **switching** **latency** -> Time taken from switch of one thread to beginning of execution of other thread. Affected by complexity of context switch process, amt of data need to be saved and restored, overhead associated with managing thread execution etc
**RTOS (Real Time OS)** -> Special type of OS where tasks must be completed within strict time constraints. Typically used in real time applications like automotive, medical devices etc.





