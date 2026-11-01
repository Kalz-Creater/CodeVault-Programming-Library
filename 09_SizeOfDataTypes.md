# Program 09 — Size of Primitive Data Types

| Field | Value |
|-------|-------|
| Program Number | 09 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `09_SizeOfDataTypes.cpp` |

---

## 1. Aim

To use the `sizeof` operator to determine the size in bytes of every primitive C++ data type, and to understand that sizes are **platform dependent** (the C++ standard fixes minimums, not exacts).

---

## 2. Concepts Used

- `sizeof` operator (compile-time, returns `size_t`)
- All primitive types: `short`, `int`, `long`, `long long`, `float`, `double`, `long double`, `char`, `bool`, `unsigned int`
- Platform dependence of type sizes
- Tabular output with `\t`

---

## 3. Problem Statement

Write a C++ program that prints a table of every primitive data type and its size in bytes on this machine.

---

## 4. Algorithm

1. Include `<iostream>`.
2. Print a header row with column titles.
3. For each primitive type, print `sizeof(type)` next to its name.
4. Use `\t` to align columns.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Data type\t\tSize (bytes)\n";
    cout << "-----------------------------\n";

    cout << "short\t\t\t"         << sizeof(short)         << "\n";
    cout << "int\t\t\t"           << sizeof(int)           << "\n";
    cout << "long\t\t\t"          << sizeof(long)          << "\n";
    cout << "long long\t\t"       << sizeof(long long)     << "\n";
    cout << "float\t\t\t"         << sizeof(float)         << "\n";
    cout << "double\t\t\t"        << sizeof(double)        << "\n";
    cout << "long double\t\t"     << sizeof(long double)   << "\n";
    cout << "char\t\t\t"          << sizeof(char)          << "\n";
    cout << "bool\t\t\t"          << sizeof(bool)          << "\n";
    cout << "unsigned int\t\t"    << sizeof(unsigned int)  << "\n";

    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `sizeof(short)`

`sizeof` is a **compile-time operator** — it does not run any code at runtime. The compiler replaces `sizeof(short)` with the literal number `2` (on essentially all modern platforms) before the program is even linked. The result has type `size_t`, an unsigned integer type wide enough to describe the size of any object.

### Why sizes vary by platform

The C++ standard fixes only **minimum sizes** and the relative ordering (`1 == sizeof(char) ≤ sizeof(short) ≤ sizeof(int) ≤ sizeof(long) ≤ sizeof(long long)`). It does *not* fix exact sizes. Typical sizes on a 64-bit Linux/GCC system:

| Type | Linux 64-bit GCC | Windows 64-bit MSVC/MinGW |
|------|------------------|---------------------------|
| `short` | 2 | 2 |
| `int` | 4 | 4 |
| `long` | **8** | **4** ← differs! |
| `long long` | 8 | 8 |
| `pointer` | 8 | 8 |

Windows uses the **LLP64** data model (`long` stays 4 bytes even on 64-bit), while Linux/macOS use **LP64** (`long` is 8 bytes on 64-bit). This is a frequent portability trap.

### `sizeof(char)` is always 1

By definition, `sizeof(char) == 1` on every C++ implementation. This is the fundamental unit of memory in C++ — a "byte" in the C++ sense is exactly the storage of one `char`, which is at least 8 bits but may be more on exotic hardware.

### Tab formatting

Each data type name is followed by enough `\t` characters to push the size into a second column. Because type names have different lengths (`int` vs `unsigned int`), we vary the number of tabs.

### Why `size_t` matters

Printing `sizeof(...)` directly with `cout` works because `cout` knows how to print `size_t`. But if you `printf`-style it with `%d`, you may get a warning on 64-bit systems because `size_t` is 8 bytes there and `int` is 4 — the argument types don't match. The C++ way (`cout`) handles this automatically.

---

## 7. Sample Input / Output

```
$ ./09_SizeOfDataTypes
Data type              Size (bytes)
-----------------------------
short                  2
int                    4
long                   8
long long              8
float                  4
double                 8
long double            16
char                   1
bool                   1
unsigned int           4
```

(Exact `long` and `long double` values depend on your platform — on Windows/MinGW you may see `long = 4` and `long double = 8`.)

---

## 8. Real-World Application

Knowing data-type sizes is essential in:

- **Binary file formats** (PNG, WAV, ELF, MP4) — every field has a fixed byte width; reading the file means reading exact-size integers.
- **Network protocols** (TCP/IP, DNS, DNSSEC) — packet headers use fixed-width fields; you must use `uint16_t`, `uint32_t` from `<cstdint>`.
- **Embedded programming** — microcontrollers may have only 2 KB of RAM; choosing `int8_t` over `int` saves 75% of memory.
- **Interoperability with C** — struct layouts depend on type sizes and padding; mismatched assumptions cause corrupt data.
- **Database engines** — column types (INT, BIGINT, TINYINT) map directly to fixed-width C++ types.

Use the fixed-width types from `<cstdint>` (`int32_t`, `uint64_t`, etc.) whenever a specific byte width is required.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Assuming `int` is always 4 bytes | Some 16-bit MCUs have 2-byte `int` | Use `<cstdint>` types like `int32_t` |
| `long` size differs between OS | LLP64 (Windows) vs LP64 (Linux/macOS) | Use `int64_t` from `<cstdint>` for guaranteed 8 bytes |
| `printf("%d", sizeof(x))` warning | `size_t` ≠ `int` on 64-bit | Use `%zu` for `size_t`, or just use `cout` |
| Pointer size assumed = `int` size | On 64-bit, pointer = 8, `int` = 4 | Use `intptr_t` or `size_t` for pointer-sized ints |
| Misaligned columns in output | Type names have varying lengths | Use multiple `\t` or `<iomanip>` `setw()` |

---

## 10. Practice Question

Add these lines and explain the output:

```cpp
cout << "int* (pointer)\t\t" << sizeof(int*) << "\n";
cout << "double* (pointer)\t" << sizeof(double*) << "\n";
```

1. What is the size of a pointer on your machine?
2. Why is the size of an `int*` the same as a `double*`, even though `int` and `double` have different sizes?
3. Include `<cstdint>` and print `sizeof(int32_t)` and `sizeof(int64_t)` — are they what you expect?
