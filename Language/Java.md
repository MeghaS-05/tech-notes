~ Invented by James Gosling and his team at Sun Microsystem in 1995. Current Owner of java is Oracle Corporation.*

## Part 1 : Introduction
Java is a high-level, objected oriented, class-based programming language which is platform independent and commonly described as “Write Once, Run Anywhere (WORA)”. Java is a Statically Typed language meaning the type of variable is known and checked before the program runs (usually at compile time).

Few Features of Java :
1. Platform Independent : It can run on any operating system with a compatible JVM.
2. Object Oriented : follows OOPs Principle
3. Secure : provides several security like Bytecode verification, class loader, security manager(legacy) etc.
4. Multithreaded : allows multiple threads to execute concurrently, improving application responsiveness and resource utilization.
5. High Performance : java achieve good performance through Just-in-time compilation , JVM optimization, Adaptive runtime optimization

Java continues to be one of the most in-demand programming languages due to its stability, ecosystem, and enterprise adoption.



## Part 2 : Variable & Datatype

2.1. Variable 
A **variable** is a named memory location (can refer as a container) used to store data that can change during the execution of a program. Variable have A name (identifier), A value, A data type.

| Variable Type | Meaning | Syntax |
| --- | --- | --- |
| Local Variable | Declared inside a method, constructor, or block. Accessible only within that scope. | `int age = 25;` |
| Instance Variable | Declared inside a class but outside methods. Each object has its own copy. | `class Student { int age = 20; }` |
| Static Variable (Class Variable) | Declared with the `static` keyword. Shared among all objects of the class. | `static int count = 0;` |

### Rules for Java Variables
- Variable names are **case-sensitive**.
- Must begin with a **letter**, **underscore (`_`)**, or **dollar sign (`$`)**.
- Cannot begin with a number.
- Cannot contain spaces.
- Cannot use Java keywords as variable names.
- Local variables must be initialized before use.
- Instance and static variables receive default values if not explicitly initialized.

### Valid Examples :
int age;
double salary;
String firstName;
boolean isActive;
int _count;
int $price;

### 2.2. DataType
| Data Type | Meaning | Java Syntax |
| --- | --- | --- |
| Integer | Stores whole numbers | `int age = 25;` |
| Floating Point | Stores decimal numbers | `double price = 99.99;` |
| Boolean | Stores `true` or `false` values | `boolean isActive = true;` |
| Character | Stores a single character | `char grade = 'A';` |
| String | Stores a sequence of characters | `String name = "John";` |
| List / Array | Stores multiple values | `int[] arr = {1, 2, 3};` |
| Tuple | Ordered immutable collection | *Not available* |
| Set | Stores unique elements | `Set<Integer> nums = Set.of(1,2,3);` |
| Dictionary / Map | Stores key-value pairs | `Map<String, Integer> map = new HashMap<>();` |
| Null / None | Represents absence of a value | `null` |
| Bytes | Stores binary data | `byte data = 10;` / `byte[] bytes = {...};` |



## Part 3 : Input & Output, Operator

### 3.1. Input & Ouput
Input is a process of providing data to a program for processing whereas output is the information produced by a program after processing the input.

Input
| Type | Syntax | Example |
| --- | --- | --- |
| User Input (Scanner) | `Scanner sc = new Scanner(System.in);` | `int age = sc.nextInt();` |
| String Input | `sc.nextLine();` | `String name = sc.nextLine();` |
| Decimal Input | `sc.nextDouble();` | `double salary = sc.nextDouble();` |
| Character Input | `sc.next().charAt(0);` | `char grade = sc.next().charAt(0);` |

Output:
| Type | Syntax | Example |
| --- | --- | --- |
| Normal Output | `System.out.print();` | `System.out.print("Hello");` |
| Output with New Line | `System.out.println();` | `System.out.println("Hello");` |
| Formatted Output | `System.out.printf();` | `System.out.printf("Age: %d", 20);` |

Note:
- Import `java.util.Scanner` before using `Scanner`.
- Close the `Scanner` object after use (`sc.close()`).
- Be careful when using `nextInt()` followed by `nextLine()` because the newline character remains in the input buffer.
- Use `printf()` when formatted output is required.



## Part 4 : Operator & Control Flow

### 4.1. Operator

#### 1. Arithmetic Operators

Operators for basic math: `+ - * / %`

- Java's `/` between two integers does **integer division** (truncates decimal part).
- **Modulo with negative numbers differs**: Java's result takes the sign of the *dividend*, Python's takes the sign of the *divisor*. This is a common bug source when translating code between languages.

```java

int a=7, b=2;
System.out.println(a/b);
```

#### 2. Relational Operators

`== != > < >= <=` — compare values.

**Theory:**

- Java: `==` on objects compares **memory reference**, not content → use `.equals()` for value comparison.
- Python: `==` compares **value**, `is` compares **identity** (memory reference).

```java
String s1=newString("hi");
String s2=newString("hi");
System.out.println(s1== s2);
```

#### 3. Logical Operators

`Operator : && || !`

**Theory:** Both use **short-circuit evaluation** — the second condition is skipped if the first already determines the result. This prevents errors like division by zero.

```java
int a=0, b=5;
if(a!=0&&(b/ a)>1){
System.out.println("safe");
}
```

#### 4. Bitwise Operators

`& | ^ ~ << >>` — operate on binary representation.

**Theory:**

- `&` (AND), `|` (OR), `^` (XOR), `~` (complement/NOT)
- `<<` shifts bits left (multiplies by 2ⁿ), `>>` shifts bits right (divides by 2ⁿ)
- XOR property: `x ^ x = 0` and `x ^ 0 = x` — used to find unique elements.
- `n & (n-1)` clears the lowest set bit — used to check powers of 2.

```java
int n=5;
System.out.println(n&1);
```

#### 5. Ternary / Conditional Expression

```java
int max=(a> b)? a: b;
```

### 4.2. Control Flow

#### 1. if / else if / else

Executes a block only if a condition is true; checks conditions top-to-bottom, stops at the first true one.

```java
int marks=75;
if(marks>=90){
  System.out.println("A grade");
}elseif(marks>=75){
  System.out.println("B grade");
}else{System.out.println("C grade");}
```

#### 2. switch (Java) vs match-case (Python)

Used to compare one variable against multiple fixed values, as a cleaner alternative to long if-else chains.

```java
int day=3;
switch(day){
case1:
System.out.println("Mon");
break;
case2:
System.out.println("Tue");
break;
default:
System.out.println("Invalid");
}
```

**Important:** Missing `break` causes **fall-through** — execution continues into the next case, a common bug.

#### 3. Nested Conditions

```java
if(a>0){
if(b>0){
System.out.println("Both positive");
}
}
```

#### 4. Assignment-in-condition Gotcha

**Theory:** Java's compiler rejects `if (x = 5)` unless it evaluates to boolean, preventing an accidental assignment bug common in C-style languages. Python doesn't allow assignment in a plain condition at all — you need the **walrus operator** `:=` to intentionally assign inside an expression.

```java
boolean flag;
if (flag = true) {
System.out.println("runs");
}
```
