# Program 08 — Celsius to Fahrenheit Converter

| Field | Value |
|-------|-------|
| Program Number | 08 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `08_CelsiusToFahrenheit.cpp` |

---

## 1. Aim

To convert a temperature given in degrees Celsius to degrees Fahrenheit using the formula `F = (C × 9/5) + 32`, and to demonstrate the critical importance of writing `9.0 / 5.0` (not `9 / 5`) to avoid integer division.

---

## 2. Concepts Used

- Reading a `double` from `cin`
- Arithmetic formula evaluation
- **Integer vs floating-point division** — the #1 beginner pitfall
- Operator precedence and parentheses

---

## 3. Problem Statement

Write a C++ program that reads a temperature in Celsius from the user and prints the equivalent temperature in Fahrenheit.

---

## 4. Algorithm

1. Declare `double celsius, fahrenheit`.
2. Prompt and read `celsius`.
3. Compute `fahrenheit = (celsius * 9.0 / 5.0) + 32.0`.
4. Print both values.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    double celsius = 0.0, fahrenheit = 0.0;

    cout << "Enter temperature in Celsius: ";
    cin  >> celsius;

    fahrenheit = (celsius * 9.0 / 5.0) + 32.0;

    cout << celsius << " C = " << fahrenheit << " F" << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `double celsius = 0.0, fahrenheit = 0.0;`

Temperatures are real numbers (37.5, −40.0, 100.0), so we use `double` for both variables. Initializing with `0.0` keeps the code safe even if `cin` fails (e.g. user types text instead of a number).

### `cin >> celsius;`

Reads one floating-point number from the keyboard. `cin` skips leading whitespace and stops at the first non-numeric character.

### `fahrenheit = (celsius * 9.0 / 5.0) + 32.0;`

The standard conversion formula `F = (C × 9/5) + 32`. **Look carefully at the literals: `9.0` and `5.0`, not `9` and `5`.**

#### The Integer Division Trap

If you write `9 / 5` (both `int`), C++ performs **integer division** and the result is `1` (the fractional part `0.8` is discarded). The formula then becomes `F = C × 1 + 32 = C + 32`, which is wildly wrong — for `C = 37` you'd get `69 F` instead of the correct `98.6 F`!

By writing `9.0 / 5.0` (both `double`), C++ performs **floating-point division** and you get the correct `1.8`. The whole expression is then `double`.

#### Precedence

Multiplication and division have higher precedence than addition, so `celsius * 9.0 / 5.0` is evaluated left-to-right as `(celsius * 9.0) / 5.0` — fine. But adding the explicit parentheses `(celsius * 9.0 / 5.0) + 32.0` makes the formula structure obvious to the next reader.

### `cout << celsius << " C = " << fahrenheit << " F" << endl;`

Four values are pushed into `cout`: the Celsius number, the unit string `" C = "`, the Fahrenheit number, and the unit `" F"`. The output reads like `37 C = 98.6 F`.

---

## 7. Sample Input / Output

```
$ ./08_CelsiusToFahrenheit
Enter temperature in Celsius: 37
37 C = 98.6 F
```

A useful sanity check: `−40 °C` and `−40 °F` are exactly the same temperature, so `−40` input should give `−40` output.

---

## 8. Real-World Application

Temperature conversion is used in:

- **Weather apps and websites** — APIs often return Kelvin internally; the UI converts to °C or °F based on the user's locale.
- **Thermostats and HVAC controllers** — sensor reads in °C, user sets target in °F (or vice versa).
- **Medical devices** — body temperature is 37 °C / 98.6 °F; both must be displayed.
- **Cooking recipes and ovens** — US ovens use °F, European ones use °C; recipe sites convert automatically.
- **Scientific data pipelines** — Celsius for chemistry, Kelvin for physics, Fahrenheit for US weather.

The same integer-division pitfall occurs in *every* formula with a fraction: percentage calculations (`mark / total * 100`), averages, scaling factors, and so on.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Output `37 C = 69 F` | Wrote `9/5` (integer division = 1) | Write `9.0 / 5.0` or `9 / 5.0` |
| Truncated to integer | Declared `int fahrenheit` | Use `double` |
| Reading into wrong variable | `cin >> fahrenheit` by mistake | Read into `celsius` first |
| Wrong precedence | `celsius * 9 / 5 + 32` without parens | Wrap in parentheses: `(celsius * 9.0 / 5.0) + 32.0` |
| Scientific notation in output | Default `cout` for very small/large numbers | Use `cout << fixed << setprecision(2);` |

---

## 10. Practice Question

Extend the program to ask the user **which direction** to convert:

```
Press C to convert Celsius -> Fahrenheit
Press F to convert Fahrenheit -> Celsius
> C
Enter temperature in Celsius: 37
37 C = 98.6 F
```

**Hint:** Read a `char` for the choice, then use an `if` statement (Chapter 2 material — try it as a preview). The reverse formula is `C = (F − 32) × 5/9`.
