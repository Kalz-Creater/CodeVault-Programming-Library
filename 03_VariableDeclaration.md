# Program 03 — Variable Declaration and Initialization

| Field | Value |
|-------|-------|
| Program Number | 03 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `03_VariableDeclaration.cpp` |

---

## 1. Aim

To understand the primitive data types in C++ and to declare, initialize and print variables of different types using the `sizeof` operator.

---

## 2. Concepts Used

| Type | Stores | Typical size |
|------|--------|--------------|
| `int` | Whole numbers (e.g. `42`, `-7`) | 4 bytes |
| `float` | Single-precision decimal (≈ 7 significant digits) | 4 bytes |
| `double` | Double-precision decimal (≈ 15 significant digits) | 8 bytes |
| `char` | A single character / small integer | 1 byte |
| `bool` | Boolean — `true` (1) or `false` (0) | 1 byte |

Also: variable declaration vs initialization, the `sizeof` operator, the `f` suffix for float literals.

---

## 3. Problem Statement

Declare one variable each of type `int`, `float`, `double`, `char` and `bool`. Initialize them with sample values and print each variable along with its size in bytes using the `sizeof` operator.

---

## 4. Algorithm

1. Include `<iostream>` and bring in the `std` namespace.
2. Declare and initialize variables of all five primitive types.
3. For each variable, print its name, value and size using `cout` and `sizeof`.
4. `return 0`.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int     age     = 42;
    float   pi      = 3.14f;
    double  euler   = 2.71828;
    char    grade   = 'A';
    bool    isPass  = true;

    cout << "Integer  : value = " << age     << ", size = " << sizeof(age)     << " bytes\n";
    cout << "Float    : value = " << pi      << ", size = " << sizeof(pi)      << " bytes\n";
    cout << "Double   : value = " << euler   << ", size = " << sizeof(euler)   << " bytes\n";
    cout << "Character: value = " << grade   << ", size = " << sizeof(grade)   << " byte\n";
    cout << "Boolean  : value = " << isPass  << ", size = " << sizeof(isPass)  << " byte\n";

    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `int age = 42;`

This **declares** a variable named `age` of type `int` (a 32-bit signed integer) and **initializes** it with the value `42`. The compiler allocates 4 bytes of memory and stores the binary representation of 42 there. Variables of type `int` can typically hold values from approximately −2.1 billion to +2.1 billion.

### `float pi = 3.14f;`

A `float` is a **single-precision** floating-point number occupying 4 bytes, giving roughly 7 significant decimal digits. The `f` suffix on `3.14f` is important: without it, `3.14` is treated as a `double`, and assigning a `double` to a `float` may cause a compiler warning about loss of precision.

### `double euler = 2.71828;`

A `double` is a **double-precision** floating-point number occupying 8 bytes, giving roughly 15 significant digits. It is the default choice when you need decimals and is preferred over `float` for most scientific and financial calculations.

### `char grade = 'A';`

A `char` stores a single character in **single quotes**. Internally it stores the ASCII code for `A`, which is 65. Characters and small integers are interchangeable in C++ — `char c = 65;` would also print `A`. Note: `'A'` (single quotes) is a char; `"A"` (double quotes) is a string literal — the two are different types!

### `bool isPass = true;`

A `bool` stores one of two values: `true` or `false`. When printed with `cout`, `true` appears as `1` and `false` appears as `0`. If you want the words "true"/"false", use `cout << boolalpha` before printing.

### `sizeof(age)`

`sizeof` is a **compile-time operator** (not a function) that returns the size in bytes of its operand. The result is a constant of type `size_t`. Using `sizeof` makes your code portable — sizes can differ between platforms (e.g. on some embedded systems, `int` is 2 bytes).

---

## 7. Sample Input / Output

```
$ ./03_VariableDeclaration
Integer  : value = 42, size = 4 bytes
Float    : value = 3.14, size = 4 bytes
Double   : value = 2.71828, size = 8 bytes
Character: value = A, size = 1 byte
Boolean  : value = 1, size = 1 byte
```

No input is required.

---

## 8. Real-World Application

Choosing the right data type is a daily engineering decision:

- **Sensor data** in IoT firmware often fits in a `float` to save RAM.
- **Currency calculations** must use `double` (or a decimal type) to avoid rounding errors — banks care about every digit.
- **Status flags** (on/off, pressed/released) should be `bool`, not `int`, for clarity.
- **Character codes** (`char`) underlie all text processing.
- **Counters and array indices** use `int` (or `size_t` for very large arrays).

Knowing the size of each type matters in embedded systems, network protocols and binary file formats where every byte is laid out explicitly.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `cannot convert 'const char*' to 'char'` | Wrote `char c = "A";` (double quotes) | Use single quotes: `char c = 'A';` |
| `cannot convert 'char' to 'const char*'` | Wrote `cout << 'Hello';` (single quotes around multi-char) | Use double quotes for strings |
| Float warning: "truncation" | Assigned `3.14` (a double) to a float | Add the `f` suffix: `3.14f` |
| `bool` prints as `0`/`1`, not `true`/`false` | Default behavior of `cout` for `bool` | Use `cout << boolalpha` first |
| Size differs from textbook | Sizes are platform-dependent | Use `sizeof` to check on your platform |

---

## 10. Practice Question

Add a variable of type `unsigned int` and one of type `long long`. Print their sizes and try to store a value larger than 2 billion in each (e.g. `3000000000`). Observe what happens if you store a value larger than `INT_MAX` into a plain `int`.

```cpp
unsigned int  bigU  = 4000000000u;
long long     bigLL = 9000000000LL;
```
