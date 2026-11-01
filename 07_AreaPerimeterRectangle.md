# Program 07 — Area and Perimeter of a Rectangle

| Field | Value |
|-------|-------|
| Program Number | 07 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `07_AreaPerimeterRectangle.cpp` |

---

## 1. Aim

To read the length and breadth of a rectangle from the user and compute both its **area** (`length × breadth`) and **perimeter** (`2 × (length + breadth)`).

---

## 2. Concepts Used

- Multiple variables of the same type declared together
- Arithmetic operators `*`, `+`, and parentheses `()`
- Two independent computations from the same input
- Formatted multi-line output

---

## 3. Problem Statement

Write a C++ program that reads the length and breadth of a rectangle and prints its area and perimeter.

---

## 4. Algorithm

1. Declare `double` variables `length`, `breadth`, `area`, `perimeter`.
2. Prompt and read `length` and `breadth`.
3. Compute `area = length * breadth`.
4. Compute `perimeter = 2 * (length + breadth)`.
5. Print both results with labels.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    double length = 0.0, breadth = 0.0;
    double area = 0.0, perimeter = 0.0;

    cout << "Enter length and breadth of rectangle: ";
    cin  >> length >> breadth;

    area      = length * breadth;
    perimeter = 2 * (length + breadth);

    cout << "Area      = " << area      << endl;
    cout << "Perimeter = " << perimeter << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `double length = 0.0, breadth = 0.0;`

The two dimensions of the rectangle are stored as `double` because real-world lengths are often not integers (e.g. `5.5` metres). Both are declared in one statement, separated by commas.

### `double area = 0.0, perimeter = 0.0;`

Two more `double` variables hold the results. Even though we will assign them before reading, initializing at declaration is good hygiene.

### `cin >> length >> breadth;`

The user enters two numbers separated by space or Enter. `cin` reads them into `length` and `breadth` respectively.

### `area = length * breadth;`

The geometric formula for the area of a rectangle. The `*` operator multiplies the two `double` values; the result is `double`.

### `perimeter = 2 * (length + breadth);`

The perimeter formula is `2 × (l + w)`. **Parentheses are essential here** because `*` has higher precedence than `+`. Without parentheses, `2 * length + breadth` would compute `(2 * length) + breadth` — mathematically wrong.

### Two `cout` statements

Each result is printed on its own line with a descriptive label. Aligning the `=` sign with spaces (`"Area      = "` vs `"Perimeter = "`) makes the output easier to read.

---

## 7. Sample Input / Output

```
$ ./07_AreaPerimeterRectangle
Enter length and breadth of rectangle: 5 3
Area      = 15
Perimeter = 16
```

---

## 8. Real-World Application

Geometry calculators are everywhere:

- **Architecture & interior design**: room area for flooring, paint quantity estimation, carpet ordering.
- **Agriculture**: land parcel area for fertilizer and seed calculations.
- **Manufacturing**: sheet metal layout, cutting plans, packaging dimensions.
- **Game development**: every 2D game uses axis-aligned bounding boxes (AABBs) — rectangles defined by width/height — for collision detection.
- **GIS (geographic information systems)**: bounding rectangles around map features.

The pattern "read inputs → compute several results → print them" is the template for thousands of utility programs.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Wrong perimeter | Missing parentheses: `2 * l + w` | Use `2 * (l + w)` |
| Area truncated to integer | Declared `int area` | Use `double area` |
| Reads `length` twice | Typo: `cin >> length >> length;` | Use distinct variable names |
| Accepts negative dimensions | No validation yet | In Chapter 2 you'll add `if (length <= 0)` checks |
| `cout` shows scientific notation for large numbers | Default `cout` format | Use `<iomanip>` with `fixed` and `setprecision` |

---

## 10. Practice Question

Extend the program to also compute and print the **length of the diagonal** of the rectangle using Pythagoras' theorem and the `sqrt` function from `<cmath>`:

```cpp
#include <cmath>
double diagonal = sqrt(length*length + breadth*breadth);
```

Verify your output: for length = 3 and breadth = 4, the diagonal should be exactly 5.
