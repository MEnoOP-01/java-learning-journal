# String

### :question: What is String?
A String is an `immutable`, `final class` in Java representing a `character sequence stored in heap memory` with a special memory optimization mechanism called the `String constant pool`. Its immutability ensures thread-saftey, supports hashcode caching, and enables safe use as map keys or constants."

##### :black_nib: Key points an interviewer expects:
- In java string is a class(not a primitive but reference type).
- String literals are just a sequence of characters stored as character of array by JVM.
- Immutable in nature. Any modification creates a new object.
- String literals are stored in string contant pool.
- Internally backed by a char[] (till Java 8) or byte[] + coder flag (Java 9+). ------> **doubt** ❓ 

### :question: Why do we need Strings
> String immutability enables `hashcode caching`, safe use in `hash-based collections`, security for `class loading`, `credentials`, and `thread safety`.

> [!NOTE]
> Difference between `==` and `.equals()`
> - `==` only compares the reference address of the objects.
> - `.equals() compares each char and case(lowercase/uppercase).
> Example:
> <img width="1203" height="353" alt="image" src="https://github.com/user-attachments/assets/76961081-df8b-4d83-9162-31745db1fd1f" />
> The output if false as the first time we declared string "Hello", it got stored in special memory location in the heap which are for unique string literals(i.e. String Pool).<br/>
> And when the second time String "Hello" is declared it was save


## :label: String Pool(Intern Pool):
**Special memory region in the heap, storing unique string literals.**<br/>
Example:
```JAVA
String a = "hello";
String b = "hello";
```
> If a 




#### Two ways of declaring string
> <img width="2505" height="827" alt="image" src="https://github.com/user-attachments/assets/5777e2a2-4fa8-47a8-9198-301d8b7f9b27" />
