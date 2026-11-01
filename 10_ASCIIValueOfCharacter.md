# Program 10 — ASCII Value of a Character

| Field | Value |
|-------|-------|
| Program Number | 10 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `10_ASCIIValueOfCharacter.cpp` |

---

## 1. Aim

To read a single character from the user and print both the character itself and its ASCII value, demonstrating the implicit conversion between `char` and `int` in C++.

---

## 2. Concepts Used

- `char` data type and character literals
- Reading a single character with `cin >> ch`
- Implicit `char ↔ int` conversion (integer promotion)
- The ASCII table (American Standard Code for Information Interchange)
- Explicit cast `(int)ch` and `(char)n`

---

## 3. Problem Statement

Write a C++ program that reads a character from the user and prints the character itself and its ASCII value.

---

## 4. Algorithm

1. Declare a `char` variable `ch`.
2. Prompt and read `ch` with `cin >> ch`.
3. Print `ch` as a character.
4. Print `(int)ch` to show its ASCII code.
5. Also print the *next* character `(char)(ch + 1)` for illustration.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    char ch = '\0';

    cout << "Enter a character: ";
    cin  >> ch;

    cout << "Character : " << ch                << "\n";
    cout << "ASCII code: " << (int)ch           << "\n";
    cout << "Next char : " << (char)(ch + 1)
         << " (ASCII "    << (int)(ch + 1)      << ")\n";

    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `char ch = '\0';`

A `char` variable is declared and initialized to the null character `'\0'` (ASCII 0). Characters use **single quotes**; the backslash `\0` is an escape sequence for "null character". Initializing to `\0` is safer than leaving `ch` uninitialized.

### `cin >> ch;`

`cin` reads a single non-whitespace character into `ch`. Important: `cin >>` skips leading whitespace (spaces, tabs, newlines) by default. If you actually want to read a space character, you must use `cin.get(ch)` instead — that reads whatever is next in the stream, including whitespace.

### `cout << "Character : " << ch << "\n";`

When you print a `char` with `cout`, you get the character itself — `A` for `'A'`, `5` for `'5'`, `+` for `'+'`.

### `(int)ch` — explicit cast to int

This is the heart of the program. Writing `(int)ch` tells the compiler to **interpret the byte stored in `ch` as an integer**. Because `char` and `int` are both integer types, the conversion is automatic (implicit) — you could even write `cout << ch + 0` and get the same effect, because adding `0` triggers **integer promotion**. But the explicit cast `(int)ch` makes the intent obvious to the reader.

For the character `'A'`, the ASCII code is `65`; for `'a'` it is `97`; for `'0'` it is `48`; for a space `' '` it is `32`.

### `(char)(ch + 1)` — back to char

Adding `1` to a `char` produces an `int` (because of integer promotion). Casting the result back to `char` with `(char)` lets us print it as a character again. For input `'A'`, `ch + 1` is `66`, which when printed as a char gives `'B'` — the next letter in the alphabet.

This trick — arithmetic on character codes — is the basis of all simple ciphers (Caesar cipher, ROT13) and case conversion.

---

## 7. Sample Input / Output

```
$ ./10_ASCIIValueOfCharacter
Enter a character: A
Character : A
ASCII code: 65
Next char : B (ASCII 66)
```

Some useful ASCII values to remember:

| Char | ASCII | Char | ASCII |
|------|-------|------|-------|
| `'0'`–`'9'` | 48–57 | `'A'`–`'Z'` | 65–90 |
| `' '` (space) | 32 | `'a'`–`'z'` | 97–122 |
| `'\n'` (newline) | 10 | `'\0'` (null) | 0 |

---

## 8. Real-World Application

Character ↔ code conversion is used in:

- **Cryptography**: Caesar cipher shifts each letter by N: `cipher = (char)(plain + key)`. ROT13 is the special case `key = 13`.
- **Case conversion**: `'A'` and `'a'` differ by exactly 32; `toupper(c) = c - 'a' + 'A'`.
- **Lexical analysis in compilers**: every scanner reads characters and classifies them by ASCII range (digit, letter, operator).
- **Password hashing**: characters are converted to their codes and mixed into a hash.
- **Text encoding**: UTF-8 encodes Unicode codepoints as sequences of bytes; the bytes are read as `unsigned char`.
- **Serial protocols**: a microcontroller receiving bytes from UART treats each byte as either a `char` or an `unsigned char` depending on whether it represents text or raw data.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Reads multiple characters into one `char` | User typed "Hello"; only `'H'` read | That's expected — `char` holds exactly one character |
| Cannot read a space | `cin >>` skips whitespace | Use `cin.get(ch)` to read any byte including space |
| `cout << ch + 0` prints a number, not a char | Integer promotion kicked in | Cast back: `(char)(ch + 0)` or just `ch` |
| Wrong case conversion | Forgot that `A` is 65 and `a` is 97 | Use library functions `toupper`/`tolower` from `<cctype>` |
| Garbage for non-ASCII input (e.g. `é`) | `char` is signed on many systems; values > 127 become negative | Use `unsigned char` for raw bytes |
| Confusion with UTF-8 | UTF-8 is multi-byte; one `char` is one byte, not one "character" | Use `wchar_t`, `char32_t`, or a UTF-8 library for Unicode |

---

## 10. Practice Question

Read a **lowercase** letter and print its **uppercase** equivalent using the ASCII relationship. Verify with the library function `toupper`.

```cpp
#include <cctype>

char lower, upper;
cin >> lower;

// Manual conversion using ASCII arithmetic:
upper = (char)(lower - 'a' + 'A');

cout << "Manual      : " << upper << "\n";
cout << "Library call: " << (char)toupper(lower) << "\n";
```

Try inputs `a`, `z`, `m` and confirm both methods give the same result. What happens for input `'A'` (already uppercase)? Why?
