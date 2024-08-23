# 🛠️ Java Virtual Machine (JVM) Architecture
The Java Virtual Machine (JVM) is the core component of the Java platform, enabling Java programs to be executed on different operating systems and devices without modification. It plays a crucial role in making Java a **write once, run anywhere** language, by converting Java bytecode into machine-specific code. This allows Java applications to be run on any platform that has a JVM implementation, regardless of the underlying hardware or operating system.

[![](https://markdown-videos-api.jorgenkh.no/youtube/MxVJct7hg1w)](https://youtu.be/MxVJct7hg1w)

## JVM Architecture
The architecture of the JVM can be broken down into several key components:
1. Class Loader Subsystem
2. Memory Area
3. Execution Engine
4. Native Interface
5. Native Method Libraries

Each of these components plays a specific role in the functioning and execution of Java applications.
![JVM Architecture](https://github.com/nakulmitra/java-tutorial/blob/master/architecture/jvm-architecture/JVMArchitecture.png)

## Class Loader Subsystem
The Class Loader Subsystem is responsible for loading Java class files into the JVM memory. When you compile a Java program, the compiler generates bytecode, which is stored in `.class` files. The class loader reads these `.class` files and loads them into memory to be executed.

### Key Functions of Class Loader Subsystem
1. #### Loading
* The class loader reads the bytecode from `.class` files and loads them into the JVM memory.
2. #### Linking
* `Verify:` Ensures the bytecode follows the Java language specifications. If the verification fails, a `java.lang.VerifyError` is thrown.
* `Prepare:` Allocates memory for class variables and assigns default values to them.
* `Resolve:` Converts symbolic references in the bytecode to direct references in the JVM memory.
3. #### Initialization
* All static variables are assigned their original values, and static blocks are executed.

#### Types of Class Loaders
* Bootstrap Class Loader: Loads core Java libraries from the `<JAVA_HOME>/lib` directory.
* Extension Class Loader: Loads classes from the extension directories, typically `<JAVA_HOME>/lib/ext`.
* System/Application Class Loader: Loads classes specified in the system classpath (`CLASSPATH` environment variable).

## Memory Area (Runtime Data Areas)
The JVM organizes memory into various runtime data areas, each serving a specific purpose during the execution of Java programs.

### Key Runtime Data Areas
1. `Method Area` Stores class-level data, including static variables, constants, and method code. The method area is shared among all threads running in the JVM.
2. `Heap` The heap is used for the dynamic allocation of objects. When a Java object is created using the `new` keyword, it is allocated memory in the heap. This area is also shared across all threads.
3. `Stack` The stack is a thread-specific area where each thread has its own JVM stack. It stores frames, which contain local variables, operand stacks, and the return address of methods. Each time a method is called, a new frame is added to the stack, and once the method finishes execution, the frame is removed.
4. `PC (Program Counter) Register` Each thread has its own PC register, which holds the address of the current JVM instruction being executed.
5. `Native Method Stack` This area is used for storing native method information when the Java program interacts with native applications written in other languages like C or C++.

## Execution Engine
The **Execution Engine** is the component of the JVM responsible for executing the bytecode. It takes the bytecode loaded by the class loader and executes it in an efficient manner.

### Key Components of the Execution Engine
1. `Interpreter` The interpreter reads and executes bytecode instructions one at a time. Although simple to implement, it is slower in performance compared to other methods of execution.
2. `Just-In-Time (JIT) Compiler` The JIT compiler improves performance by compiling bytecode into native machine code at runtime. It keeps track of methods being executed and, once a method is called frequently enough (crossing a threshold), the JIT compiler compiles it into native code. This results in faster execution as the JVM can now execute native code instead of interpreting bytecode repeatedly.
3. `Garbage Collector (GC)` The garbage collector automatically manages memory by deallocating memory occupied by objects that are no longer in use (unreachable). The JVM provides different garbage collection algorithms to optimize memory management and performance.

## Native Interface
The Native Interface allows Java code to interact with native applications written in other programming languages, like C and C++. This interaction is crucial for performing tasks that are platform-dependent, such as I/O operations, memory management, or interacting with system libraries.

The JVM provides an interface, commonly known as the **Java Native Interface (JNI)**, that facilitates this interaction.

## Native Method Libraries
The Native Method Libraries are platform-specific libraries required by the JVM to perform certain tasks. These libraries are written in languages like C/C++ and are responsible for interacting with the underlying operating system to handle tasks like memory management and hardware-level operations.

## JVM Lifecycle
The JVM undergoes several stages during the lifecycle of a Java program
1. `Load:` The class loader subsystem loads the `.class` file into the JVM memory.
2. `Verify:` The bytecode verifier checks the bytecode for validity, ensuring it adheres to Java language rules and security guidelines.
3. `Prepare:` The JVM allocates memory for class variables and initializes them to default values.
4. `Resolve:` Symbolic references (e.g., method names, class names) in the bytecode are resolved to direct references in the method area.
5. `Initialize:` Static initializers are executed, and static variables are assigned their actual values.
6. `Execute:` The execution engine either interprets the bytecode or compiles it into native machine code (via the JIT compiler) for execution.
7. `Unload:` Classes that are no longer needed are unloaded from memory, and the garbage collector reclaims memory used by unreachable objects.

## Key Features of JVM
The JVM offers several powerful features that make it an essential part of the Java platform
1. `Platform Independence` The JVM enables Java programs to run on any device or operating system that has a JVM implementation. This is the essence of Java's **write once, run anywhere** philosophy.
2. `Automatic Memory Management` The garbage collector (GC) automatically manages memory, freeing developers from having to manually allocate and deallocate memory.
3. `Security` The JVM enforces strong security mechanisms through bytecode verification and runtime checks, protecting systems from malicious or erroneous code.
4. `Performance Optimization` The JIT compiler and other optimizations in the execution engine allow the JVM to execute bytecode efficiently, improving the performance of Java applications.

## How JVM Works
When you run a Java program, the JVM follows these steps to execute it
1. `Compilation` The Java compiler (javac) compiles the Java source code into bytecode, which is stored in .class files.
2. `Class Loading` The class loader subsystem loads the .class files into the JVM memory.
3. `Bytecode Verification` The bytecode verifier checks the bytecode to ensure it adheres to Java's security rules and does not perform any unsafe operations.
4. `Execution` The execution engine either interprets the bytecode or uses the JIT compiler to convert it into native machine code, which is then executed by the host machine.
5. `Garbage Collection` Periodically, the garbage collector reclaims memory used by objects that are no longer reachable, freeing up resources.

## Conclusion
The **Java Virtual Machine (JVM)** is a powerful component of the Java ecosystem, ensuring platform independence, efficient execution, and secure memory management. Understanding its architecture `class loading`, `memory areas`, `execution engine`, and `native interfaces` is crucial for developing robust and performant Java applications. The JVM enables Java's promise of **write once, run anywhere**, making it a widely adopted and versatile platform for building applications across diverse environments.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/introduction-to-java/JavaBenefits.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/architecture/jdk-jre-jvm/JDKvsJREvsJVM.md)
