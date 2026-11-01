# Program 01 — Hello World

| Field | Value |
|-------|-------|
| Program Number | 01 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `01_HelloWorld.cpp` |

---

## 1. Aim

To write, compile and execute the first C++ program that prints a greeting message on the screen, and to understand the basic structure of every C++ program.

---

## 2. Concepts Used

| Concept | What it means |
|---------|---------------|
| `#include` | Preprocessor directive that copies a header file into the source before compilation |
| `<iostream>` | Standard header that declares `cin`, `cout`, `cerr`, `endl` |
| `using namespace std` | Lets us write `cout` instead of `std::cout` |
| `main()` | The function where operating system starts executing the program |
| `cout` | Standard output stream object, attached to the console |
| `<<` | Stream insertion operator — pushes data into `cout` |
| `endl` | Inserts a newline and flushes the output buffer |
| `return 0` | Signals successful termination to the operating system |

---

## 3. Problem Statement

Write a C++ program that displays the message **`Hello, World!`** on the standard output.

---

## 4. Algorithm

1. Include the input-output stream header `<iostream>`.
2. Bring the standard namespace `std` into scope.
3. Define the `main()` function — the program's entry point.
4. Inside `main()`, use `cout` to print `Hello, World!`.
5. End the line with `endl` and `return 0` to indicate success.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello, World!" << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `#include <iostream>`

This is a **preprocessor directive**. The `#` symbol tells the compiler's preprocessor to run this line *before* actual compilation. `#include <filename>` literally copies the contents of the named header file into your source code. `<iostream>` is the standard C++ header that declares the input/output stream objects `cin` (console input), `cout` (console output), `cerr` (error output) and `endl` (newline + flush). Without this line, the compiler would not know what `cout` is.

### `using namespace std;`

C++ groups names (functions, classes, variables) into containers called **namespaces** to prevent name clashes in large projects. Everything in the standard library lives inside the namespace `std`, so the full name of `cout` is actually `std::cout`. Writing `using namespace std;` "imports" the entire `std` namespace into the current file so that we can simply write `cout`. The semicolon `;` ends the statement — every C++ statement must end with a semicolon.

### `int main()`

This declares the **main function**. Every C++ program must have exactly one `main()` — the operating system calls it when the program starts. `int` before `main` says this function returns an integer to the OS. The empty parentheses `()` mean the function takes no arguments.

### `{` … `}`

These curly braces mark the **body** of `main()`. Everything between them is what the function executes.

### `cout << "Hello, World!" << endl;`

This is the heart of the program:

- `cout` — the standard output stream object; it represents the console.
- `<<` — the **stream insertion operator**. It sends the value on its right into the stream on its left. You can chain it: `cout << a << b << c;`
- `"Hello, World!"` — a **string literal** enclosed in double quotes. C++ does not have a built-in string type for literals; this is a C-style `const char[15]` that the stream library knows how to print.
- `endl` — a **manipulator** that inserts a newline character `\n` *and* flushes the output buffer so the text appears immediately.

### `return 0;`

Returns the integer `0` to the operating system. By convention, `0` means "the program finished successfully"; any non-zero value indicates an error. Modern C++ allows you to omit `return 0;` in `main()` only — the compiler inserts it implicitly — but writing it explicitly is good practice.

---

## 7. Sample Input / Output

```
$ ./01_HelloWorld
Hello, World!
```

No input is required by this program.

---

## 8. Real-World Application

Every C++ project — be it an operating system kernel module, a game engine, a desktop application, or a firmware controller for an embedded device — begins from this minimal structure of `#include`, `main()`, and I/O. The "Hello World" program is the **canonical smoke test** used worldwide to verify that the compiler toolchain (preprocessor, compiler, linker, runtime) is correctly installed and working.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `expected ';' before '}'` | Missing semicolon after `cout` statement | Add `;` at the end of every statement |
| `'cout' was not declared` | Forgot `#include <iostream>` or `using namespace std;` | Add both lines, or write `std::cout` |
| `'Cout' was not declared` | C++ is case-sensitive; `Cout ≠ cout` | Use lowercase `cout` |
| `#include <iostream.h>` error | Old Turbo C++ style, removed in modern C++ | Use `<iostream>` (no `.h`) |
| `'Hello' was not declared` | Used single quotes `'Hello'` (char literal) instead of double quotes | Always use `"..."` for strings |

---

## 10. Practice Question

Modify the program to print your **full name** and your **college name** on two separate lines using a single `cout` statement.

**Hint:** You can chain `endl` between two strings:

```cpp
cout << "My Name" << endl << "My College" << endl;
```
