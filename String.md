# String

### :question: What is String?
> A String is an `immutable`, `final class` in Java representing a `character sequence stored in heap memory` with a special memory optimization mechanism called the `String constant pool`<ins>(SCP for literals)</ins>. Its immutability ensures thread-saftey, supports hashcode caching, and enables safe use as map keys or constants."

#### :gear: Analogy
```
Think of a String as a sealed, laminated document.
You can read it, copy it, pass it around, but you cannot erase or modify the letters on it. Any “change” gives you a new laminated copy.
```
##### :black_nib: Key points an interviewer expects:
- In java string is a class(not a primitive but reference type).
- String literals are just a sequence of characters stored as character of array by JVM.
- Immutable in nature. Any modification creates a new object.
- String literals are stored in string contant pool.
- Internally backed by a char[] (till Java 8) or byte[] + coder flag (Java 9+). ------> $\\color{red}isn't\\ clear$ ❓ 

### :brain: Two ways of declaring string
> <img width="1798" height="344" alt="image" src="https://github.com/user-attachments/assets/124115a2-8dba-40e0-b144-282ae0e8ea60" />
- **<ins>Analogy</ins>**
  - Literal = borrowing a book from a public library shelf.
  - new String = buying your own new book even if the library already has one.

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
> - `==` only compares the reference address(memory references) of the objects.(In short compares references)
> - `.equals()` compares each character and case(lowercase/uppercase).(In short compares content)
> - Example:
> <img width="1203" height="353" alt="image" src="https://github.com/user-attachments/assets/76961081-df8b-4d83-9162-31745db1fd1f" /> <br/>
> - Using `==` returns `false` because the references are not the same.
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
  > - Because strings are immutable, hashcode can be cached, improving lookup performance. <br/>
  > - **<ins>Analogy</ins>:** If the name on your locker changed randomly, you’d never find your locker again. A stable label (= immutable string) prevents chaos. 

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
## :books: Internal Representation (Java 8 vs Java 9+)
- **<ins>Java 8 and earlier</ins>**
```JAVA
private final char[] value;
```
- Each char = 2 bytes (UTF-16).
- **<ins>Java 9+ (Compact Strings)</ins>**
```JAVA
private final byte[] value;
private final byte coder; // 0 = Latin-1, 1 = UTF-16
```
- JVM stores Strings more compactly, saving 30–50% memory for ASCII/LATIN characters.

#### :gear: <ins>Analogy</ins>
> Think of storing notes: <br/>
> - Before Java 9 → always store each letter in a big notebook page (2 bytes).
> - After Java 9 → if letters are small (ASCII), use a sticky note (1 byte) instead.

---
## :books: String Pool(or Intern Pool or String Constant Pool):
- **Special memory region in the heap, storing unique string literals to optimize memory usage.**
- When a string literal is created, JVM first checks the pool:
  - If the value already exists, JVM reuses the same object.
  - If not, the value is stored in the pool and reused for future identical literals.
- Example:Memory management when string is created using new keyword:<br/>
> <img width="1270" height="182" alt="image" src="https://github.com/user-attachments/assets/14ab8925-d120-489a-a3ba-4862d52bb04e" /> <br/>
> This creates:
  > - "Java" in the String Pool (if not already there).
  > - new String("Java") → heap object + optional pool entry
- **<ins>Analogy:</ins>**
```
SCP = Library shelf with only one copy of each book.
intern() = “Check if this book is already in the library; if yes, give me that existing copy.”
```

#### :question: When does String NOT go to the pool?
**1. <ins>When created using `new String("...")`</ins>**
```JAVA
String str = new String("java");
```
- As here `java` is a literal it will be stored inside string pool.
- While the `new object` created by `new String("...")` will be stored inside the heap memory.
- And `str` will point to the heap as it's storing the address of string object stored in heap memory.
- **Key point:**
  - new keyword always creates a non-pooled String object.
- **<ins>Analogy:</ins>**
> Literal = one copy kept in the library.<br/>
> new String() = photocopy of the book you keep at home.

**2. <ins>When a String is created at `runtime (not a compile-time constant)`</ins>**
```JAVA
String a = "ab";
String b = a + "c";     // runtime concatenation → heap
```
- a + "c" is evaluated at runtime, so the result ("abc") is heap, not pool.
- **<ins>Analogy:</ins>**
> If the book title is known at compile time → library stores 1 copy.<br/>
> If you construct the title dynamically → library can’t store it.

**3. <ins>When String formed by `+` operator `if operands are not all literals`</ins>**
```JAVA
String x = "a" + 10;     // compile-time constant → SCP (exception)
String y = x + 10;       // x is a variable → runtime → heap
```
- If any operand is a variable, it becomes runtime → heap.

**4. <ins>When a String is created using `StringBuilder` or `StringBuffer`</ins>**
```JAVA
StringBuilder sb = new StringBuilder();
sb.append("hello");
String s = sb.toString();
```
- This final `toString()` string is always a new heap object.
- It doesn't automatically enter the pool.

**5. <ins>Strings created  `using any API` that allocates new objects</ins>**
```JAVA
substring()
concat()
replace()
trim()
toUpperCase()
toLowerCase()

```
- They generally produce new heap string, unless they return the same reference (optimization).

**6. <ins>Strings deserialized from objects</ins>**
```JAVA
ObjectInputStream → heap object
```

**7. <ins>Strings loaded from external sources</ins>**
- User input
- File read
- Network I/O(response)
- Database fetch
- Scanner, BufferedReader, Properties(JSON/XML parsing)
```
These strings are always heap objects.
As Only compile-time constants are automatically pooled.
Java cannot pool what it cannot know at compile time.
```
###### :label: Quick Table
| Expression          |     SCP     |          Heap          |
| ------------------- | :---------: | :--------------------: |
| `"abc"`             |      ✓      |            ✗           |
| `new String("abc")` | ✓ (literal) |     ✓ (new object)     |
| `"a" + "b" + "c"`   |      ✓      |            ✗           |
| `a + "b"`           |      ✗      |            ✓           |
| User input          |      ✗      |            ✓           |
| `"abc".intern()`    |      ✓      | ✗ (no new heap object) |


##### :question: Interning
- A heap string can be forced into the pool by using `.intern()`.
- `.intern()` returns the pooled reference.
> <img width="1270" height="182" alt="image" src="https://github.com/user-attachments/assets/60a6cbf8-9680-43cc-b412-445ed3ac054e" /><br/>

Example to understand string pool better
> <img width="1872" height="628" alt="image" src="https://github.com/user-attachments/assets/30f68c93-4e14-45f8-a656-1732132f3ad6" />
> <img width="1527" height="1014" alt="image" src="https://github.com/user-attachments/assets/abee1ebf-e35e-4235-a36c-605156549df0" />

##### :question: Why String Pool Exists?
- Strings are very common (file paths, DB URLs, JSON, API calls).
- Pooling:
  - Saves memory by avoiding duplicates.
  - Improves performance due to reuse and cached hashcode.
 
### <ins>Mental Analogy</ins>:
- Think of SCP as a “government-issued ID database”:
  > - Only official constants get stored there
  > - One unique copy per value
- Heap is like:
  > - Everyone printing their own duplicate ID cards
  > - Many copies exist, wasteful but allowed

---
## :books: Unicode, Charset, Code Points
### 1. Why char Is Not Enough
- `Java uses UTF-16 internally` OR Java `char` is **16-bit** → can represent only **Unicode Basic Multilingual Plane (BMP)** (0–65535).. 
- Modern characters (emoji, rare scripts) require more than 16 bits(2 byte).
- Emoji, some Asian characters need 2 chars → “surrogate pairs”.

- Important APIs
  - codePointAt()
  - codePoints()
  - offsetByCodePoints()

##### <ins>Analogy</ins>
```
Some characters are “big emoji stickers” that don’t fit into a single cell in a grid. They occupy 2 cells.
Emoji are “big characters”, so Java joins two grids to host them.
```
### 2. Surrogate Pairs
- Emoji or extended characters > 65535 are stored as:
  - High surrogate
  - Low surrogate
- Together, they form one logical character.

##### <ins>Analogy</ins>
```
💠 Like a VIP guest (emoji) who needs two adjoining rooms.
💠 JVM sees both rooms and treats the VIP as one person.
```

### 3. Why "💖".length() == 2
- .length() counts char units, not visual characters.
- Emoji = surrogate pair → two char units → length = 2.

##### <ins>Analogy</ins>
```
💠 You’re counting rooms, not people.
💠 Emoji occupies two rooms, so .length() reports 2.
```

### 4. Correct Way to Count Actual Characters
- Use code point APIs, not .length():
  - codePointCount(0, str.length())
  - str.codePoints()
  - Character.charCount(codePoint)

##### <ins>Analogy</ins>
```
.length() = count rooms
codePointCount() = count actual guests
codePoints() = list each real guest (emoji included)
```

### 5. Important APIs to Know
| API                    | Purpose                                        |
| ---------------------- | ---------------------------------------------- |
| `codePointAt(index)`   | Get actual Unicode code point (handles emoji)  |
| `codePoints()`         | Stream of Unicode code points                  |
| `offsetByCodePoints()` | Move N characters forward safely               |
| `toCharArray()`        | Returns raw char units (not actual characters) |

##### <ins>Analogy</ins>
```
Think of code points as passport numbers of each guest.
You’re no longer looking at rooms — you’re identifying actual individuals.
```

6. Interview-Ready Summary (You Must Say This)
- Java `char` cannot store many modern characters.
- Emoji require two chars → surrogate pair.
- `.length()` misleads because it counts char units, not characters.
- Use **code point methods** to work with real characters.
