# Unicode → UTF-16 → char → code points → surrogate pairs

## 1. Why text is complicated (The root problem)
- Computers store everything as numbers, not letters.
> <img width="576" height="842" alt="image" src="https://github.com/user-attachments/assets/057847c7-1355-4fa4-8916-201a54a8d2fd" />
- The problem > Different languages have thousands of symbols, not just A–Z.

## 2. What is Unicode?
- Unicode is a **global dictionary** that assigns a **unique number** to every character in every language.
```
OR
Unicode provides a unified, language-agnostic code space so all characters across scripts, symbols, and emoji have unique, stable identifiers (code points).
```
- Examples:

| Character | Unicode Code | Meaning          |
| --------- | ------------ | ---------------- |
| A         | U+0041       | English letter A |
| क         | U+0915       | Hindi Ka         |
| 中         | U+4E2D       | Chinese Zhong    |
| 😊        | U+1F60A      | Smiling emoji    |

## 3. What is a Code Point?
- A code point is simply the ID number assigned by Unicode.
  - “A” → U+0041
  - “😊” → U+1F60A
- Code Points v/s Code Units > key distinction
  - Code point = actual Unicode character (numeric identity).
  - Code unit = storage unit of an encoding (in Java: 16-bit `char`).
  - Example:
    - `'A'` → one code unit.
    - `'😊'` → one code point, but **two** code units → surrogate pair.
  - Analogy
    - Code point = the item itself.
    - Code unit = the shelf space used to store it. 

##### <ins>Analogy</ins>
```
Code point = an Aadhaar number for every character.
It uniquely identifies the character.
```

## 4. How Java stores characters (UTF-16)
- Unicode is just the dictionary.
- Java must decide how many bytes to use to store these numbers.
- Java chose UTF-16:
  - Most characters → stored in 2 bytes (16 bits)
  - Some characters → need 4 bytes (16 + 16 bits)
- Java uses **char** to store **one 16-bit unit**.

## 5. Why some characters need two chars (Surrogate Pairs)
- UTF-16 can store values up to **65535** (2 bytes).
- Emoji and many special characters are **bigger numbers** (e.g., 128512).
- So they don’t fit in one `char`.
- Solution → **use two 16-bit pieces**:
  - High surrogate (1 char)
  - Low surrogate (1 char)
- Together → **one real character**.
- To understand in better way:
```
Characters > U+FFFF are encoded as:
 High surrogate: range D800–DBFF
 Low surrogate: range DC00–DFFF
Together, they form a single Unicode scalar value.

:bricks: Analogy:
A large package is split into two labeled crates (high + low).
Only together do they represent the actual product.
```

##### <ins>Analogy</ins>
```
💠 Most guests fit into one chair.
💠 Some guests are big bodybuilders → need two chairs.
The two chairs = surrogate pair.
```
## 6. Why `"😊".length() == 2` in Java
- `.length()` counts **char units**, not characters
  - Normal character = 1 char
  - Emoji = 2 chars (surrogate pair)
- So > `"😊".length() == 2`

##### <ins>Analogy</ins>
```
.length() is counting chairs, not people.
An emoji person uses two chairs, so count = 2.
```

## 7. Code Unit vs Code Point (Important)
| Concept        | Explanation                           | Analogy                    |
| -------------- | ------------------------------------- | -------------------------- |
| code unit      | one 16-bit chunk (Java `char`)        | one chair                  |
| code point     | actual Unicode character              | actual guest               |
| surrogate pair | two chars representing one code point | one guest using two chairs |

## 8. How to count actual characters correctly
- Since .length() counts chars, not true characters:
- Use > `str.codePointCount(0, str.length())` > This counts code points (real characters).

##### <ins>Analogy</ins>
``` 
This counts people, not chairs.
```
## 9. Charset (important but simple)
- A **charset** tells how **bytes ↔ characters are converted**.
- Common ones:
  1. UTF-8
  2. UTF-16
  3. ISO-8859-1

##### <ins>Analogy</ins>
```
A charset is like choosing a language to write your book.
Same story, but different scripts.
```

## 10. Putting It ALL Together (Story Analogy)
### Think of a hotel:
- Unicode = list of all possible guests in the world
- Code point = each guest's passport number
- UTF-16 = hotel management rule:
  - “Each room has 1 chair; some guests need 1 chair, big guests need 2 chairs.”
- Java char = one chair
- Surrogate pair = two chairs reserved together
- `.length()` = count chairs
- `codePointCount()` = count guests 

## Think of Java as an apartment building.
- Each apartment = one char (16 bits)
- Most people = normal characters → fit into one apartment
- Some people = very large people (emoji) → cannot fit into 1 apartment
- So Java does this: > “Give this big person 2 apartments next to each other.”
  - First apartment = high surrogate
  - Second apartment = low surrogate
  - Person = one emoji
  - Even though it's one person, they occupy two apartments.
