# JDK vs JRE vs JVM
[![](https://markdown-videos-api.jorgenkh.no/youtube/lbyLT3KgkF0)](https://youtu.be/lbyLT3KgkF0)

## Differences between JVM, JRE, and JDK
![JVM Architecture](https://github.com/nakulmitra/java-tutorial/blob/master/introduction-to-java/jdk-jre-jvm/JDKvsJREvsJVM.png)

|         Component         |   JVM (Java Virtual Machine) |   JRE (Java Runtime Environment)  |   JDK (Java Development Kit) |
| ------------------------- | ---------------------------- | --------------------------------- | ---------------------------- |
| Purpose  | Executes Java bytecode, provides a platform-independent execution environment.  | Provides everything required to run Java applications, including the JVM and libraries.                 | Provides tools for developing Java applications, including the JRE and development utilities.  |  
| Contains  | Class loader, runtime data areas, execution engine, garbage collector, etc. | JVM, core libraries (Java API), and resources needed to run Java applications. | JRE, development tools (compiler, debugger, etc.), and additional libraries required for development. | 
| Used By  | End users or environments where Java bytecode needs to be executed. | End users who need to run Java applications. | Java developers who need to write, compile, debug, and run Java code. | 
| Development Tools  | No | No | Yes (compiler, debugger, etc.) | 

## Java Virtual Machine (JVM)
The **Java Virtual Machine (JVM)** is the cornerstone of the Java programming language, playing a crucial role in Java's `write once, run anywhere` capability. It is responsible for running the compiled Java bytecode, making the same code executable across various platforms without requiring modifications.

### Key Points about JVM
* `Functionality:` The JVM provides a runtime environment that converts Java bytecode (compiled from Java source code) into machine code that can be understood by the host operating system.
* `Platform Independence:` By using JVMs tailored to specific operating systems, Java programs can run on any platform without the need for recompilation, ensuring platform independence.
* `Execution Process:` The JVM handles memory management (through garbage collection), provides security features, and interprets or compiles bytecode into native machine instructions.

### Components of JVM
* `Class Loader:` Loads the `.class` files into memory.
* `Runtime Data Areas:` Manages memory and stores data during the execution of Java programs, including the heap, stack, and method area.
* `Execution Engine:` Executes the loaded bytecode, either through interpretation or Just-In-Time (JIT) compilation.
* `Garbage Collector (GC):` Manages memory by automatically reclaiming memory from objects no longer in use.

## Java Runtime Environment (JRE)
The **Java Runtime Environment (JRE)** is the software package that provides everything required to run Java applications. While the JVM only offers an environment to execute bytecode, the JRE provides the complete runtime environment, including the JVM, libraries, and other resources.

### Key Points about JRE
* `Functionality:` The JRE includes the JVM along with a set of core Java libraries and other resources necessary for executing Java applications.
* `No Development Tools:` The JRE does not include development tools such as the Java compiler (`javac`). It is intended solely for users who need to run Java applications, not for developers who need to write or compile code.
* `Libraries:` It contains a set of standard Java libraries (such as Java APIs, class libraries) that are required by the JVM during the execution of Java programs.

### Components of JRE
* `JVM:` The core component that executes Java bytecode.
* `Core Libraries:` Java class libraries, such as those from `java.lang`, `java.util`, `java.io`, etc.
* `Other Resources:` Configuration files and other runtime support files that the JVM uses to ensure a smooth execution process.

## Java Development Kit (JDK)
The **Java Development Kit (JDK)** is the full-featured software development kit used by developers to create, compile, and debug Java programs. The JDK contains everything found in the JRE, plus additional development tools.

### Key Points about JDK
* `Functionality:` The JDK provides the necessary tools for Java application development, including a compiler to convert source code into bytecode, a debugger, and a variety of libraries.
* `Includes JRE:` The JDK includes the JRE, meaning it contains both the JVM and the libraries needed to run Java applications, along with additional tools for development.
* `Development Tools:` The JDK comes with a range of utilities such as `javac` (Java compiler), `javadoc` (documentation generator), and `jar` (packaging tool).

### Components of JDK
* `JRE:` Provides everything required to run Java applications.
* `Development Tools:` Tools such as `javac` (the Java compiler), `jdb` (Java debugger), and `jarsigner` for signing JAR files.

## Summary
* ### JVM (Java Virtual Machine)
* It is the core part of the Java platform, responsible for executing Java bytecode. It is included in both the JRE and the JDK.
* Ensures platform independence by converting bytecode into machine-specific instructions.
* ### JRE (Java Runtime Environment)
* It is the runtime environment required to run Java applications. It includes the JVM and the standard Java libraries but does not include development tools like the compiler.
* ### JDK (Java Development Kit)
* It is the complete development environment, containing the JRE along with development tools like the Java compiler, debugger, and more.It is required by developers to write, compile, and debug Java applications.

#### In short
* `JVM:` Core engine to run Java bytecode.
* `JRE:` Used to run Java programs, contains JVM and libraries.
* `JDK:` Full development kit, containing the JRE and tools for compiling and debugging Java applications.

## Conclusion
The understanding of **JVM**, **JRE**, and **JDK** is essential for anyone working with Java. The JVM provides the core execution engine, while the JRE offers the runtime environment to run Java applications. For Java development, the JDK is indispensable as it includes everything needed to write, compile, and debug programs. Knowing the distinction between these three components will help you determine what is needed in different situations: JDK for development, JRE for running applications, and JVM as the execution engine.
