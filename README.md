# Learning_JAVA
# **How Java Code Runs: JVM, JIT, and Key Concepts Explained**  

Java is known for its **"Write Once, Run Anywhere"** capability, made possible by the **Java Virtual Machine (JVM)** and **Just-In-Time (JIT) Compilation**. Let's go through the entire process step by step, covering all the important concepts.

---

## **1. Java Code Execution Overview**  

When you write Java code, it goes through multiple stages before execution:

1. **Compilation** – Java code is compiled into **bytecode**.
2. **Class Loading** – The **JVM loads bytecode** into memory.
3. **Bytecode Interpretation** – The JVM **interprets** bytecode line by line.
4. **JIT Compilation** – The **JIT compiler** optimizes frequently used code by converting it into **native machine code**.
5. **Execution** – The **CPU executes the optimized machine code**.

Now, let's explore each step in detail.

---

## **2. Java Compilation Process**  
### **Step 1: Writing Java Code**
You write Java source code in a `.java` file:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### **Step 2: Compiling to Bytecode**
You compile the Java file using the `javac` compiler:
```sh
javac HelloWorld.java
```
This produces a **HelloWorld.class** file, which contains **bytecode** (a platform-independent representation).

### **Step 3: Running the Bytecode in JVM**
When you run:
```sh
java HelloWorld
```
The **JVM (Java Virtual Machine)** executes the bytecode.

---

## **3. Understanding the JVM (Java Virtual Machine)**  
The **JVM** is responsible for running Java programs. It consists of the following components:

| Component | Function |
|-----------|----------|
| **Class Loader** | Loads `.class` files into memory. |
| **Bytecode Verifier** | Checks for security and correctness. |
| **Interpreter** | Executes bytecode line-by-line. |
| **JIT Compiler** | Converts frequently used bytecode to native machine code for faster execution. |
| **Garbage Collector** | Frees memory by removing unused objects. |

---

## **4. JVM Execution Flow (Step-by-Step)**  
### **Step 1: Class Loading**
- The **ClassLoader** loads `.class` files into JVM memory.
- It follows a **three-step process**:
  - **Loading** – Reads the `.class` file.
  - **Linking** – Verifies bytecode and prepares it for execution.
  - **Initialization** – Initializes static variables.

### **Step 2: Bytecode Verification**
- The **Bytecode Verifier** checks for:
  - Security vulnerabilities.
  - Invalid bytecode instructions.
  - Type-safety violations.

### **Step 3: Interpretation (Initial Execution)**
- The **JVM initially interprets** the bytecode, executing instructions **line by line**.
- This is slow because each instruction is processed separately.

### **Step 4: JIT Compilation (Performance Optimization)**
- The **JIT Compiler** identifies frequently executed methods ("hotspots") and compiles them into **native machine code**.
- This machine code runs directly on the **CPU**, speeding up execution.

---

## **5. Just-In-Time (JIT) Compilation in JVM**
### **What is JIT Compilation?**
- Instead of **interpreting** bytecode repeatedly, **JIT compiles "hot" code** into **native machine code** at runtime.
- This compiled code is stored in memory and reused for faster execution.

### **How JIT Works (Step-by-Step)**
1. The JVM **executes bytecode** using an **interpreter**.
2. If a method is executed frequently, it is marked as a **hotspot**.
3. The **JIT Compiler compiles** the hotspot into **native machine code**.
4. The JVM **executes the native code instead of interpreting bytecode**, making execution much faster.

### **JIT Optimizations**
- **Method Inlining** – Removes function call overhead by embedding the method body directly.
- **Loop Unrolling** – Optimizes loops by reducing control statements.
- **Dead Code Elimination** – Removes unused code.
- **Branch Prediction** – Optimizes `if-else` conditions based on execution history.

---

## **6. Garbage Collection in JVM**
The **Garbage Collector (GC)** automatically manages memory by removing unused objects.

### **Types of GC in Java**
| Garbage Collector | Description |
|------------------|-------------|
| **Serial GC** | Best for small applications. |
| **Parallel GC** | Uses multiple threads for faster execution. |
| **G1 GC** | Default GC in modern JVMs, balances performance and memory. |
| **ZGC / Shenandoah GC** | Designed for ultra-low pause times. |

---

## **7. Memory Management in JVM**
The **JVM Memory Model** is divided into several areas:

| Memory Area | Purpose |
|------------|---------|
| **Method Area** | Stores class metadata, static variables. |
| **Heap** | Stores objects (managed by GC). |
| **Stack** | Stores method call frames and local variables. |
| **PC Register** | Keeps track of the next instruction to execute. |
| **Native Method Stack** | Supports native (non-Java) method execution. |

---

## **8. Java Execution Modes**
Java can run in different execution modes:

| Mode | Description |
|------|-------------|
| **Interpreted Mode** | JVM executes bytecode line-by-line (slower). |
| **JIT Compilation** | JVM compiles hotspots into native code (faster). |
| **AOT Compilation** | Compiles Java code **before execution** (like GraalVM). |

---

## **9. JIT vs. AOT Compilation**
| Feature | JIT (Just-In-Time) | AOT (Ahead-Of-Time) |
|---------|----------------|----------------|
| **Compilation Time** | At runtime | Before execution |
| **Optimization Level** | High (adapts to runtime behavior) | Medium (fixed at compile time) |
| **Startup Time** | Slower (needs to warm up) | Faster (precompiled) |
| **Performance** | Faster after warm-up | Faster from the start |
| **Example** | HotSpot JIT | GraalVM Native Image |

---

## **10. Java Performance Optimization Techniques**
- **Use JIT Compilation** – JVM optimizes performance dynamically.
- **Enable GC Logging** – Monitor garbage collection:
  ```sh
  -XX:+PrintGCDetails
  ```
- **Use JVM Flags for Performance Tuning**:
  ```sh
  java -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC MyApp
  ```
- **Profile Application** – Use tools like **JVisualVM**, **JFR**, or **YourKit**.

---

## **Final Summary**
1. **Java Compilation**
   - `javac` compiles Java code to **bytecode**.
   - Bytecode is platform-independent.

2. **JVM Execution**
   - The **JVM loads, verifies, and executes bytecode**.
   - Initially, it **interprets** the code.

3. **JIT Compilation**
   - **JIT compiles frequently used code** into **native machine code** for faster execution.
   - It applies **optimizations** like inlining and loop unrolling.

4. **Memory & Garbage Collection**
   - The **Garbage Collector (GC)** manages memory automatically.
   - JVM **divides memory** into the **Heap, Stack, and Method Area**.

5. **Performance Optimization**
   - Use **JVM tuning flags**, **profilers**, and **G1 GC** for performance.

---

## **Next Steps**
### Multithreading
Yes, exactly! Let’s break it down step by step:

### **Understanding CPU Cores & Threads in Execution**
1. **CPU with 8 Cores**:  
   - A CPU with **8 cores** means it can handle **8 independent tasks (processes) at the same time**.
   - Each core is capable of executing instructions independently.

2. **Each Program is a Set of Instructions (Process)**:  
   - Programs like **Word, Notepad, and a music player** are all **processes**.
   - A process consists of multiple **instructions** that need execution.

3. **Multithreading in a Core**:  
   - Modern CPUs use **Simultaneous Multithreading (SMT)**, commonly known as **Hyperthreading** (in Intel CPUs).
   - If a core supports **2 threads**, then an **8-core CPU can handle 16 threads** at once.
   - **Each thread executes a part of a process** (e.g., Word could have multiple threads handling UI updates, autosave, spell-checking, etc.).

---

### **Example: How an 8-Core CPU Runs Multiple Programs**
Let's assume:
- **Word** (Process 1) runs on **Core 1**  
- **Notepad** (Process 2) runs on **Core 2**  
- **Music Player** (Process 3) runs on **Core 3**  
- **Chrome** (Process 4) runs on **Core 4**  
- **VS Code** (Process 5) runs on **Core 5**  
- **Game** (Process 6) runs on **Core 6**  
- **Zoom** (Process 7) runs on **Core 7**  
- **Background OS Tasks** (Process 8) run on **Core 8**  

Now, if **each core supports 2 threads**, then:
- Each program can have **multiple threads executing in parallel**.
- For example, Chrome might have **one thread for rendering UI** and **another for network requests**.

---

### **Key Takeaways**
✅ More cores = More parallel execution of different programs (processes).  
✅ More threads per core = Better utilization of CPU power (multitasking within a process).  
✅ Hyperthreading allows **one physical core to act as two logical threads**, improving efficiency.  
✅ The **OS scheduler** assigns processes and threads to different cores dynamically.  

### **⏳ Time Slicing & Context Switching in CPUs**  

When multiple programs (processes) are running on a CPU, the operating system ensures fair execution using two important concepts:  

1. **Time Slicing** ⏳  
2. **Context Switching** 🔄  

---

### **🔹 1. Time Slicing (CPU Scheduling)**
- The CPU **divides time into small chunks (time slices or time quanta)**.  
- Each **process gets a fixed time slice** to execute on a core.  
- When the time slice expires, the **CPU switches to another process**.  
- This switching is managed by the **CPU scheduler** (e.g., Round Robin scheduling).  

#### **Example of Time Slicing:**
- Suppose an **8-core CPU** runs 10 programs, but only 8 can run simultaneously.
- The OS assigns **each program a short time slice** (e.g., 10ms).
- If a program doesn’t finish within 10ms, it goes to the **waiting queue** while the next program gets CPU time.

✅ **Effect:** Users feel like all programs are running simultaneously, even though each gets CPU time in turns.  

---

### **🔹 2. Context Switching (Process & Thread Switching)**
- When the **CPU switches from one process to another**, it **saves the current state** (registers, program counter, etc.) and **loads the new process state**.
- This transition is called **context switching**.  
- Context switching happens when:
  - The time slice ends (**preemption**).
  - A process moves to a waiting state (e.g., waiting for I/O).
  - A higher-priority task needs CPU time.  

#### **Example of Context Switching:**
1. **Process A** is running, and its time slice ends.  
2. CPU **saves Process A’s state** (registers, program counter, stack).  
3. CPU **loads Process B’s state** and starts executing it.  
4. Later, when Process A gets CPU time again, its **saved state is restored**, and execution resumes.

✅ **Effect:** Users experience smooth multitasking, even with limited CPU cores.  

---

### **🔹 Time Slicing vs. Context Switching**
| Feature | Time Slicing ⏳ | Context Switching 🔄 |
|---------|---------------|--------------------|
| **Purpose** | Divides CPU time among processes | Saves & restores process states |
| **Who Manages It?** | OS Scheduler | CPU & OS Kernel |
| **When It Happens?** | Fixed time quantum expires | Switching between processes or threads |
| **Performance Impact** | Keeps programs responsive | Adds overhead (switching takes time) |

---

### **🛠️ Impact on Java & Spring Boot**
Since Java applications (especially Spring Boot microservices) run multiple **threads**, understanding these concepts helps with:  
✅ **Optimizing thread pools** (reducing excessive context switching).  
✅ **Using non-blocking I/O** (reducing idle waiting).  
✅ **Tuning CPU-intensive tasks** (leveraging multiple cores).  

---

### **🚀 Java Thread Lifecycle Explained**  

In Java, a thread goes through **five main states** during its lifetime. These states are managed by the **JVM & OS Scheduler**.  

---

### **📌 1. New (Created) 🆕**
- A thread is created using `Thread` class or implementing `Runnable`.  
- It is **not yet started**, just an object in memory.  
- **Method:** `new Thread(runnableInstance);`  
- **State:** `NEW`  

🔹 **Example:**  
```java
Thread t = new Thread(() -> System.out.println("Hello"));
```
🔹 **At this stage, the thread is not running yet.**  

---

### **📌 2. Runnable (Ready) ▶️**
- When `start()` is called, the thread moves to **Runnable** state.  
- It is **waiting for CPU time** (scheduled by the OS).  
- **Method:** `t.start();`  
- **State:** `RUNNABLE`  

🔹 **Example:**  
```java
Thread t = new Thread(() -> System.out.println("Hello"));
t.start();  // Now it's in the RUNNABLE state
```
🔹 **The thread is now waiting for CPU allocation.**  

---

### **📌 3. Running (Executing) ⚡**
- The thread is **actively executing** its task.  
- The OS scheduler assigns CPU time to this thread.  
- **State:** `RUNNING`  

🔹 **Example:**  
If a thread gets CPU time, it enters the `RUNNING` state:  
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is Running");
    }
}
MyThread t = new MyThread();
t.start();  // Moves from NEW -> RUNNABLE -> RUNNING
```
🔹 **If a thread is preempted (time slice over), it goes back to RUNNABLE.**  

---

### **📌 4. Blocked / Waiting / Timed Waiting ⏳**
A thread is **paused temporarily** and waiting for an event (e.g., I/O, lock).  

There are **3 types of waiting states**:
1. **Blocked**: Waiting for a resource (e.g., lock on synchronized block).  
2. **Waiting**: Waiting indefinitely until notified (`wait()` without timeout).  
3. **Timed Waiting**: Waiting for a fixed time (`sleep()`, `join(time)`, `wait(time)`).  

#### **Examples**:
🔹 **Blocked:**
```java
synchronized(obj) {
    obj.wait();  // Thread will wait until obj.notify() is called
}
```
🔹 **Waiting:**
```java
t.join();  // Current thread waits indefinitely for t to finish
```
🔹 **Timed Waiting:**
```java
Thread.sleep(1000);  // Thread will wait for 1 second
```

---

### **📌 5. Terminated (Dead) ☠️**
- A thread completes execution **or is stopped**.  
- **Cannot be restarted** once terminated.  
- **State:** `TERMINATED`  

🔹 **Example:**  
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread execution completed");
    }
}
MyThread t = new MyThread();
t.start();  // RUNNABLE -> RUNNING -> TERMINATED
```
🔹 **Once a thread finishes execution, it cannot be restarted.**  

---

### **📌 Java Thread Lifecycle Diagram**
```
       [NEW] ---> start() ---> [RUNNABLE] ---> [RUNNING] ---> [TERMINATED]
                               ↑        |   |        |  
                      (Waiting) |        |   | (Time Slicing)  
                               |        ↓   ↓  
                     [BLOCKED]  [WAITING] [TIMED WAITING]  
```

---

### **🚀 Summary of Thread Lifecycle**
| State | Trigger | Example |
|--------|---------|---------|
| **NEW** | Created but not started | `Thread t = new Thread();` |
| **RUNNABLE** | `start()` called, waiting for CPU | `t.start();` |
| **RUNNING** | OS assigns CPU | `run()` method executes |
| **BLOCKED** | Waiting for a resource (e.g., lock) | `synchronized(obj) { wait(); }` |
| **WAITING** | Waiting indefinitely | `t.join();` |
| **TIMED WAITING** | Waiting for a fixed time | `Thread.sleep(1000);` |
| **TERMINATED** | Execution complete | Thread ends |

---

### **🔥 Real-World Java Thread Use Cases**
✅ **Multi-threaded servers** (Spring Boot microservices, handling multiple requests).  
✅ **Background tasks** (e.g., cron jobs, email sending).  
✅ **Parallel computing** (e.g., processing large datasets).  
✅ **Asynchronous processing** (e.g., CompletableFuture).  

Would you like me to explain **thread synchronization, deadlocks, or executors next?** 🚀
