# Program 05 — Product of Two Floating-Point Numbers

| Field | Value |
|-------|-------|
| Program Number | 05 |
| Chapter | 1 — C++ Basics and Input/Output |
| Difficulty | Beginner |
| File | `05_ProductOfFloats.cpp` |

---

## 1. Aim

To take two floating-point numbers from the user and print their product, demonstrating the `*` operator and `double` arithmetic.

---

## 2. Concepts Used

- `double` data type (preferred over `float` for general use)
- `cin >>` reading floating-point values
- Arithmetic operator `*`
- Difference between integer and floating-point division
- Default precision of `cout` for `double`

---

## 3. Problem Statement

Write a C++ program that reads two floating-point numbers from the keyboard and displays their product.

---

## 4. Algorithm

1. Declare two `double` variables `a`, `b`, and a `product` variable.
2. Prompt the user.
3. Read the two doubles with `cin >> a >> b`.
4. Compute `product = a * b`.
5. Print the product.

---

## 5. Source Code

```cpp
#include <iostream>
using namespace std;

int main()
{
    double a = 0.0, b = 0.0, product = 0.0;

    cout << "Enter two floating-point numbers: ";
    cin  >> a >> b;

    product = a * b;

    cout << "Product = " << product << endl;
    return 0;
}
```

---

## 6. Line-by-Line Explanation

### `double a = 0.0, b = 0.0, product = 0.0;`

Three `double` variables are declared and initialized. `double` is a 64-bit floating-point type that gives about 15 significant decimal digits — enough for almost all general-purpose computation. We initialize with `0.0` (a `double` literal) rather than `0` (an `int` literal) to make intent clear, although the compiler would convert automatically.

### `cin >> a >> b;`

`cin` reads floating-point numbers much like integers — it skips whitespace, then reads digits, an optional decimal point, an optional `e` exponent (e.g. `1.5e3` for 1500), and stops at the first non-numeric character.

### `product = a * b;`

The `*` operator performs floating-point multiplication because both operands are `double`. If one operand were `int`, C++ would implicitly convert it to `double` first ("usual arithmetic conversions") — but if *both* were `int`, the result would be `int` and any fractional part would be discarded.

### `cout << "Product = " << product << endl;`

By default, `cout` prints doubles with up to 6 significant digits and trims trailing zeros. To control precision you would include `<iomanip>` and write `cout << fixed << setprecision(4);`. For now, the default is fine.

---

## 7. Sample Input / Output

```
$ ./05_ProductOfFloats
Enter two floating-point numbers: 2.5 4.0
Product = 10
```

(`cout` trims the trailing `.0` because 10 is exactly representable.)

---

## 8. Real-World Application

Floating-point multiplication is everywhere:

- **Graphics & games**: every 3D transform is a matrix multiplication.
- **Physics simulations**: `force = mass × acceleration`, `momentum = mass × velocity`.
- **Finance**: `interest = principal × rate × time`.
- **Sensor calibration**: `real_value = raw_reading × scale_factor + offset`.
- **Machine learning**: a neural network forward pass is mostly matrix multiplications.

Choosing `double` over `float` matters whenever you accumulate many operations — rounding errors compound and `double` keeps them small.

---

## 9. Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `5 / 2 = 2` instead of `2.5` | Integer division (both operands `int`) | Make at least one operand `double` (e.g. `5.0 / 2`) |
| `product = 4.999999` | Floating-point rounding | Use `setprecision` from `<iomanip>` to round display |
| `cannot convert double to int` warning | Assigned `double` result to `int` variable | Use `double` for the result, or cast explicitly |
| Wrong result for very large numbers | Overflow beyond `double` range | Use `long double` or rethink the algorithm |
| Wrong result for tiny numbers | Catastrophic cancellation | Use a numerically stable algorithm |

---

## 10. Practice Question

Read three doubles representing the **length, width and height of a box** and print its **volume** and **surface area**.

```cpp
double volume = length * width * height;
double surface = 2 * (length*width + width*height + height*length);
```
