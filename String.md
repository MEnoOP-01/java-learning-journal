# String

### :question: What is String?
> A String is an `immutable`, `final class` in Java representing a `character sequence stored in heap memory` with a special memory optimization mechanism called the `String constant pool`. Its immutability ensures thread-saftey, supports hashcode caching, and enables safe use as map keys or constants."

##### :black_nib: Key points an interviewer expects:
- In java string is a class(not a primitive but reference type).
- String literals are just a sequence of characters stored as character of array by JVM.
- Immutable in nature. Any modification creates a new object.
- String literals are stored in string contant pool.
- Internally backed by a char[] (till Java 8) or byte[] + coder flag (Java 9+). ------> $\\color{red}isn't\\ clear$ ❓ 

### :brain: Two ways of declaring string
> <img width="2505" height="827" alt="image" src="https://github.com/user-attachments/assets/5777e2a2-4fa8-47a8-9198-301d8b7f9b27" />

### :question: Why do we need Strings
> We need Strings because applications must work with textual data. A single char only stores one symbol, but Strings allow us to represent meaningful sequences of characters such as names, commands, authentication data, and communication messages. Java provides the String class to handle this efficiently with built-in methods for formatting, comparing, searching, and modifying text.

##### :black_nib: Real-world use cases of Strings:
| Use Case          | Example                            |
| ----------------- | ---------------------------------- |
| User input        | Name, email, password              |
| Communication     | JSON, XML, HTTP requests/responses |
| System operations | File paths, command-line arguments |
| Storage           | Database queries (`SQL`)           |
| UI text           | Buttons, labels, messages          |
| Networking        | URLs, IP addresses, tokens         |


> [!NOTE]
> Difference between `==` and `.equals()`
> - `==` only compares the reference address(memory references) of the objects.
> - `.equals()` compares each character and case(lowercase/uppercase).
> - Example:
> <img width="1203" height="353" alt="image" src="https://github.com/user-attachments/assets/76961081-df8b-4d83-9162-31745db1fd1f" /> <br/>
> - Using  `==` returns `false` because the references are not the same.
> - When the first String "Hello" is created using a string literal, it gets stored in the String Constant Pool (SCP).
> - When the second String is created using new String("Hello"), Java forces the creation of a new String object in the Heap, not reused from SCP.
> - So even though both objects contain the same text "Hello", they have different memory addresses.

---
## :books: String Immutability in Java
### :question: What does immutability mean?
> A String is immutable, meaning once it is created, its value cannot be changed.
> Any operation that seems to modify a string actually creates a new String object.
> Example:
> <img width="1345" height="430" alt="image" src="https://github.com/user-attachments/assets/a0b1e5f2-9277-43cb-9500-48f231839dd4" />
> Here, "FirstNameLastName" is a new object. The original "FirstName" remains unchanged.

### :question: Why are Strings immutable? $\\color{blue}(Real\\ Interview\\ Answer)$
> Strings are immutable for four key reasons:
> 1. Security
  > - Strings are used in sensitive areas: **<ins> passwords, database URLs, file paths, class loading, network protocols </ins>**.
  > - If strings could be modified, malicious code could alter them after being passed to secure functions.
> 2. String Pool Optimization
  > - Because strings do not change, <ins>JVM can safely store and reuse identical values in the String Constant Pool</ins>.
  > - This saves memory and improves performance. 
> 3. Thread Safety
  > - <ins>Immutable objects require no synchronization</ins>.
  > - Strings can be <ins>safely shared across threads without locking</ins>.
>  4. Caching and Hashcode Stability
  > - Strings are often used as keys in maps (HashMap, HashTable).
  > - If their value changed, hashcode would change → map would break.
  > - Because strings are immutable, hashcode can be cached, improving lookup performance.    

##### :black_nib: Benefits Summary:
| Benefit            | Reason                                           |
| ------------------ | ------------------------------------------------ |
| Security           | Strings used in system-level operations          |
| Memory efficiency  | String pool reuses literal values                |
| Thread safety      | No synchronization needed                        |
| Faster collections | Stable hashcode improves performance in HashMaps |

### :brain: Common follow-up question:
> :question: If Strings are immutable, how do we modify text efficiently? <br/>
> For frequent modifications, Java provides `StringBuilder` (non-thread safe but fast) and `StringBuffer` (thread-safe).

---
## :label: String Pool(Intern Pool):
- **Special memory region in the heap, storing unique string literals to optimize memory usage.**
- When a string literal is created, JVM first checks the pool:
  - If the value already exists, JVM reuses the same object.
  - If not, the value is stored in the pool and reused for future identical literals.
##### :question: When does String NOT go to the pool?
> <img width="1270" height="182" alt="image" src="https://github.com/user-attachments/assets/14ab8925-d120-489a-a3ba-4862d52bb04e" /> <br/>
> This creates:
  > - "Hello" in the String Pool (if not already there).
  > - A new String object in heap. 

##### :question: Interning
- A heap string can be forced into the pool by using `.intern()`.
- `.intern()` returns the pooled reference.
> <img width="1270" height="182" alt="image" src="https://github.com/user-attachments/assets/60a6cbf8-9680-43cc-b412-445ed3ac054e" />

> Example to understand string pool better
> <img width="1872" height="628" alt="image" src="https://github.com/user-attachments/assets/30f68c93-4e14-45f8-a656-1732132f3ad6" />
> <img width="1527" height="1014" alt="image" src="https://github.com/user-attachments/assets/abee1ebf-e35e-4235-a36c-605156549df0" />

##### :question: Why String Pool Exists?
- Strings are very common (file paths, DB URLs, JSON, API calls).
- Pooling:
  - Saves memory by avoiding duplicates.
  - Improves performance due to reuse and cached hashcode. 

---

