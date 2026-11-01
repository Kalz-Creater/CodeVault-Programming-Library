# Program 04 — Sum of Two Integers

| Field | Value |
|-------|-------|
| Program Number | 04 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `04_SumOfTwoIntegers.cpp` |

---

## 1. Aim

To take two integers as input from the user and display their sum, introducing the `cin` input stream and the `+` arithmetic operator.

---

## 2. Concepts Used

- Variable declaration and initialization
- `cin` — standard input stream object (paired with `cout`)
- `>>` — stream **extraction** operator (pulls data from a stream into a variable)
- Arithmetic operator `+`
- Prompting the user before reading input

---

## 3. Problem Statement

Write a C++ program that reads two integers from the keyboard and prints their sum.

---

## 4. Algorithm

1. Declare two `int` variables `a` and `b`, plus a third variable `sum`.
2. Prompt the user with `cout`.
3. Read the two integers using `cin >> a >> b`.
4. Compute `sum = a + b`.
5. Print the result using `cout`.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a = 0, b = 0, sum = 0;

    cout << "Enter two integers: ";
    cin  >> a >> b;

    sum = a + b;

    cout << "Sum = " << sum << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `int a = 0, b = 0, sum = 0;`

Three `int` variables are declared and initialized to `0` in a single statement, separated by commas. Initializing variables at declaration is **best practice** — it avoids the classic bug of reading from an uninitialized variable, which produces undefined behavior (random garbage values).

### `cout << "Enter two integers: ";`

A **prompt** is printed so the user knows the program is waiting for input. Without a prompt, the program appears frozen and the user does not know what to type.

### `cin >> a >> b;`

`cin` (pronounced "see-in") is the standard input stream object, attached to the keyboard. `>>` is the **stream extraction operator** — it pulls data out of the stream and stores it into the variable on its right. The two extractions can be chained: the first integer goes into `a`, the second into `b`. `cin` skips leading whitespace (spaces, tabs, newlines) automatically and stops reading a number when it hits a non-digit character.

### `sum = a + b;`

The `+` operator adds the two values. The result is stored into `sum` via the assignment operator `=`. The right-hand side is evaluated first (`a + b`), then assigned to the left-hand side.

### `cout << "Sum = " << sum << endl;`

Three things are pushed into `cout` in sequence: the literal string `"Sum = "`, the value of `sum`, and a newline. The output looks like `Sum = 19`.

---

## 7. Sample Input / Output

```
$ ./04_SumOfTwoIntegers
Enter two integers: 12 7
Sum = 19
```

The user types `12 7` then presses Enter.

---

## 8. Real-World Application

Reading input from a user and producing a computed result is the **template for every interactive program**:

- **Calculators** read two numbers and an operator
- **Billing systems** read quantities and prices
- **Statistical aggregators** read data points and sum / average them
- **POS terminals** read item codes and accumulate totals

The same `cin >> ... >> ...` pattern scales up to file and network streams in later chapters.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Program appears to hang | No prompt before `cin` | Always print a prompt |
| `'>>' should be '<<'` warning | Wrote `cin << a` | Use `>>` with `cin`, `<<` with `cout` |
| Wrong result (garbage value) | Variable uninitialized | Initialize at declaration: `int a = 0;` |
| Reads only one number | User pressed Enter between numbers | Either enter both on one line, or call `cin` twice |
| Crash on non-integer input | `cin` enters fail state | For now: just enter integers; later we handle invalid input |

---

## 10. Practice Question

Extend the program to read **three** integers and print both their **sum** and **average** (the average should be a `double`).

```cpp
double avg = sum / 3.0;   // Use 3.0, not 3, to avoid integer division!
```
