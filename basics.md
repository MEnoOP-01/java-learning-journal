## BASICS

## 1. JDK, JVM and JRE 
<img width="2846" height="1780" alt="image" src="https://github.com/user-attachments/assets/641b1fa2-6132-4f44-8069-218e7084f12f" /><br/>

> .java --> javac(compilation) --> .class(bytecode) which is platform independent -->JVM(interepretes) --> machine code which is platform dependent

#### JDK:
- Java Development kit
- It contains all the development tools required to develop a java application.
- It contains `javac` compiler which coverts the `.java`(Source code) file to `. class`(byte code) file.
- It contains the source code of all the inbuilt helping methods which we uses.
- It contains debugging tools and JRE too.

#### JRE:
- Java runtime environment.
- It contains all the core libraries and JVM.
- To run java, JRE must be in the system.
- The root Object class is part of the core Java libraries hence JRE contains root object class.

#### JVM:
- Java virtual machine.
- It loads and executes Java bytecode.
- It contains JIT compiler.

## **NOTES**:
1. Interpreter: In first parse, read the whole code line by line and group the instructions and then in second parse run through the grouped instructions line by line.
2. To develop Java program - JDK is must
3. Only to run java program - JRE is more than enough
4. The JVM loads and executes Java bytecode. It starts by interpreting the bytecode and, for frequently executed code(block of code), uses JIT compilation to convert it to native machine code for faster execution. So the JVM does two things:
   1. Interprets bytecode initially.
   2. JIT Compiles hot code paths for performance.
