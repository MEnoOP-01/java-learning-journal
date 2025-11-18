- cyclomatic complexity?

# BASICS

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
> <img width="1879" height="1390" alt="image" src="https://github.com/user-attachments/assets/f2b1513b-4ef1-4ae5-b098-c8d9a7eec701" />
> Datatype defines what type of value a variable can hold and how much memory it needs.

- In java `datatypes` are of two types:
   1. Primitive datatypes(stores in stack, fixed size, store actual values)
   2. Non-Primitive datatypes(stores in heap, store address of objects)
- range of each primitive type

| Data Type | Size               | Default Value | Range                                       |
| --------- | ------------------ | ------------- | --------------------------------------------|
| byte      | 1 byte             | 0             | -128 to 127                                 |
| short     | 2 bytes            | 0             | -32,768 to 32,767                           |
| int       | 4 bytes            | 0             | -2³¹ to 2³¹-1                               |
| long      | 8 bytes            | 0L            | -2⁶³ to 2⁶³-1                               |
| float     | 4 bytes            | 0.0f          | ~±3.4 × 10^38 (7 decimal digits precision)  |
| double    | 8 bytes            | 0.0d          | ~±1.7 × 10^308 (15 decimal digits precision)|
| char      | 2 bytes            | '\u0000'      | 0 to 65,535 (Unicode)                       |
| boolean   | JVM dependent      | false         | true/false                                  |

##### NOTE: 
> The size of boolean is not specified by the Java language. The JVM decides it. Practically, it is usually stored as 1 byte in arrays, but inside objects it may take 1 byte or more due to padding and alignment.
> Local variables don’t have default values; instance and static variables do.
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
---
## Variable
#### Naming convention:
> <img width="3051" height="619" alt="image" src="https://github.com/user-attachments/assets/f63cd14e-7e9f-4902-bff6-8a5943d6387d" />

##### Q: What is variable:
- A `variable` is a named memory location that stores a value which can change during program execution.
	- Suppose it is a labeled box where you can store a value and read or update it.
	- Every variable has a data type, which defines what kind of value it can store.

##### Types of Variables in Java:  
| Type             | Where Defined                         | Scope                          | Default Value        | Lifetime                       | Notes                                     |
| ---------------- | ------------------------------------- | ------------------------------ | -------------------- | ------------------------------ | ----------------------------------------- |
| **Local**        | Inside a method/block                 | Only inside the method/block   | None                 | Exists during method execution | Must be explicitly initialized before use |
| **Instance**     | Inside a class (non-static)           | Accessible via object          | Yes (0, false, null) | Lifetime of object             | Each object has its own copy              |
| **Static/Class** | Inside a class, with `static` keyword | Accessible via class or object | Yes (0, false, null) | Lifetime of the class          | Shared across all objects                 |

##### Primitive vs Reference Variables
- **Primitive variables**: Store actual values. (`int`, `float`, `char`, `boolean`)
- **Reference variables**: Store the address of objects. (`String`, custom objects, arrays)

##### Variable Modifiers
- final → constant (value cannot change)
- static → class-level variable
- transient → not serialized
- volatile → visibility guarantee in multithreading
> Tricky point: `final` objects cannot change the reference, but their internal state can be modified.

##### Initialization
- **Local variables**: Must be explicitly initialized.
- **Instance/static variables**: Can be initialized explicitly or get default values.
- **Static block**: Used for static variable initialization.

##### Type Casting / Conversion
- Widening (implicit): `int → long → float → double`
- Narrowing (explicit): `double → float → long → int`
```JAVA
int x = 10;
double y = x; // implicit widening
double z = 12.34;
int w = (int) z; // explicit narrowing
```

##### Scope & Shadowing
- Local variable can shadow instance variable with the same name.
- Static method cannot directly access instance variables.
---
## Operator
##### Types of Operators in Java
> <img width="1070" height="707" alt="image" src="https://github.com/user-attachments/assets/7f1172bf-70dd-43a6-8375-f45bd4f43531" />

#### Ternary operator
> variable = (condition) ? valueIfTrue : valueIfFalse;

#### instanceof Operator
- Checks whether an object belongs to a given class.
```JAVA
String s = "Hello";
System.out.println(s instanceof String); // true
```

#### compound assignment operator: +=, -= etc 
- In compound assignment operator implicit casting happens automatically if required.

#### Bit-wise operator:
> <img width="1568" height="775" alt="image" src="https://github.com/user-attachments/assets/bc4d0a9d-6584-417b-afda-1423d8dddc73" />

- operation cannot be done on decimal numbers.

##### NOTE:
> `==` compares the reference address of the comparing values.
> Short-circuit evaluation means that in Java’s logical operators `&& (AND)` and `|| (OR)`, the second condition is evaluated only if necessary.
> Unsigned right shift `(>>>)` is used mainly in bitwise operations, encryption, compression, and low-level data processing.
---

## printf 
- It is a formatted output method.
- By the help of it we can control how the values will appear when printed(width, decimals, alignment, symbols).
- Example:
```JAVA
public class Main
{
	public static void main(String[] args) {
		int a = 2;
		int b = 3;
		String c = "sum";
		
	System.out.printf("%s of %d & %d : %d", c,a,b,a+b);		
	}
}
```
- Format Specifiers
	- `%d` is the placeholder of integer.
	- `%s` is the placeholdet of string
	- `%c` for char
	- `%f` for float(if %f is used, then after decimal six digits will be there)
	- `%b` is for boolean
	- `%e` for exponential format
 	- `%.2f` → float with 2 decimal places
  	- `%n` → newline (use instead of `\n` inside printf as `%n` is platform-independent) 

##### Q: Why we need it:
- `println` just prints the value directly with no formatting.
- `printf` is used when the exact formatting matters (numbers, tables, currency, alignment).

##### Q: When printf is better:
- printing decimal numbers with controlled precision.
- printing formatted tables/columns.
- creating clean output layouts.

##### Q: Width & Alignment
```JAVA
System.out.printf("%5d", 7);   // pads spaces → "    7"
System.out.printf("%-5d", 7);  // left-align  → "7    "
```
##### Locale-dependent formatting:
- `printf` uses default locale. That affects decimal separator.
> <img width="3202" height="1557" alt="image" src="https://github.com/user-attachments/assets/69265991-8cc6-4307-891a-c0776d29b9cc" />

##### Points to remember:
- `printf` returns a `PrintStream`, not void which means chaining is possible. Isn't commonly used
 ```JAVA
System.out.printf("A").printf("B");
```
-  %f, Java treats the value as double by default
```JAVA
System.out.printf("%f", 3.14);   // valid (double)
System.out.printf("%f", 3.14f);  // also valid, float auto-promotes to double
```
-  If the datatype and specifier don’t match, Java won’t compile.
-  This compiles but throws runtime exception:
> <img width="813" height="112" alt="image" src="https://github.com/user-attachments/assets/f20a775c-9631-4ca8-9367-0299a26344bf" /><br/>
> Output: <img width="944" height="96" alt="image" src="https://github.com/user-attachments/assets/85a64b98-cd9a-43a6-9b24-3d8a0837842e" />

Because format specifiers must match argument count.
- String.format() → Same as printf but returns a String
```JAVA
String s = String.format("Value: %.2f", 3.14159);
System.out.println(s);
```
###### Q: When should you use String.format instead of printf?”
> Use String.format when we need formatted output stored as a string, not printed directly.

##### NOTE: Interview
> printf is used for formatted output. It allows control over precision, width, alignment, and display format. Use it when output needs specific formatting, especially for tables and numeric formatting. println is enough for simple output.

---
## Conditional Statements
- `if`
```JAVA
  if(condition)
	{ // statement}
```
- `if-else`
```JAVA
  if(condition)
	{ // statement}
  else
	{ // statement}
```
- `else if`
```JAVA
  if(condition)
	{ // statement}
  else if(condition)
	{ // statement}
  else
	{ // statement}
```
- `switch`
```JAVA
switch(variable)
{
  case 1: // statement break;
  case 2: // statement break;
  "
  "
  "
  default:
  // statement
}
```

#### Nested if's
- Nested if creates depth-based branching, not linear checks.
- Inner conditions are gated by outer conditions.
- JVM generates multiple jump instructions, each inside another.
- The execution path tree becomes hierarchical, not sequential.
- It enforces logical dependency, not mutual exclusivity.

#### Key Points
1. Nested if = dependency
	- Condition 2 makes sense only if condition 1 is true.
2. Else-if ladder = alternatives
	- Only one branch should execute.
3.Else-if stops evaluating after first match
	- Nested if does not.
4. Else-if improves readability and avoids unnecessary nesting
5. Using nested if when you need else-if is a logic error
	- You will check wrong conditions or execute wrong branches.
6. Unlike `switch`, there is no lookup table or hash-based dispatch hence execution flow is strictly `linear — O(n)`.

#### Interview ready answer for:
###### Q.What is conditional statements and why do we need them
> Conditional statements are control-flow mechanisms that decide which block of code executes based on a boolean expression. In Java, they include if-else, else-if chains, and switch.<br/><br/> if-else is used for complex boolean logic, range checks, and multi-condition validations. It supports relational and logical operators, making it suitable when the decision depends on expressions rather than fixed values.<br/><br/> switch is used when decisions are based on discrete constant values (like enums, integers, or Strings). The compiler optimizes many switch statements internally using tables or hash-based dispatch, which makes them faster and more readable than long if-else chains.<br/><br/> Conditional statements are needed to enforce program correctness, guard against invalid states, perform input validation, and control the execution path depending on runtime data. Modern Java also provides enhanced switch expressions, which eliminate fall-through and return values directly, improving safety and maintainability.

###### Q.Why not just multiple ifs? (critical point interviewers check)
Multiple if statements:
- evaluate every condition
- can execute multiple blocks
  
Else-if ladder:
- stops evaluating after the first true condition
- guarantees only one block runs

### switch
Older switch statement:
> <img width="1735" height="1480" alt="image" src="https://github.com/user-attachments/assets/ae95a699-fa9f-442a-bd87-900f2aa2aad9" />

Enhanced switch statement:
> <img width="1701" height="646" alt="image" src="https://github.com/user-attachments/assets/833a1793-9558-4124-bb9c-037d09d49d3c" />
> In enchanced switch statement `break` is there after every case(by default).

eg: older switch v/s enhanced switch
> <img width="1685" height="1442" alt="image" src="https://github.com/user-attachments/assets/4839235a-9914-4453-a230-b69a9682c173" />

--- 
## LOOPs
> A loop repeatedly executes a block of code as long as a specified condition remains true. It is used to handle repetitive tasks, iterate over data structures, and avoid code duplication.
##### Why Do We Use Loops?
- Repetition without redundancy: Avoids writing the same code again and again.
- Automates repetitive tasks: Process arrays, lists, or other data structures easily.
- Dynamic execution: Works for unknown or changing number of iterations.
- Efficiency & readability: Makes code compact, easier to maintain.

##### Types of Loops in Java
| Loop       | Description                                             | When to Use                                  |
| ---------- | ------------------------------------------------------- | -------------------------------------------- |
| `for`      | Executes a block a known number of times                | Iterating over arrays, counters              |
| `while`    | Executes as long as a condition is true                 | When number of iterations unknown in advance |
| `do-while` | Executes block **at least once**, then checks condition | When block must run at least once            |

##### Syntax:
- for loop
> A for loop is used when the number of iterations is known or predictable. It gives tight control over initialization, condition-checking, and increment in a single line, making it ideal for indexed iteration—especially over arrays or for counter-based logic.
```JAVA
for(intialization; condition; updation)
{ \\ statement}
```
- while loop
> A while loop is used when the number of iterations is not known upfront. It keeps running as long as a condition remains true, making it suitable for scenarios where the stopping point depends on dynamic runtime conditions.
```JAVA
while(condition)
{ \\ statement}
```
- do while loop
> A do-while loop guarantees at least one execution because the condition is evaluated after the body runs. It's appropriate when the first execution is mandatory before any condition check—for example, menus or user-input-driven flows.
```JAVA
do
{\\ statement}
while(condition)
{ \\ statement}
```
- for-each loop(enhance for loop)
> An enhanced for loop is used for simplified iteration over arrays or collections when you don't need the index. It improves readability and eliminates boilerplate, but doesn't allow modifying the underlying collection structure or accessing the index directly.
> <img width="3040" height="1178" alt="image" src="https://github.com/user-attachments/assets/33b577c1-9800-444f-9d95-2e15612d84f3" />
- limitations:
	- It cannot:
 		- modify the underlying collection
		- access index
  		- iterate backwards
    	- remove elements directly 
```JAVA
for(datatype index:variable_name)
{ \\ statement}
```

###### Difference between break vs continue.
- break → exits the loop
- continue → skips current iteration

###### Loop labels
- Used to break out of outer loop directly.
```JAVA
outer:
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < 5; j++) {
        if (j == 2) break outer;
    }
}
```

###### Iterator vs For-Each
Ques: Why can’t you remove an element from a list inside a for-each loop?
>Because the underlying iterator in for-each is hidden, and removing causes `ConcurrentModificationException`.
Correct approach:
```JAVA
Iterator<String> it = list.iterator();
while(it.hasNext()) {
    if (condition) it.remove();
}
```

###### Loop optimization
Why avoid heavy logic inside loops?
→ Performance. Loops run repeatedly; inefficiency multiplies.

#### Ques: <img width="166" height="218" alt="image" src="https://github.com/user-attachments/assets/640e9db2-15c4-47bc-bc4e-1c2ca92ca6e2" /><br/>
Approach:
> 1st:<br/><img width="1203" height="640" alt="image" src="https://github.com/user-attachments/assets/cf2aa894-a575-4840-8a68-19795187ab18" /><br/><br/>2nd:<br/><img width="2298" height="1248" alt="image" src="https://github.com/user-attachments/assets/6bdb1d5c-8aef-4aac-953b-d83a193755a0" />

#### Ques: Can we create an infinite loop?
- for loop
```JAVA
for(;;) {}
```
- while loop
```JAVA
while(true) {}
```
###### NOTE: Empty loop causing logic error
```JAVA
while(i < 5); // BAD
```
#### Which Loop to Use When
| Loop Type    | When to Use                             | Pros                           | Cons                                              | Example                                                  |
| ------------ | --------------------------------------- | ------------------------------ | ------------------------------------------------- | -------------------------------------------------------- |
| **for**      | Known number of iterations              | Clear syntax, index available  | Slightly verbose for unknown iterations           | `for(int i=0;i<10;i++) System.out.println(i);`           |
| **while**    | Unknown iterations, condition-driven    | Simple, checks condition first | Risk of infinite loop if condition not updated    | `while(!input.equals("exit")) input=scanner.nextLine();` |
| **do-while** | Run at least once, then check condition | Guarantees 1 execution         | Condition checked after execution, easy to forget | `do { choice=scanner.nextInt(); } while(choice!=0);`     |
| **for-each** | Iterating arrays or collections         | Clean, no index required       | Cannot modify array elements directly, no index   | `for(int n: nums) System.out.println(n);`                |

##### Quick Tips / Rules
1. Off-by-one error check: for(int i=0;i<arr.length;i++) ✅
2. Short-circuit loops: Prefer for-each for read-only iteration.
3. Infinite loop prevention: Ensure loop condition eventually becomes false.
4. Formatted output in loops: Use printf("%-10s %d%n", name, age);

#### practice
1. Always check start, end, and increment/decrement to avoid off-by-one errors.
2. Know difference between for, while, do-while, and for-each.
3. Be ready to explain why you would use one over the other.
4. Nested loops: Watch out for O(n²) behavior; explain in interviews.
5. Expect output prediction questions, e.g., nested loops, off-by-one, infinite loops.

---
## String

 
