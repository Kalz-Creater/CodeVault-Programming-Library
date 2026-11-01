# Program 02 — Multi-line Output and Escape Sequences

| Field | Value |
|-------|-------|
| Program Number | 02 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `02_MultilineAndEscapeSequences.cpp` |

---

## 1. Aim

To learn how to print text on multiple lines, how to insert tabs and quotes inside output, and how to write comments — using C++ escape sequences.

---

## 2. Concepts Used

| Concept | Description |
|---------|-------------|
| `cout` chaining | Multiple `<<` operators can be chained in one statement |
| `\n` | Newline character — moves cursor to next line |
| `\t` | Horizontal tab — moves cursor to next tab stop (≈ 8 spaces) |
| `\\` | Literal backslash (needed because `\` starts an escape) |
| `\"` | Literal double quote inside a string literal |
| `//` | Single-line comment — compiler ignores rest of line |
| `/* ... */` | Multi-line comment — compiler ignores everything between |
| `endl` vs `\n` | `endl` flushes the buffer; `\n` does not (faster) |

---

## 3. Problem Statement

Write a C++ program that prints a short student profile containing the user's name, course, a tabular subject list, a quoted sentence and a Windows-style file path — using escape sequences to format the output across multiple lines.

---

## 4. Algorithm

1. Include `<iostream>` and bring in the `std` namespace.
2. Inside `main()`, print the heading using `\n` for line breaks.
3. Print rows of columns separated by `\t` (tab) for alignment.
4. Print a quoted sentence using `\"` to embed double quotes.
5. Print a Windows file path using `\\` for each backslash.
6. `return 0`.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Student Profile\n";
    cout << "Name:  Aman Verma\n";
    cout << "Course: B.Tech (CSE)\n\n";

    cout << "Subject\t\tMarks\n";
    cout << "Maths\t\t95\n";
    cout << "Physics\t\t88\n\n";

    cout << "Quote: \"C++ is fun!\"\n";
    cout << "File path: C:\\CPP\\hello.cpp\n";

    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `cout << "Student Profile\n";`

The string `"Student Profile\n"` contains the escape sequence `\n`. When `cout` sees `\n` it moves the cursor to the beginning of the next line instead of printing a backslash and an `n`. This is how we print on multiple lines without writing many `cout` statements.

### `cout << "Subject\t\tMarks\n";`

`\t` is the **horizontal tab** escape sequence. It moves the cursor to the next tab stop (usually every 8th column). Two tabs `\t\t` push "Marks" far enough right to form a neat column with the data rows below it.

### `cout << "Quote: \"C++ is fun!\"\n";`

A double quote `"` normally ends a string literal. To *print* a double quote we must escape it with a backslash: `\"`. The output therefore reads exactly `Quote: "C++ is fun!"`.

### `cout << "File path: C:\\CPP\\hello.cpp\n";`

In Windows, file paths use backslashes. But `\` starts an escape sequence in C++ string literals — so `\C` could be misread (and `\n` inside a path would print as a newline!). To print a literal backslash, we write `\\` (escape the backslash itself). The output is `File path: C:\CPP\hello.cpp`.

### `// Single-line comment`

Anything after `//` on a line is ignored by the compiler. Use it for short notes.

### `/* ... */`

A multi-line comment. Everything between `/*` and the *next* `*/` is ignored, even across many lines. Never nest these — a `*/` closes the *first* `/*`, even if you intended it to close an inner one.

### `endl` vs `\n`

`endl` and `\n` both move to the next line, but `endl` also **flushes** the output buffer (forces the OS to write pending output immediately). In performance-sensitive code, prefer `\n` — flushing on every line is slow.

---

## 7. Sample Input / Output

```
$ ./02_MultilineAndEscapeSequences
Student Profile
Name:  Aman Verma
Course: B.Tech (CSE)

Subject         Marks
Maths           95
Physics         88

Quote: "C++ is fun!"
File path: C:\CPP\hello.cpp
```

No input is required.

---

## 8. Real-World Application

Formatted console output is the foundation of **command-line tools**, **log file writers**, **terminal dashboards** and **report generators**. Escape sequences are used everywhere — installers print colored progress bars (via `\033[...m`), database dumps align columns with `\t`, and Windows service loggers double every backslash in file paths. The same skills apply when generating HTML/XML or building text-based menus in embedded systems that lack a GUI.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `C: ew` instead of `C:\new` | `\n` interpreted as newline | Write `\\n` → `\\` + `n` |
| Output appears on same line | Forgot `\n` or `endl` | Add `\n` or chain `endl` |
| `expected ';'` | Long `cout` chain missing trailing `;` | Add `;` at end of statement |
| Comment never ends | `/*` opened but `*/` missing | Always close multi-line comments |
| `missing terminating "` | Wrote `"C++ is fun!"` and forgot to escape quotes | Use `\"` inside the literal |

---

## 10. Practice Question

Write a program that prints the ASCII art of a triangle using escape sequences and a single `cout` statement:

```
    /\
   /  \
  /____\
```

**Hint:** You need to escape both `\` and the forward slash `/` is fine as-is. Use leading spaces for alignment and `\n` between lines.
