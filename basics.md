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

## **NOTES**(on JDK, JRE and JVM):
1. Interpreter: In first parse, read the whole code line by line and group the instructions and then in second parse run through the grouped instructions line by line.
2. To develop Java program - JDK is must
3. Only to run java program - JRE is more than enough
4. The JVM loads and executes Java bytecode. It starts by interpreting the bytecode and, for frequently executed code(block of code), uses JIT compilation to convert it to native machine code for faster execution. So the JVM does two things:
   1. Interprets bytecode initially.
   2. JIT Compiles hot code paths for performance.
  
##### Interview 
- Answer:
   - JVM is the execution engine. It runs Java bytecode and handles memory and garbage collection.
   - JRE provides the environment required to run Java applications. It includes the JVM and core libraries.
   - JDK provides everything needed to develop Java applications. It includes the JRE plus the compiler (javac) and development tools.
- One-liner to close:
   - JDK = JRE + compiler
   - JRE = JVM + libraries
   - JVM = runs bytecode
---
## Datatypes
##### NOTE: 1 byte = 8 bit
<img width="1879" height="1390" alt="image" src="https://github.com/user-attachments/assets/f2b1513b-4ef1-4ae5-b098-c8d9a7eec701" />
`Datatype defines what type of value a variable can hold and how much memory it needs`.

- In java `datatypes` are of two types:
   1. Primitive datatypes(stores in stack, fixed size, store actual values)
   2. Non-Primitive datatypes(stores in heap, store address of objects)
- range of each primitive type

| Type    |Size (bits)            | Size (bits)           | Range                                                   |
| ------- | --------------------- | --------------------- | ------------------------------------------------------- |
| byte    | 1                     | 8                     | -128 to 127                                             |
| short   | 2                     | 16                    | -32,768 to 32,767                                       |
| int     | 4                     | 32                    | -2,147,483,648 to 2,147,483,647                         |
| long    | 8                     | 64                    | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| float   | 4                     | 32                    | ~±3.4 × 10^38 (7 decimal digits precision)              |
| double  | 8                     | 64                    | ~±1.7 × 10^308 (15 decimal digits precision)            |
| char    | 2                     | 16                    | 0 to 65,535 (Unicode)                                   |
| boolean | JVM dependent         | 1 bit (JVM dependent) | true / false                                            |
##### NOTE: 
> The size of boolean is not specified by the Java language. The JVM decides it. Practically, it is usually stored as 1 byte in arrays, but inside objects it may take 1 byte or more due to padding and alignment.
##### Do NOT say: 
> The statement i.e. `boolean is 1 bit` is wrong as it represents 1 bit logically, but is not stored as 1 bit in memory
##### Interview line:
> `boolean` does not have a defined size in Java. It is typically represented as 1 byte at runtime, but the JVM may use more depending on memory alignment.

##### In-built method to see the **_min and max range_ of primitive datatypes**.
```JAVA
public class Main
{
	public static void main(String[] args) {
		// int
		System.out.println("min: "+Integer.MIN_VALUE);
		System.out.println("max: "+Integer.MAX_VALUE);
		
		// datatype
		//System.out.println("min: "+WrapperClass.MIN_VALUE);
		//System.out.println("max: "+WrapperClass.MAX_VALUE);
	}
}
```
##### In-built method to get **_binary_ of a number**.
```JAVA
public class Main
{
	public static void main(String[] args) {
		// int
		System.out.println("binary of int's max range");
		System.out.println(Integer.toBinaryString(Integer.MAX_VALUE));
		
		// random Number
		System.out.println("binary of of random number");
		System.out.println(Integer.toBinaryString(7));
		
		// general way
		//System.out.println(WrapperClass.toBinaryString(value));
	}
}
```

### char
- It is an unsigned datatype
   - Unsigned: char is always non-negative  
- In java instead of `ascii` table, `unicode` table is used.
- `ASCII` is a subset of `Unicode`.
   - ASCII: 0-128
   - Unicode: 128-65,535 
- Unicode was introduced in java to overcome the limitation of `ASCII` as it covers almost all languages characters. 
- In java char's size is of 2 byte i.e., it takes around 16 bits of memory.

| Feature              | Details                                                        |
| -------------------- | -------------------------------------------------------------- |
| **Type**             | Primitive, unsigned                                            |
| **Size**             | 2 bytes (16 bits)                                              |
| **Range**            | 0 to 65,535 (Unicode)                                          |
| **Literal Notation** | Single quotes `'A'`, `'₹'`, `'中'`                             |
| **Escape Sequences** | `\n`, `\t`, `\\`, `\'`, `\"`                                   |
| **Numeric Nature**   | Internally stores Unicode code point; arithmetic allowed       |
| **ASCII Relation**   | ASCII is subset of Unicode (0–127)                             |
| **Purpose**          | Represent characters from **all languages** using Unicode      |
| **Why Java uses it** | Overcomes ASCII limitation of handling only English characters |

```JAVA
public class Main
{
	public static void main(String[] args) {
		// char
		char format1 = 124;
		System.out.println("format1: "+ format1);
		char format2 = 'b';
		System.out.println("format2: "+ format2);
		char format3 = '\u0025';
		System.out.println("format3: "+ format3);	
		
		// char to int
		System.out.println((int)'%');
		// char to unicode
		System.out.println(Character.codePointAt("%", 0));
		
	}
}
```

