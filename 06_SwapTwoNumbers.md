# Program 06 — Swap Two Numbers Using a Third Variable

| Field | Value |
|-------|-------|
| Program Number | 06 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `06_SwapTwoNumbers.cpp` |

---

## 1. Aim

To swap the values of two variables using a temporary third variable, introducing the assignment operator `=` and the classic three-step swap idiom.

---

## 2. Concepts Used

- Variable assignment with `=`
- Temporary / helper variable
- The three-step swap idiom
- Printing values before and after to verify the swap

---

## 3. Problem Statement

Read two integers from the user, display them, swap their values using a third variable, and display them again.

---

## 4. Algorithm

1. Read `a` and `b`.
2. Print "Before swap: a = ..., b = ...".
3. `temp = a;` — save `a`'s value into `temp`.
4. `a = b;` — overwrite `a` with `b`'s value.
5. `b = temp;` — restore the original `a` (now in `temp`) into `b`.
6. Print "After swap: a = ..., b = ...".

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a = 0, b = 0, temp = 0;

    cout << "Enter two integers: ";
    cin  >> a >> b;

    cout << "Before swap: a = " << a << ", b = " << b << endl;

    temp = a;
    a    = b;
    b    = temp;

    cout << "After  swap: a = " << a << ", b = " << b << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `int a = 0, b = 0, temp = 0;`

Three integer variables are declared and zero-initialized. The `temp` variable is the **helper** that will hold `a`'s value temporarily while we overwrite `a`.

### `cout << "Before swap: ..." << a << ", b = " << b << endl;`

We print the values *before* the swap. This is critical for verifying that the swap actually worked — without "before" and "after" prints, you cannot tell if anything changed.

### `temp = a;`

This is **step 1 of the swap**. We copy `a`'s value into `temp` so that `a`'s original value is preserved somewhere safe. After this line, `temp == a` (originally) and `a` is unchanged.

### `a = b;`

**Step 2**. We overwrite `a` with `b`'s value. After this line, `a == b` (the original `b`). But `a`'s original value is *still safely stored in `temp`*.

### `b = temp;`

**Step 3**. We copy the saved original `a` (from `temp`) into `b`. After this line, `b == original a`. The swap is now complete: `a` holds `b`'s original value and `b` holds `a`'s original value.

### Why this ordering matters

If you did `a = b;` *before* `temp = a;`, you would lose `a`'s original value forever — both `a` and `b` would end up equal to `b`. The order `temp = a; a = b; b = temp;` is the **only correct sequence** with three assignments.

---

## 7. Sample Input / Output

```
$ ./06_SwapTwoNumbers
Enter two integers: 5 9
Before swap: a = 5, b = 9
After  swap: a = 9, b = 5
```

---

## 8. Real-World Application

Swapping is a fundamental building block of countless algorithms:

- **Sorting algorithms**: bubble sort, insertion sort and the partitioning step of quicksort all swap elements.
- **Graphics double-buffering**: the front and back frame buffers are swapped each frame to avoid tearing.
- **Concurrency**: a "swap" primitive underlies lock-free data structures (e.g. compare-and-swap).
- **Undo/redo**: the current state and the backup state are swapped on each undo step.
- **Cryptography**: some ciphers (e.g. RC4) swap bytes in a key schedule.

In later chapters you'll see C++ provide `std::swap(a, b);` which does this for you (and is optimized for many types).

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Both variables end up equal to `b` | Did `a = b;` before saving `a` | Always save `a` into `temp` *first* |
| `a, b = b, a` syntax error | That's Python, not C++ | Use the three-step idiom (or `std::swap`) |
| Looks like nothing changed | Forgot "before" print, or printed in same order after | Always print both before and after |
| `temp` not initialized | `int temp;` with no `= 0` | Initialize: `int temp = 0;` (good hygiene) |

---

## 10. Practice Question

Swap two integers **without** using a third variable, using:

**(a) Arithmetic method** (watch out for overflow!):
```cpp
a = a + b;
b = a - b;
a = a - b;
```

**(b) XOR method** (overflow-safe):
```cpp
a ^= b;
b ^= a;
a ^= b;
```

Verify both methods produce the same result as the temp-variable approach for inputs like `7 13` and `-5 9`.
