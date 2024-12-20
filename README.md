# `matrix.h`

![GitHub license](https://img.shields.io/github/license/Keshav11-coder/matrix.h)
![GitHub issues](https://img.shields.io/github/issues/Keshav11-coder/matrix.h)
![GitHub release](https://img.shields.io/github/v/release/Keshav11-coder/matrix.h)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/Keshav11-coder/matrix.h)

A lightweight C++ library for basic and advanced matrix operations, optimized for microcontrollers and compatible with standard C++ projects.

`matrix.h` simplifies matrix manipulation, leveraging `std::vector` under the hood for efficient storage and operations. Designed for ease of use in environments like Arduino but versatile enough for other platforms.

---

## Table of Contents

- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Setup](#setup)  
- [Creating Matrices](#creating-matrices)  
- [Examples (API / Usage)](#examples-api--usage)  
  - [Arithmetic Operations](#arithmetic-operations)  
    - [Addition](#addition)  
    - [Subtraction](#subtraction)  
    - [Multiplication](#multiplication)  
    - [Scalar Multiplication](#scalar-multiplication)  
    - [Matrix Sum](#matrix-sum)  
    - [Element-wise Multiplication (Hadamard)](#element-wise-multiplication-hadamard)  
  - [Matrix Operations](#matrix-operations)  
    - [Transpose](#transpose)  
    - [Inverse](#inverse)  
    - [Pseudo-inverse](#pseudo-inverse)  
  - [Matrix Accessors](#matrix-accessors)  
    - [Get Cell](#get-cell)  
    - [Get Region](#get-region)  
    - [Get Row](#get-row)  
    - [Get Column](#get-column)  
  - [Matrix Manipulators](#matrix-manipulators)  
    - [Set Cell](#set-cell)  
    - [Set Region](#set-region)  
    - [Manipulate Using forEach](#manipulate-using-foreach)  
  - [Other Useful Utilities](#other-useful-utilities)  
    - [Matrix Comparison](#matrix-comparison)  
    - [Get Dimensions](#get-dimensions)  
    - [Print Matrix](#print-matrix)  

---

## Getting Started

### Requirements
The `matrix.h` library uses a couple of built-in C++ native (`std::`) libraries:
- `std::vector`
- `std::functional`

Optional requirements are:
- `std::iostream` (for alternative matrix printing)
- `std::iomanip` (for controlling decimal places for `iostream` matrix prints)

### Setup
To integrate `matrix.h` into your project:
1. Download and copy `matrix.h` into your project directory.
   Your project structure could look like this:
   
   ```
   Project
   ├─main.cpp
   └─matrix.h
   ```
2. Include `matrix.h` in your project:
   
   ```cpp
   #include <iostream>
   
   #include "matrix.h"

   int main() {
     return 0;
   }
   ```

## Creating Matrices

1. Using matrix dimensions and a filter value:

   ```cpp
   matrix A(2, 2, 0);
   ```
2. Using `std::vector` or `std::initializer_list`:

   ```cpp
   matrix A({
     {1, 2},
     {3, 4}
   });
   ```

> [!NOTE]
> `matrix.h` also uses initializer lists (`std::initializer_list`) to allow `matrix` objects to identify as such:
>
> ```cpp
> matrix A = {
>   {1, 2},
>   {3, 4}
> };
> ```

---

## Examples (API / Usage)

### Arithmetic Operations

#### Addition

```cpp
matrix A(2, 2, 1);
matrix B(2, 2, 4);

matrix C = A + B; // 2x2 matrix with filter value 5
```

#### Subtraction

```cpp
matrix A(2, 2, 4);
matrix B(2, 2, 1);

matrix C = A - B; // 2x2 matrix with filter value 3
```

#### Multiplication

```cpp
matrix A(2, 3, 4);
matrix B(3, 4, 1);

matrix C = A * B; // 2x4 matrix
```

#### Scalar Multiplication

```cpp
matrix A(2, 2, 4);

matrix B = A * 1.25; // 2x2 matrix multiplied by 1.25
```

#### Matrix Sum

```cpp
matrix A(2, 2, 4);

float sum = A.sum(); // Floating point variable with the sum of all cells of matrix A
```

#### Element-wise Multiplication (Hadamard)

```cpp
matrix A(2, 2, 4);
matrix B(2, 2, 5);

matrix C = A.hadamard(B); // 2x2 matrix with filter value 20
```

### Matrix Operations

#### Transpose

```cpp
matrix A(2, 3, 4);

matrix B = A.T(); // Transposed (diagonally flipped) matrix 3x2 with filter value 4
```

#### Inverse

```cpp
matrix A(4, 4, 4);

matrix B = !A; // Inverse of matrix A with dimensions 4x4
```

#### Pseudo-inverse

```cpp
matrix A(4, 6, 4);

matrix B = A.pseudoinverse(); // Pseudo-inverse of matrix A
```

### Matrix Accessors

#### Get Cell

```cpp
matrix A(2, 2, 4);

float value = A(1, 1); // Returns 4.
```

#### Get Region

```cpp
matrix A(4, 4, 4);

matrix B = A(1, 1, 2, 2); // Returns a 2x2 matrix, the top left portion of A.
```

#### Get Row

```cpp
matrix A(4, 4, 4);

std::vector<float> row1 = A.row(1); // Returns the first row of matrix A
```

#### Get Column

```cpp
matrix A(4, 4, 4);

std::vector<float> column1 = A.column(1); // Returns the first column of matrix A
```

### Matrix Manipulators

#### Set Cell

```cpp
matrix A(2, 2, 4);

A.set(1, 1, 9); // Sets the top-left value of A to 9.
```

#### Set Region

```cpp
matrix A(4, 4, 4);
matrix B(2, 2, 9);

A.set(1, 1, 2, 2, B); // Sets the top-left portion of A (2x2) to the values of B.
```

#### Manipulate Using forEach

```cpp
matrix A(4, 4, 4);

A.forEach([&](float x) mutable -> float { // Modifies A sequentially, and multiplies each value by 2.
  return x * 2;
});
```

> [!TIP]
> If you want the current position of an iteration in rows and columns, use this method:
> ```cpp
> matrix A(4, 4, 4);
>
> A.forEach([&](float x, int row, int column) mutable -> float { // Modifies A sequentially, and multiplies each value by the positional coordinates.
>  return x * row * column;
> });
> ```

### Other Useful Utilities

#### Matrix Comparison

```cpp
matrix A(4, 4, 4);
matrix B(4, 4, 2);
matrix C(4, 4, 4);

(A == B); // false
(A == C); // true
```

#### Get Dimensions

```cpp
matrix A(4, 4, 4);

A.rows(); // 4
A.columns(); // 4
```

#### Print Matrix

```cpp
matrix A(4, 4, 4);

A.print();
```

> [!NOTE]
> At the top of every `matrix.h` file there is a `printMatrix()` function. Modify this to your needs, or take one of the built-in examples—for example, the one for `std::cout`.

