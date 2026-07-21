~ invented by Guido van Rossum in 1991. Managed by Python Software Foundation (PSF).*

## Part 1 : Introduction
Python is a high-level, interpreted, general-purpose, easiest and clean syntax programming language.  Python is dynamically typed language meaning the type of variable is determined while the program is running.

Python was designed to address several goals:
- Simpler syntax than many existing languages
- Faster software development
- Better code readability
- Easy extensibility
- Cross-platform compatibility

Its philosophy is summarized by **"The Zen of Python"**, which values readability, simplicity, and explicitness.

Few Features of Python :
1. Simple Syntax : uses clean, readable syntax with minimal boilerplate
2. Dynamically Typed : variable types are determined at runtime, so developer do not need to declare data types explicitly.
3. Object-Oriented : follows OOPs Principle
4. Cross Platform : python program runs on windows, linux, and other type of operating system with minimal or no changes.
5. Huge Standard Library : python have a large, comprehensive standard library.

Python continues to grow because of its versatility and dominant position in emerging technologies.



## Part 2 : Variable & Datatype

### 2.1. Variable
Python has **one main kind of variable assignment**. Variables are created automatically when a value is assigned. Their scope (local, global, or nonlocal) depends on where they are defined, but the assignment syntax remains the same.

| Variable Type | Meaning | Syntax |
| --- | --- | --- |
| Variable Assignment | Creates a variable by assigning a value. The type is determined automatically at runtime. | `age = 25` |
| Global Variable | Declared outside all functions and accessible throughout the module. | `count = 0` |
| Local Variable | Declared inside a function and accessible only within that function. | `def fun(): age = 20` |
| Nonlocal Variable | Used inside nested functions to refer to a variable in the enclosing function. | `nonlocal count` |

### Rules for Python Variables
- Variable names are **case-sensitive**.
- Must begin with a **letter** or **underscore (`_`)**.
- Cannot begin with a number.
- Cannot contain spaces.
- Cannot use Python keywords as variable names.
- No declaration keyword (`int`, `float`, etc.) is required.
- Variables are created when a value is assigned.

Valid Example :
age = 25
salary = 50000
first_name = "John"

### 2.2. DataType
| Data Type | Meaning | Python Syntax |
| --- | --- | --- |
| Integer | Stores whole numbers | `age = 25` |
| Floating Point | Stores decimal numbers | `price = 99.99` |
| Boolean | Stores `true` or `false` values | `is_active = True` |
| Character | Stores a single character | *No separate `char` type; use a one-character string:* `grade = 'A'` |
| String | Stores a sequence of characters | `name = "John"` |
| List / Array | Stores multiple values | `arr = [1, 2, 3]` |
| Tuple | Ordered immutable collection | `point = (10, 20)` |
| Set | Stores unique elements | `nums = {1, 2, 3}` |
| Dictionary / Map | Stores key-value pairs | `data = {"age": 20}` |
| Null / None | Represents absence of a value | `None` |
| Bytes | Stores binary data | `data = b"Hello"` |



## Part 3 : Input & Output, Operator

### 3.1. Input & Output
Input is a process of providing data to a program for processing whereas output is the information produced by a program after processing the input.

Input
| Type | Syntax | Example |
| --- | --- | --- |
| User Input | `input()` | `name = input("Enter Name: ")` |
| Integer Input | `int(input())` | `age = int(input("Enter Age: "))` |
| Float Input | `float(input())` | `salary = float(input())` |
| Multiple Inputs | `input().split()` | `a, b = input().split()` |

Output
| Type | Syntax | Example |
| --- | --- | --- |
| Normal Output | `print()` | `print("Hello")` |
| Multiple Values | `print()` | `print(name, age)` |
| Formatted Output (f-string) | `print(f"...")` | `print(f"Age: {age}")` |

Note:
- `input()` always returns a **string**.
- Convert the input to the required type using `int()`, `float()`, etc.
- Handle invalid user input to avoid `ValueError`.
- Use **f-strings** for clean and readable formatted output (Python 3.6+).



## Part 4: Operator & Control Flow

### 4.1. Operator

#### 1. Arithmetic Operators

Operators for basic math: `+ - * / %`

```python
a, b=7,2
print(a/ b)
print(a// b)
```

#### 2. Relational Operators

`== != > < >= <=` — compare values.

```python
a=[1,2]
b=[1,2]
print(a== b)
print(a is b)
```

#### 3. Logical Operators

`Operator : and or not`

Both use **short-circuit evaluation** — the second condition is skipped if the first already determines the result. This prevents errors like division by zero.

```python
a, b=0,5
if a!=0 and(b/ a)>1:
print("safe")
```

#### 4. Bitwise Operators

`& | ^ ~ << >>` — operate on binary representation.

**Theory:**

- `&` (AND), `|` (OR), `^` (XOR), `~` (complement/NOT)
- `<<` shifts bits left (multiplies by 2ⁿ), `>>` shifts bits right (divides by 2ⁿ)
- XOR property: `x ^ x = 0` and `x ^ 0 = x` — used to find unique elements.
- `n & (n-1)` clears the lowest set bit — used to check powers of 2.

```python
n=5
print(n&1)
print(1<<3)
print(n&(n-1))
```

#### 5. Ternary / Conditional Expression

```python
max_val= a
if a> b
else b
```

### 4.2. Control Flow

#### 1. if / else if / else

Executes a block only if a condition is true; checks conditions top-to-bottom, stops at the first true one.

```python
marks=75
if marks>=90:
print("A grade")
elif marks>=75:
print("B grade")
else:
print("C grade")
```

#### 2. switch (Java) vs match-case (Python)

Used to compare one variable against multiple fixed values, as a cleaner alternative to long if-else chains.

```python
day=3
match day:
case1:
print("Mon")
case2:
print("Tue")
case_:
print("Invalid")
```

Python's `match-case` (3.10+) has **no fall-through issue** — each case is automatically isolated.

#### 3. Nested Conditions

```python
if a>0:
if b>0:
print("Both positive")
```

#### 4. Assignment-in-condition Gotcha

Java's compiler rejects `if (x = 5)` unless it evaluates to boolean, preventing an accidental assignment bug common in C-style languages. Python doesn't allow assignment in a plain condition at all — you need the **walrus operator** `:=` to intentionally assign inside an expression.

```python
if (x := 5) > 3:
    print(x)  
```
