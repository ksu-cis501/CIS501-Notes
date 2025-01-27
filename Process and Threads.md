## Processes and Threads Overview
#### What Are Processes and Threads?  
**Processes**  
- A process is an executing program with a unique virtual memory space.  
- Contains code (instructions), global variables, heap (dynamic memory), and stack (local variables).  
- **Process Control Block (PCB)** maintains the process context, including its state and resources.  
- Processes can have the following states:  
  - **New**, **Ready**, **Running**, **Waiting**, **Terminated**, and **Suspended**.  

**Threads**  
- A thread is a lightweight unit of execution within a process.  
- Threads share the process's code, global data, heap, and kernel resources but have separate stacks.  
- States of a thread:  
  - **Running**, **Ready**, **Blocked**.  

---

#### Key Similarities and Differences  
**Similarities**  
- Both are execution units managed by the operating system.  
- Both have states indicating their current status.  
- Both require scheduling by the CPU.  

**Differences**  
- Processes are isolated from each other, while threads share memory and resources.  
- Threads are faster to create, switch, and terminate compared to processes.  
- A process can contain multiple threads, but threads cannot exist without a parent process.  

---

**Processes and Threads in Action**  
#### Examples of Processes and Threads  
**Example 1: A Web Browser**  
- Process: Web browser application.  
- Threads:  
  - Rendering the web page.  
  - Handling user input (e.g., clicks, keystrokes).  
  - Managing network requests (e.g., loading images or scripts).  

**Example 2: A Media Player**  
- Process: Media player application.  
- Threads:  
  - Decoding audio/video.  
  - Rendering video frames.  
  - Managing playback controls (e.g., play, pause).  

---

#### The Role of the OS and Scheduler  
**Operating System (OS):**  
- Manages the creation, execution, and termination of processes and threads.  
- Allocates resources to processes (e.g., memory, I/O, CPU time).  

**Scheduler:**  
- Determines when each process or thread runs on the CPU.  
- **Process Scheduling:** Focuses on resource allocation and isolation.  
- **Thread Scheduling:** Optimizes CPU utilization and enables concurrency within processes.  

---

### **How Processes and Threads Work**  
#### States of Processes and Threads  
**Process States:**  
1. **New**: Process is being created.  
2. **Ready**: Process is waiting to execute.  
3. **Running**: Process is executing on the CPU.  
4. **Waiting**: Process is waiting for I/O or an event.  
5. **Terminated**: Process has completed execution.  
6. **Suspended**: Process is paused and moved to secondary memory.  

**Thread States:**  
1. **Running**: Thread is executing.  
2. **Ready**: Thread is waiting to execute.  
3. **Blocked**: Thread is waiting for resources or an event.  

---

#### Key Concepts in Execution  
- **Processes** own resources such as memory, files, and network connections.  
- **Threads** share resources within the process but execute independently.  
- **Multithreading** allows multiple threads within a process to execute concurrently, improving performance.  
- **Switching Between Threads:**  
  - Done by the scheduler to optimize CPU usage.  
  - Fast because threads share the same process context.  

---
