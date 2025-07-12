# Foolang

Foolang is a modern, educational programming language inspired by C, Rust, and JavaScript. It features a tree-walking interpreter implemented in Rust, with comprehensive error handling, rich type system, and extensive standard library. Designed for learning, experimentation, and practical programming tasks.

---

## Table of Contents
1. [Overview](#1-overview)
2. [Lexical Structure](#2-lexical-structure)
3. [Types and Literals](#3-types-and-literals)
4. [Variables and Constants](#4-variables-and-constants)
5. [Operators](#5-operators)
6. [Control Flow](#6-control-flow)
7. [Functions](#7-functions)
8. [Structs and Enums](#8-structs-and-enums)
9. [Arrays](#9-arrays)
10. [Modules and Imports](#10-modules-and-imports)
11. [Native Functions](#11-native-functions)
12. [Casting and Byte Manipulation](#12-casting-and-byte-manipulation)
13. [Error Handling](#13-error-handling)
14. [Examples](#14-examples)
15. [How to Run](#15-how-to-run)
16. [Contributing](#16-contributing)
17. [Language Reference](#17-language-reference-summary-table)

---

## 1. Overview
Foolang is a dynamically-typed, block-scoped, imperative language with C-like syntax and modern features. It supports:
- **Rich Type System**: Integers, floats, strings, chars, arrays, structs, enums
- **Comprehensive Operators**: Arithmetic, logical, bitwise, assignment, increment/decrement
- **Control Structures**: If-else, while loops, for loops, break/continue
- **Functions**: User-defined functions with parameters and return values
- **Standard Library**: 20+ built-in functions for I/O, string manipulation, file operations
- **Module System**: File imports with `grab` statement
- **Error Handling**: Precise error reporting with file, line, and column information
- **Memory Management**: Automatic memory management via Rust's ownership system

---

## 2. Lexical Structure
- **Identifiers**: `[a-zA-Z_][a-zA-Z0-9_]*`
- **Keywords**: `ty`, `const`, `if`, `else`, `while`, `for`, `function`, `omeo`, `struct`, `new`, `enum`, `grab`, `miala`, `andana`, `true`, `false`, `NULL`
- **Comments**:
  - Single-line: `// ...`
  - Multi-line: `/* ... */`
- **Literals**:
  - Integer: `42`, `-7`, `0xFF`, `0b1010`, `0o77`
  - Float: `3.14`, `-0.5`
  - String: `"hello"`, supports escapes (`\n`, `\t`, `\"`, `\\`)
  - Char: `'a'`, `'\n'`
- **Whitespace**: Spaces, tabs, newlines (ignored except as separators)

---

## 3. Types and Literals

### Supported Types

- **Integer** (`int`): 64-bit signed integer (e.g., `42`, `-7`, `0xFF`, `0b1010`, `0o77`)
- **Float** (`float`): 64-bit IEEE754 floating point (e.g., `3.14`, `-0.5`)
- **Boolean** (`bool`): `true` (1), `false` (0)
- **String** (`string`): UTF-8 encoded, supports escape sequences (e.g., `"hello"`, `"line\\nbreak"`)
- **Char** (`char`): Single Unicode codepoint (e.g., `'a'`, `'\n'`)
- **Array** (`array`): Dynamic, can hold mixed types (e.g., `[1, 2, 3]`, `[1, "foo", 3.14]`)
- **Struct**: Custom data type with named fields (see Structs section)
- **Enum**: Custom tagged union with optional values (see Enums section)

### Literals

#### Integer Literals

- **Decimal**: `123`, `-42`
- **Hexadecimal**: `0xFF` (255)
- **Binary**: `0b1010` (10)
- **Octal**: `0o12` (10)

#### Float Literals

- `3.14`, `-0.5`, `2.0`, `1e-3`

#### Boolean Literals

- `true` (internally `1`)
- `false` (internally `0`)

#### String Literals

- `"hello"`
- `"line\nbreak"` (interpreted as `line\nbreak`)
- Supports: `\n`, `\t`, `\r`, `\"`, `\\`

#### Char Literals

- `'a'`, `'\n'`, `'\''`

#### Array Literals

- `[1, 2, 3]`
- `[1, "foo", 3.14, true]`

### Type Coercion and Conversion

- **Automatic conversion**:
  - `int` ↔ `float`: Arithmetic operations automatically convert as needed.
  - `int`/`float` ↔ `string`: Using `+` with a string converts the other operand to string.
  - `char` ↔ `int`: Use `ord()` and `chr()` for conversion.
- **Explicit conversion**:
  - Use built-in functions: `to_string()`, `to_int()`, `to_i8()`, `to_i16()`, `to_i32()`, etc.

#### Examples

```fg
ty a = 5 + 2.5;        // 7.5 (float)
ty s = "foo" + 42;     // "foo42"
ty c = 'A';
ty code = ord(c);      // 65
ty ch = chr(66);       // 'B'
ty arr = [1, "two", 3.0, true];
hurle(arr[1]);         // "two"
```

### Type Checking and Errors

- **Invalid operation**:
  ```
  Runtime error: Cannot apply bitwise operator to float
  ```
- **Invalid conversion**:
  ```
  Runtime error: Cannot convert string 'abc' to int
  ```
- **Out-of-bounds access**:
  ```
  Runtime error: Index 5 out of bounds for array of length 3
  ```

### Advanced Examples

```fg
ty nums = [1, 2, 3];
push(nums, 4.5);
hurle(nums); // [1, 2, 3, 4.5]

ty s = "Result: " + (2 * 3);
hurle(s); // "Result: 6"

ty b = true;
hurle(b + 1); // 2

ty f = 2.5;
ty i = to_int(f); // 2
```

---

## 4. Variables and Constants

### Variable Declaration

- **Syntax**:  
  ```fg
  ty name = value;
  ```
  Example:
  ```fg
  ty x = 42;
  ty name = "Foolang";
  ty pi = 3.14;
  ```

- **Allowed types**:  
  Variables can hold any type: integer, float, boolean, string, array, struct, enum, etc.

### Constant Declaration

- **Syntax**:  
  ```fg
  const NAME = value;
  ```
  Example:
  ```fg
  const PI = 3.14159;
  const MAX = 1000;
  ```

- **Rules**:  
  - Constants are immutable: any attempt to modify them will cause an error.
  - Constant names follow the same rules as variables, but uppercase is recommended by convention.

### Scope

- **Block scope**:  
  Variables and constants are only visible within the block where they are declared.
  ```fg
  ty x = 1;
  if (true) {
      ty x = 2; // Shadowing: this variable hides the previous one in this block
      hurle(x); // Prints 2
  }
  hurle(x); // Prints 1
  ```

- **Function scope**:  
  Function parameters and local variables are only visible inside the function.

### Shadowing

- You can redeclare a variable with the same name in a nested block (shadowing).
- Native constants (`true`, `false`, `NULL`) can never be redeclared.

### Assignment and Reassignment

- **Reassignment**:  
  ```fg
  ty x = 10;
  x = 20; // OK
  ```
- **Constant**:  
  ```fg
  const PI = 3.14;
  PI = 3.1415; // Error: cannot modify a constant
  ```

### Compound Assignment Operators

- `+=`, `-=`, `*=`, `/=`, `%=` are supported for mutable variables.

### Increment/Decrement

- Both postfix and prefix: `x++`, `++x`, `x--`, `--x`

### Possible Errors

- **Redeclaring a native constant**:
  ```
  Error: Cannot redefine native constant 'true'
  ```
- **Redeclaring a constant**:
  ```
  Error: Cannot redefine constant 'PI'
  ```
- **Modifying a constant**:
  ```
  Error: Cannot assign to constant 'MAX'
  ```
- **Using an undeclared variable**:
  ```
  Runtime error: Variable 'foo' not defined
  ```
- **Using a reserved name**:
  ```
  Error: Cannot use reserved name 'NULL' as variable or constant
  ```

### Advanced Examples

```fg
ty counter = 0;
counter += 1;
counter++;
hurle(counter); // 2

const VERSION = "1.0.0";
hurle(VERSION);

if (true) {
    ty counter = 100; // Shadowing
    hurle(counter); // 100
}
hurle(counter); // 2

// Error: redeclaring a native constant
const true = 1; // Error: Cannot redefine native constant 'true'
```

---

## 5. Operators

### Arithmetic Operators

| Operator | Description         | Supported Types      | Example         | Result   |
|----------|---------------------|----------------------|-----------------|----------|
| `+`      | Addition/Concat     | int, float, string   | `2 + 3`         | `5`      |
|          |                     |                      | `"foo" + "bar"` | `"foobar"` |
|          |                     |                      | `"foo" + 42`    | `"foo42"` |
| `-`      | Subtraction         | int, float           | `5 - 2`         | `3`      |
| `*`      | Multiplication      | int, float           | `4 * 2`         | `8`      |
| `/`      | Division            | int, float           | `8 / 2`         | `4`      |
| `%`      | Modulo              | int                  | `7 % 3`         | `1`      |

- **String concatenation**: Using `+` with a string and any other value will convert the value to a string and concatenate.
- **Integer division**: `/` on integers performs truncated division.
- **Division by zero**: Triggers a runtime error (see below).

### Assignment Operators

| Operator | Description              | Example     | Result         |
|----------|--------------------------|-------------|----------------|
| `=`      | Simple assignment        | `x = 5`     | `x is 5`       |
| `+=`     | Add and assign           | `x += 2`    | `x = x + 2`    |
| `-=`     | Subtract and assign      | `x -= 1`    | `x = x - 1`    |
| `*=`     | Multiply and assign      | `x *= 3`    | `x = x * 3`    |
| `/=`     | Divide and assign        | `x /= 2`    | `x = x / 2`    |
| `%=`     | Modulo and assign        | `x %= 4`    | `x = x % 4`    |

### Comparison Operators

| Operator | Description         | Example     | Result         |
|----------|---------------------|-------------|----------------|
| `==`     | Equal               | `x == 2`    | `true`/`false` |
| `!=`     | Not equal           | `x != 3`    | `true`/`false` |
| `<`      | Less than           | `x < 5`     | `true`/`false` |
| `>`      | Greater than        | `x > 1`     | `true`/`false` |
| `<=`     | Less or equal       | `x <= 2`    | `true`/`false` |
| `>=`     | Greater or equal    | `x >= 0`    | `true`/`false` |

### Logical Operators

| Operator | Description         | Example     | Result         |
|----------|---------------------|-------------|----------------|
| `&&`     | Logical AND         | `a && b`    | `true`/`false` |
| `||`     | Logical OR          | `a || b`    | `true`/`false` |
| `!`      | Logical NOT         | `!a`        | boolean negation |

- **Short-circuit**: `&&` and `||` do not evaluate the right-hand side if the result is already determined.

### Bitwise Operators (integers only)

| Operator | Description         | Example     | Result   |
|----------|---------------------|-------------|----------|
| `&`      | Bitwise AND         | `5 & 3`     | `1`      |
| `|`      | Bitwise OR          | `5 | 2`     | `7`      |
| `^`      | Bitwise XOR         | `5 ^ 1`     | `4`      |
| `~`      | Bitwise NOT         | `~2`        | `-3`     |
| `<<`     | Left shift          | `1 << 2`    | `4`      |
| `>>`     | Right shift         | `8 >> 1`    | `4`      |

### Increment/Decrement Operators

- **Postfix**: `x++`, `x--`
- **Prefix**: `++x`, `--x`
- Only valid for integer variables.

### Access Operators

- **Struct field**: `obj.field`
- **Array/String index**: `arr[0]`, `str[1]`
- **Enum variant**: `Enum::Variant`

### Operator Precedence

See the precedence table above for full details.

---

#### Possible Operator Errors

- **Division by zero**:
  ```
  Runtime error: Division by zero
  ```
- **Bitwise operator on non-integer**:
  ```
  Runtime error: Bitwise operations only allowed on integers
  ```
- **Index out of bounds**:
  ```
  Runtime error: Index 5 out of bounds for array of length 3
  ```

---

#### Advanced Examples

```fg
ty a = 5;
ty b = 2;
hurle(a + b * 3); // 11

ty s = "foo" + "bar";
hurle(s); // "foobar"

ty x = 10;
x /= 2;
x++;
hurle(x); // 6

ty arr = [1, 2, 3];
hurle(arr[1]); // 2

ty mask = 0b1010;
hurle(mask | 0b0101); // 15

if (a > 0 && b < 10) {
    hurle("ok");
}
```

---

## 6. Control Flow

### Conditional Statements

Foolang supports classic `if`/`else` branching.

**Syntax:**
```fg
if (condition) {
    // code if condition is true
} else {
    // code if condition is false
}
```

**Example:**
```fg
ty x = 10;
if (x > 5) {
    hurle("x is greater than 5");
} else {
    hurle("x is not greater than 5");
}
```

---

### While Loops

**Syntax:**
```fg
while (condition) {
    // code to repeat
}
```

**Example:**
```fg
ty i = 0;
while (i < 3) {
    hurle(i);
    i++;
}
```

---

### For Loops (C-style)

**Syntax:**
```fg
for (ty i = 0; i < 5; i++;) {
    // code to repeat
}
```

- The for loop consists of an initialization, a condition, and an increment statement, separated by semicolons.
- The initialization can declare a new variable with `ty`.

**Example:**
```fg
for (ty i = 0; i < 5; i++;) {
    hurle(i);
}
```

---

### Loop Control: `miala` and `andana`

- **`miala;`**: Exits the nearest enclosing loop (`while` or `for`).
- **`andana;`**: Skips to the next iteration of the nearest enclosing loop.

**Example:**
```fg
for (ty i = 0; i < 5; i++;) {
    if (i == 2) {
        andana;
    }
    if (i == 4) {
        miala;
    }
    hurle(i);
}
// Output: 0, 1, 3
```

---

### Nested Loops

`miala` and `andana` always affect the **innermost** loop in which they appear.

**Example:**
```fg
for (ty i = 0; i < 3; i++;) {
    for (ty j = 0; j < 3; j++;) {
        if (j == 1) {
            andana;
        }
        if (i == 2 && j == 2) {
            miala;
        }
        hurle(i, j);
    }
}
// Output: 0 0, 0 2, 1 0, 1 2, 2 0
```

---

### Possible Errors

- **Infinite loop**: No error, but may hang your program if the condition never becomes false.
- **Invalid use of `miala` or `andana` outside a loop**:
  ```
  Runtime error: 'miala' or 'andana' used outside of a loop
  ```
- **Non-boolean condition**: Any value is accepted; `0` is false, all others are true.

---

### Advanced Examples

```fg
ty sum = 0;
for (ty i = 1; i <= 10; i++;) {
    if (i % 2 == 0) {
        andana;
    }
    sum += i;
}
hurle(sum); // 25 (sum of odd numbers from 1 to 10)

ty n = 5;
while (n > 0) {
    hurle(n);
    n--;
    if (n == 2) {
        miala;
    }
}
hurle("done");
```

---

## 7. Functions

### Function Declaration

Functions in foolang are declared using the `function` keyword.

**Syntax:**
```fg
function name(param1, param2, ...) {
    // function body
}
```

**Example:**
```fg
function add(a, b) {
    omeo a + b;
}
ty result = add(5, 3);
hurle(result); // 8
```

- Functions can have any number of parameters.
- Parameters are passed by value.
- The function body must be enclosed in braces `{}`.

---

### Return Values

- Use the `omeo` keyword to return a value from a function.
- If no `omeo` is encountered, the function returns `NULL` by default.

**Example:**
```fg
function square(x) {
    omeo x * x;
}
hurle(square(4)); // 16
```

---

### Scope

- Function parameters and local variables are only visible inside the function.
- Variables declared inside a function shadow variables with the same name in outer scopes.

**Example:**
```fg
ty x = 10;
function test(x) {
    hurle(x); // prints the parameter, not the outer variable
}
test(42); // prints 42
hurle(x); // prints 10
```

---

### Recursion

Functions can call themselves recursively.

**Example:**
```fg
function factorial(n) {
    if (n <= 1) {
        omeo 1;
    } else {
        omeo n * factorial(n - 1);
    }
}
hurle(factorial(5)); // 120
```

---

### Multiple Parameters

**Example:**
```fg
function calculate(a, b, c) {
    omeo a * b + c;
}
hurle(calculate(2, 3, 4)); // 10
```

---

### Possible Errors

- **Calling an undefined function:**
  ```
  Runtime error: Function 'foo' not defined
  ```
- **Wrong number of arguments:**
  ```
  Runtime error: Function 'add' expects 2 arguments, got 1
  ```
- **Using reserved names as parameters:**
  ```
  Error: Cannot use reserved name 'true' as parameter
  ```

---

### Advanced Examples

```fg
function greet(name) {
    hurle("Hello, " + name + "!");
}

function sum_all(arr) {
    ty total = 0;
    for (ty i = 0; i < len(arr); i++;) {
        total += arr[i];
    }
    omeo total;
}

greet("foolang");
ty numbers = [1, 2, 3, 4];
hurle(sum_all(numbers)); // 10

// Recursive Fibonacci
function fib(n) {
    if (n <= 1) {
        omeo n;
    }
    omeo fib(n - 1) + fib(n - 2);
}
hurle(fib(6)); // 8
```

---

## 8. Structs and Enums

### Structs

Structs are custom data types that group named fields together.

#### Declaration

**Syntax:**
```fg
struct StructName {
    field1,
    field2,
    ...
}
```

**Example:**
```fg
struct Point {
    x,
    y
}
```

#### Instantiation

Create a new struct instance using the `new` keyword and field initializers.

**Example:**
```fg
ty p = new Point { x: 10, y: 20 };
```

#### Field Access and Modification

Access or modify struct fields using the dot `.` operator.

**Example:**
```fg
hurle(p.x); // 10
p.x = 15;
hurle(p.x); // 15
```

#### Nested Structs

Structs can contain other structs as fields.

**Example:**
```fg
struct Address {
    street,
    city,
    zip
}

struct Person {
    name,
    age,
    address
}

ty addr = new Address { street: "123 Main St", city: "Paris", zip: "75001" };
ty person = new Person { name: "Alice", age: 30, address: addr };
hurle(person.address.street); // "123 Main St"
```

---

### Enums

Enums are custom types that represent a set of named variants, optionally with explicit integer values.

#### Declaration

**Syntax:**
```fg
enum EnumName {
    Variant1,
    Variant2 = value,
    ...
}
```

**Example:**
```fg
enum Color {
    Red,
    Green = 2,
    Blue,
    Yellow = 10
}
```

#### Usage and Comparison

Create enum values and compare them using `==`.

**Example:**
```fg
ty c = Color::Green;
if (c == Color::Green) {
    hurle("It's green!");
}
```

#### Features

- Variants can have explicit integer values; otherwise, values increment from the previous.
- Enum values can be compared for equality.
- Enum variants can be accessed using the `::` operator.

---

### Possible Errors

- **Accessing an undefined field:**
  ```
  Runtime error: Struct 'Point' has no field 'z'
  ```
- **Missing field during instantiation:**
  ```
  Runtime error: Missing field 'y' in struct 'Point'
  ```
- **Unknown enum variant:**
  ```
  Runtime error: Enum 'Color' has no variant 'Purple'
  ```
- **Assigning to a non-existent field:**
  ```
  Runtime error: Cannot assign to field 'foo' in struct 'Point'
  ```

---

### Advanced Examples

```fg
struct Rectangle {
    width,
    height
}

function area(rect) {
    omeo rect.width * rect.height;
}

ty r = new Rectangle { width: 5, height: 3 };
hurle(area(r)); // 15

enum Status {
    Ok = 0,
    Warning = 1,
    Error = 2
}

function check_status(s) {
    if (s == Status::Error) {
        hurle("An error occurred!");
    } else if (s == Status::Warning) {
        hurle("Warning!");
    } else {
        hurle("All good.");
    }
}

ty s = Status::Warning;
check_status(s); // "Warning!"
```

---

## 9. Arrays

Arrays in foolang are dynamic and can hold values of any type, including mixed types.

### Declaration

**Syntax:**
```fg
ty arr = [value1, value2, ...];
```

**Examples:**
```fg
ty numbers = [1, 2, 3, 4, 5];
ty mixed = [1, "hello", 3.14, true];
```

---

### Access and Modification

- Access elements by zero-based index using square brackets.
- Assign new values to elements by index.

**Examples:**
```fg
hurle(numbers[0]); // 1
numbers[1] = 10;   // Modify element
hurle(numbers);    // [1, 10, 3, 4, 5]
```

---

### Array Operations

Foolang provides several built-in functions for array manipulation:

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `len(array)`            | Get array length                   | `len(numbers)`                 | `5`                   |
| `push(array, value)`    | Add element to end                 | `push(numbers, 6)`             | `[1,2,3,4,5,6]`       |
| `pop(array)`            | Remove and return last element     | `pop(numbers)`                 | `5` (and array is `[1,2,3,4]`) |
| `contains(array, val)`  | Check if value exists in array     | `contains(numbers, 3)`         | `1` (true)            |

**Examples:**
```fg
ty fruits = ["apple", "banana", "orange"];
hurle(len(fruits)); // 3

push(fruits, "kiwi");
hurle(fruits); // ["apple", "banana", "orange", "kiwi"]

ty last = pop(fruits);
hurle(last); // "kiwi"

hurle(contains(fruits, "banana")); // 1 (true)
hurle(contains(fruits, "grape"));  // 0 (false)
```

---

### Features

- **Dynamic Size**: Arrays can grow and shrink at runtime.
- **Heterogeneous**: Arrays can hold values of different types.
- **Zero-based Indexing**: The first element is at index 0.
- **Bounds Checking**: Accessing an out-of-bounds index triggers a runtime error.

---

### Possible Errors

- **Index out of bounds:**
  ```
  Runtime error: Index 5 out of bounds for array of length 3
  ```
- **Invalid operation on non-array:**
  ```
  Runtime error: Attempted to use array function on non-array value
  ```

---

### Advanced Examples

```fg
ty arr = [1, 2, 3];
push(arr, 4.5);
hurle(arr); // [1, 2, 3, 4.5]

for (ty i = 0; i < len(arr); i++;) {
    hurle("Element", i, ":", arr[i]);
}

ty empty = [];
push(empty, "first");
hurle(empty); // ["first"]

// Nested arrays
ty matrix = [
    [1, 2],
    [3, 4]
];
hurle(matrix[1][0]); // 3
```

---

## 10. Modules and Imports

Foolang supports modular programming by allowing you to import code from other files using the `grab` statement.

### Importing Modules

**Syntax:**
```fg
grab "filename.fg";
```

- The `grab` statement imports and executes the contents of another `.fg` file.
- The path can be relative or absolute.
- Each file is imported only once, even if `grab` is called multiple times (idempotent import).

**Example:**
```fg
grab "math_utils.fg";
hurle(add(2, 3)); // Uses function from math_utils.fg
```

---

### How Imports Work

- Imported code is executed in the global scope of the importing file.
- Functions, constants, structs, enums, and variables defined in the imported file become available in the importing file.
- If an imported file itself uses `grab`, its dependencies are also loaded (once each).

---

### File Context and Error Reporting

- Errors in imported files show the correct file name, line, and column for precise debugging.
- The import stack is tracked, so you always know where an error originated.

---

### Possible Errors

- **File not found:**
  ```
  Error: unable to read file 'utils.fg': No such file or directory
  ```
- **Circular import:**
  ```
  Error: Circular import detected for file 'a.fg'
  ```
- **Syntax or runtime error in imported file:**
  ```
  Runtime error in file 'math_utils.fg' at line 5, column 10: Division by zero
  ```

---

### Advanced Examples

```fg
// In math_utils.fg
function add(a, b) {
    omeo a + b;
}
const PI = 3.14159;

// In main.fg
grab "math_utils.fg";
hurle(add(10, 20)); // 30
hurle(PI);          // 3.14159

// Nested import
// In a.fg
grab "b.fg";
ty x = 1;

// In b.fg
grab "c.fg";
ty y = 2;

// In c.fg
ty z = 3;

// In main.fg
grab "a.fg";
// x, y, z are all available after import
hurle(x, y, z); // 1 2 3
```

---

## 11. Native Functions

Foolang provides a comprehensive standard library of built-in functions for I/O, string and array manipulation, type conversion, file operations, and more.

### Input/Output

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `hurle(...)`            | Print values to the console        | `hurle("Hello", 42)`         | Prints: `Hello 42`    |
| `input()`               | Read a line from user input        | `ty name = input();`           | User input as string  |

---

### String Functions

| Function                        | Description                        | Example                        | Result                |
|----------------------------------|------------------------------------|------------------------------- |-----------------------|
| `len(string)`                    | Get string length                  | `len("abc")`                 | `3`                   |
| `substring(string, start, end)`  | Extract substring                  | `substring("hello", 1, 4)`   | `"ell"`               |
| `to_string(value)`               | Convert value to string            | `to_string(42)`                | `"42"`                |
| `to_int(string)`                 | Convert string to integer          | `to_int("123")`              | `123`                 |

---

### Character Functions

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `ord(char)`             | Get Unicode code of character       | `ord('A')`                     | `65`                  |
| `chr(code)`             | Get character from Unicode code     | `chr(66)`                      | `'B'`                 |

---

### Array Functions

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `len(array)`            | Get array length                   | `len([1,2,3])`                 | `3`                   |
| `push(array, value)`    | Add element to array               | `push(arr, 4)`                 | arr becomes `[1,2,3,4]`|
| `pop(array)`            | Remove and return last element     | `pop(arr)`                     | Returns last element  |
| `contains(array, val)`  | Check if value exists in array     | `contains(arr, 2)`             | `1` (true) or `0` (false) |

---

### Type Conversion Functions

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `to_i8(value)`          | Convert to 8-bit integer           | `to_i8(300)`                   | `44` (overflow wraps) |
| `to_i16(value)`         | Convert to 16-bit integer          | `to_i16(70000)`                | `4464` (overflow wraps)|
| `to_i32(value)`         | Convert to 32-bit integer          | `to_i32(1e10)`                 | Overflow wraps        |

---

### File I/O Functions

| Function                        | Description                        | Example                        | Result                |
|----------------------------------|------------------------------------|------------------------------- |-----------------------|
| `read_file(filename)`            | Read file content as string        | `read_file("test.txt")`      | File content          |
| `write_file(filename, content)`  | Write content to file              | `write_file("a.txt", "hi")`| Writes to file        |
| `append_file(filename, content)` | Append content to file             | `append_file("a.txt", "!")`| Appends to file       |
| `file_exists(filename)`          | Check if file exists               | `file_exists("a.txt")`       | `1` (true) or `0` (false) |

---

### Bit Manipulation Functions

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `to_bin(value)`         | Convert to binary string            | `to_bin(10)`                   | `"0b1010"`            |
| `to_hex(value)`         | Convert to hexadecimal string       | `to_hex(255)`                  | `"0xff"`              |
| `to_oct(value)`         | Convert to octal string             | `to_oct(8)`                    | `"0o10"`              |

---

### Examples

```fg
// String operations
ty message = "Hello, World!";
hurle(len(message)); // 13
hurle(substring(message, 0, 5)); // "Hello"

// File operations
write_file("test.txt", "Hello from Foolang!");
ty content = read_file("test.txt");
hurle(content); // "Hello from Foolang!"

// Type conversions
ty num = 255;
hurle(to_bin(num)); // "0b11111111"
hurle(to_hex(num)); // "0xff"
hurle(to_oct(num)); // "0o377"
```

---

### Possible Errors

- **Invalid argument type:**
  ```
  Runtime error: Expected string, got int
  ```
- **File not found:**
  ```
  Error: unable to read file 'missing.txt': No such file or directory
  ```
- **Conversion error:**
  ```
  Runtime error in file 'grab.fg' at line 1, column 7 : to_int() invalid conversion for 'abc'
  ```
- **Index out of bounds (for arrays):**
  ```
  Runtime error: Index 10 out of bounds for array of length 3
  ```

---

## 12. Casting and Byte Manipulation

Foolang provides comprehensive type casting and bit manipulation capabilities for low-level programming tasks.

### Numeric Type Casting

#### Integer Type Casting

Foolang supports casting to different integer sizes with overflow behavior similar to C/Rust:

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `to_i8(value)`          | Cast to 8-bit signed integer       | `to_i8(300)`                   | `44` (overflow wraps) |
| `to_i16(value)`         | Cast to 16-bit signed integer      | `to_i16(70000)`                | `4464` (overflow wraps)|
| `to_i32(value)`         | Cast to 32-bit signed integer      | `to_i32(1e10)`                 | Overflow wraps        |

- **Overflow behavior**: Values that exceed the target type's range wrap around (modulo arithmetic).
- **Float truncation**: Floats are truncated to integers before casting.
- **Negative values**: Preserved during casting with proper sign extension.

**Examples:**
```fg
hurle(to_i8(300));   // 44 (300 % 256)
hurle(to_i8(-300));  // -44
hurle(to_i16(70000)); // 4464 (70000 % 65536)
```

---

### Bit Representation Functions

#### Binary, Hexadecimal, and Octal Conversion

| Function                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `to_bin(value)`         | Convert to binary string            | `to_bin(10)`                   | `"0b1010"`            |
| `to_hex(value)`         | Convert to hexadecimal string       | `to_hex(255)`                  | `"0xff"`              |
| `to_oct(value)`         | Convert to octal string             | `to_oct(8)`                    | `"0o10"`              |

- **Integer values**: Converted to their binary/hex/octal representation.
- **Float values**: The IEEE754 bit pattern is used (as in Rust/C).
- **String format**: All functions return strings with appropriate prefixes (`0b`, `0x`, `0o`).

**Examples:**
```fg
ty x = 254;
hurle(to_bin(x)); // "0b11111110"
hurle(to_hex(x)); // "0xff"
hurle(to_oct(x)); // "0o376"

ty y = 3.14;
hurle(to_bin(y)); // "0b0100000000001001000111101011100001010001111010111000010100011111"
hurle(to_hex(y)); // "0x40091eb851eb851f"
```

---

### Bitwise Operations

Foolang supports all standard bitwise operations on integers:

| Operator                | Description                        | Example                        | Result                |
|-------------------------|------------------------------------|------------------------------- |-----------------------|
| `&`                     | Bitwise AND                         | `5 & 3`                        | `1`                   |
| `|`                     | Bitwise OR                          | `5 | 2`                        | `7`                   |
| `^`                     | Bitwise XOR                         | `5 ^ 1`                        | `4`                   |
| `~`                     | Bitwise NOT                         | `~2`                           | `-3`                  |
| `<<`                    | Left shift                          | `1 << 2`                       | `4`                   |
| `>>`                    | Right shift                         | `8 >> 1`                       | `4`                   |

**Examples:**
```fg
ty a = 0b1010;  // 10
ty b = 0b1100;  // 12
hurle(a & b);   // 8 (0b1000)
hurle(a | b);   // 14 (0b1110)
hurle(a ^ b);   // 6 (0b0110)
hurle(~a);      // -11
hurle(a << 1);  // 20 (0b10100)
hurle(a >> 1);  // 5 (0b101)
```

---

### Advanced Examples

```fg
// Bit manipulation for flags
const FLAG_READ = 1;      // 0b001
const FLAG_WRITE = 2;     // 0b010
const FLAG_EXEC = 4;      // 0b100

ty permissions = FLAG_READ | FLAG_WRITE; // 0b011 (3)
hurle(permissions & FLAG_READ);  // 1 (true)
hurle(permissions & FLAG_EXEC);  // 0 (false)

// Type casting with overflow
ty large_num = 1000000;
hurle(to_i8(large_num));  // 64 (1000000 % 256)

// Bit pattern analysis
ty value = 42;
hurle("Binary:", to_bin(value));
hurle("Hex:", to_hex(value));
hurle("Octal:", to_oct(value));

// Float bit pattern
ty pi = 3.14159;
hurle("Float bits:", to_bin(pi));
```

---

### Possible Errors

- **Bitwise operations on non-integers:**
  ```
  Runtime error: Bitwise operations only allowed on integers
  ```
- **Invalid casting:**
  ```
  Runtime error: Cannot cast string to integer type
  ```

---

## 13. Error Handling

Foolang provides comprehensive error handling with precise location reporting and clear error messages to help developers debug their code effectively.

### Error Types

#### Lexical Errors
Errors that occur during the tokenization phase when the lexer encounters invalid characters or malformed literals.

**Examples:**
```
Lexical error at line 3, column 15: An unknown character '#' slipped into your code...
Lexical error at line 5, column 8: Expected digits after prefix '0x'
Lexical error at line 2, column 12: Missing closing apostrophe for character literal
```

#### Syntax Errors
Errors that occur during parsing when the code structure doesn't match the language grammar.

**Examples:**
```
Error at line 4, column 12: expected Semicolon, found Identifier
Error at line 7, column 8: expected RParen, found LBrace
Error at line 3, column 15: expected Identifier, found Number
```

#### Runtime Errors
Errors that occur during program execution, such as division by zero, out-of-bounds access, or undefined variables.

**Examples:**
```
Runtime error in file 'test.fg' at line 5, column 10: Division by zero
Runtime error in file 'test.fg' at line 3, column 8: Unknown variable 'c'
Runtime error in file 'test.fg' at line 5, column 7: Array index out of bounds (index 4)
```

#### Type Errors
Errors that occur when operations are performed on incompatible types.

**Examples:**
```
Runtime error: Bitwise operations only allowed on integers
Runtime error in file 'grab.fg' at line 1, column 7: to_int() invalid conversion for 'abc'
Runtime error: Expected string, got int
```

---

### Error Reporting Features

#### Precise Location Information
All errors include:
- **File name**: The exact file where the error occurred
- **Line number**: The exact line of the error
- **Column number**: The exact column position
- **Error message**: Clear description of the problem

#### Import Error Tracking
When errors occur in imported files, the complete file context is preserved:

```
Runtime error in file 'math_utils.fg' at line 5, column 10: Division by zero
```

---

### Common Error Categories

#### Variable and Constant Errors
- **Undefined variable**: `Runtime error in file 'code.fg' at line 3, column 8: Unknown variable 'c'`
- **Redeclaring constants**: `Error: Cannot redefine constant 'PI'`
- **Using reserved names**: `Error: Cannot use reserved name 'NULL' as variable`

#### Function Errors
- **Undefined function**: `Runtime error: Function 'foo' not defined`
- **Wrong argument count**: `Runtime error: Function 'add' expects 2 arguments, got 1`
- **Invalid parameters**: `Error: Cannot use reserved name 'true' as parameter`

#### Array and String Errors
- **Index out of bounds**: `Runtime error in file 'code.fg' at line 5, column 7: Array index out of bounds (index 4)`
- **Invalid array operation**: `Runtime error: Attempted to use array function on non-array value`

#### File I/O Errors
- **File not found**: `Cannot read imported file 'missing.txt'`
- **Circular import**: `Error: Circular import detected for file 'a.fg'`

---

### Error Prevention Strategies

#### Bounds Checking
- Array and string access is automatically bounds-checked
- Out-of-bounds access triggers immediate runtime errors

#### Type Safety
- Automatic type conversion with clear error messages
- Explicit type checking for operations that require specific types

#### Scope Validation
- Variables must be declared before use
- Function parameters are validated at call time

#### Constant Protection
- Built-in constants (`true`, `false`, `NULL`) cannot be redefined
- User-defined constants are immutable

---

## 14. Examples

This section provides comprehensive examples demonstrating Foolang's features and capabilities.

### Basic Examples

#### Hello World
```fg
hurle("Hello, Foolang!");
```

#### Variables and Arithmetic
```fg
ty x = 10;
ty y = 20;
ty sum = x + y;
hurle("Sum:", sum); // Sum: 30
```

#### String Operations
```fg
ty name = "Foolang";
ty version = "1.0";
ty message = "Welcome to " + name + " " + version;
hurle(message); // Welcome to Foolang 1.0
```

---

### Control Flow Examples

#### Conditional Statements
```fg
ty age = 18;
if (age >= 18) {
    hurle("You are an adult\n");
} else {
    hurle("You are a minor\n");
}
```

#### Loops
```fg
// While loop
ty i = 0;
while (i < 5) {
    hurle(i, "\n");
    i++;
}

// For loop
for (ty j = 0; j < 3; j++;) {
    hurle("Count:", j, "\n");
}
```

#### Loop Control
```fg
for (ty k = 0; k < 10; k++;) {
    if (k == 3) {
        andana; // Skip 3
    }
    if (k == 7) {
        miala; // Exit at 7
    }
    hurle(k, "\n");
}
// Output: 0, 1, 2, 4, 5, 6
```

---

### Function Examples

#### Simple Function
```fg
function greet(name) {
    omeo "Hello, " + name + "!";
}

ty message = greet("Alice");
hurle(message, "\n"); // Hello, Alice!
```

#### Recursive Function
```fg
function factorial(n) {
    if (n <= 1) {
        omeo 1;
    } else {
        omeo n * factorial(n - 1);
    }
}

hurle(factorial(5), "\n"); // 120
```

#### Multiple Parameters
```fg
function calculate(a, b, operation) {
    if (operation == "add") {
        omeo a + b;
    } else if (operation == "multiply") {
        omeo a * b;
    } else {
        omeo 0;
    }
}

hurle(calculate(5, 3, "add"), "\n"); // 8
hurle(calculate(5, 3, "multiply"), "\n"); // 15
```

---

### Data Structure Examples

#### Arrays
```fg
ty numbers = [1, 2, 3, 4, 5];
push(numbers, 6);
hurle(numbers, "\n"); // [1, 2, 3, 4, 5, 6]

ty last = pop(numbers);
hurle("Last element:", last, "\n"); // Last element: 6

for (ty i = 0; i < len(numbers); i++;) {
    hurle("Element", i, ":", numbers[i], "\n");
}
```

#### Structs
```fg
struct Person {
    name,
    age,
    city
}

ty person = new Person { name: "Bob", age: 30, city: "Paris" };
hurle(person.name, "is", person.age, "years old\n");

person.age = 31;
hurle("Updated age:", person.age, "\n");
```

#### Enums
```fg
enum Status {
    Pending = 0,
    Active = 1,
    Completed = 2,
    Cancelled = 3
}

ty task_status = Status::Active;
if (task_status == Status::Active) {
    hurle("Task is active\n");
}
```

---

### File I/O Examples

#### Reading and Writing Files
```fg
// Write to file
write_file("data.txt", "Hello from Foolang!");

// Read from file
ty content = read_file("data.txt");
hurle("File content:", content, "\n");

// Append to file
append_file("data.txt", "\nNew line added");
```

#### File Existence Check
```fg
if (file_exists("config.txt")) {
    ty config = read_file("config.txt");
    hurle("Config loaded:", config, "\n");
} else {
    hurle("Config file not found\n");
}
```

---

### Type Conversion Examples

#### String and Number Conversion
```fg
ty num_str = "42";
ty number = to_int(num_str);
hurle(number + 8, "\n"); // 50

ty float_num = 3.14;
ty str_num = to_string(float_num);
hurle("String:", str_num, "\n"); // String: 3.14
```

#### Character Functions
```fg
ty char_a = 'A';
ty code = ord(char_a);
hurle("ASCII code of A:", code, "\n"); // ASCII code of A: 65

ty char_b = chr(66);
hurle("Character for code 66:", char_b, "\n"); // Character for code 66: B
```

---

### Bit Manipulation Examples

#### Binary Operations
```fg
ty flags = 0b1010; // 10
ty mask = 0b1100;  // 12

hurle("Original:", to_bin(flags), "\n");
hurle("AND:", to_bin(flags & mask), "\n");
hurle("OR:", to_bin(flags | mask), "\n");
hurle("XOR:", to_bin(flags ^ mask), "\n");
```

#### Type Casting
```fg
ty large_num = 1000;
hurle("Original:", large_num, "\n");
hurle("as i8:", to_i8(large_num), "\n"); // 232 (1000 % 256)
hurle("as i16:", to_i16(large_num), "\n"); // 1000
```

---

### Advanced Examples

#### Calculator Function
```fg
function calculator(operation, a, b) {
    if (operation == "+") {
        omeo a + b;
    } else if (operation == "-") {
        omeo a - b;
    } else if (operation == "*") {
        omeo a * b;
    } else if (operation == "/") {
        if (b == 0) {
            hurle("Error: Division by zero\n");
            omeo 0;
        }
        omeo a / b;
    } else {
        hurle("Unknown operation:", operation, "\n");
        omeo 0;
    }
}

hurle(calculator("+", 10, 5), "\n"); // 15
hurle(calculator("*", 4, 3), "\n");  // 12
hurle(calculator("/", 15, 3), "\n"); // 5
```

#### Array Processing
```fg
function find_max(arr) {
    if (len(arr) == 0) {
        omeo NULL;
    }
    
    ty max_val = arr[0];
    for (ty i = 1; i < len(arr); i++;) {
        if (arr[i] > max_val) {
            max_val = arr[i];
        }
    }
    omeo max_val;
}

ty numbers = [3, 7, 2, 9, 1, 5];
ty max_num = find_max(numbers);
hurle("Maximum value:", max_num, "\n"); // Maximum value: 9
```

#### Complex Data Structure
```fg
struct Book {
    title,
    author,
    year
}

ty library = [
    new Book { title: "1984", author: "Orwell", year: 1949 },
    new Book { title: "Brave New World", author: "Huxley", year: 1932 }
];

for (ty i = 0; i < len(library); i++;) {
    ty book = library[i];
    hurle(book.title, "by", book.author, "(", book.year, ")\n");
}
```

---
## 16. How to Run

 **Create a program**: Write your code in a `.fg` file
 **Run the program**: Use the `fg` command

### Running foolang Programs
```bash
fg programme.fg

fg /path/to/programme.fg
```

### File Extension
Foolang files use the `.fg` extension:
```bash
echo 'hurle("Hello, Foolang!");' > hello.fg

fg hello.fg
```


### Quick Start
```bash
echo 'hurle("Hello, Foolang!");' > hello.fg

fg hello.fg

cat > test.fg << 'EOF'
ty x = 10;
ty y = 20;
hurle("Sum:", x + y);
EOF

fg test.fg
```

---

## 17. Contributing
This is a personal programming language project. For questions, suggestions, or support, please contact me directly.

---

## 18. Language Reference (Summary Table)
| Feature         | Syntax/Example                | Notes |
|-----------------|------------------------------|-------|
| Variable        | `ty x = 1;`                 | Mutable, block-scoped |
| Constant        | `const PI = 3.14;`           | Immutable, global |
| Function        | `function f(a) { ... }`      | User-defined, recursive |
| Struct          | `struct S { x, y }`          | Custom type, named fields |
| Enum            | `enum E { A, B = 2 }`        | Tagged union, optional values |
| Array           | `[1,2,3]`                    | Dynamic, heterogeneous |
| Import          | `grab "file.fg";`            | Module system |
| Print           | `hurle(x);`                  | Native I/O |
| String          | `len(s)`, `substring(s,0,5)` | String manipulation |
| File I/O        | `read_file(f)`, `write_file(f,c)` | File operations |
| Type Conversion | `to_string(x)`, `to_int(s)`  | Type coercion |
| Bit Operations  | `to_bin(x)`, `to_hex(x)`     | Bit manipulation |
| Error Handling  | Runtime errors                | File/line/column context |

---

# End of Reference

