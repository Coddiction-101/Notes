# C Programming — College Exam Q&A Book

> **Purpose:** High-yield notes for typical introductory college C programming exams. Focuses on concepts often asked in theory papers, practicals, and viva. Your university's exact syllabus/past papers should take priority.
>
> **How to study:** Read the **Answer**, understand the **Example**, memorize the **Easy recall**, then attempt the **Exam practice** without looking.

## Priority map

| Priority | Topics | Why it matters |
|---|---|---|
| **Must know** | Program structure; variables/data types; operators; input/output; decisions; loops; arrays; strings; functions; pointers | Appears in both theory and coding questions |
| **Very important** | Recursion; structures/unions; storage classes/scope; dynamic memory; file handling | Frequent longer answers and practical programs |
| **Quick revision** | Preprocessor; type conversion; `break`/`continue`; common errors | Short-answer and viva questions |

---

# UNIT 1 — C Fundamentals

## 1. What is C programming language? What are its features?

**Answer:** C is a compiled, general-purpose, procedural programming language created by Dennis Ritchie at Bell Labs in the early 1970s. A C program is typically written in source code, compiled into machine code, and executed.

**Important features:**
- **Procedural:** organizes logic into functions.
- **Compiled:** source code is translated before execution.
- **Portable:** standard-compliant code can be compiled on different systems, with platform-specific considerations.
- **Efficient:** allows low-level operations and memory access through pointers.
- **Rich operators and standard library:** supports arithmetic, control flow, input/output, strings and more.

**Example:**
```c
#include <stdio.h>

int main(void) {
    printf("Hello, C!\n");
    return 0;
}
```

**Easy recall:** C = **Functions + Control Flow + Memory Access**.

**Exam practice:** Define C and write any four features.

## 2. Explain the basic structure of a C program.

**Answer:** A simple C program usually has a header inclusion, the `main` function, statements inside braces, and a return statement. Execution starts at `main` in a hosted C program.

```c
#include <stdio.h>       // Standard input/output declarations

int main(void) {         // Entry point
    int age = 20;        // Declaration + initialization
    printf("%d\n", age); // Statement
    return 0;            // Successful completion
}
```

**Parts to remember:** `#include`, `main()`, `{ }`, declarations, statements, `return 0;`.

**Easy recall:** **Header → main → declarations → statements → return**.

**Exam practice:** Draw or write the structure and explain each part.

## 3. What are variables, constants, and data types?

**Answer:** A **variable** is a named storage location whose value can change. A **constant** is a value that does not change during program execution (for example, a literal or a `const`-qualified object). A **data type** tells C what kind of value an object holds and what operations are meaningful.

| Type | Typical purpose | Example declaration | `printf` specifier |
|---|---|---|---|
| `int` | Whole numbers | `int marks = 85;` | `%d` |
| `char` | Single character | `char grade = 'A';` | `%c` |
| `float` | Decimal number | `float price = 2.5f;` | `%f`* |
| `double` | Higher-precision decimal | `double pi = 3.14159;` | `%f`* |

*For `printf`, `float` is promoted to `double`. For `scanf`, use `%f` with `float *` and `%lf` with `double *`. Exact sizes depend on implementation; do not claim `int` is always 4 bytes.*

```c
int count = 10;
const double TAX_RATE = 0.18;
count = 11;              // Allowed
// TAX_RATE = 0.20;      // Not allowed
```

**Easy recall:** Variable = can change; constant = fixed; data type = what kind of data.

**Exam practice:** Define each and give two examples.

## 4. Explain operators in C and operator precedence.

**Answer:** Operators perform computations, comparisons, assignments or logical tests.

| Kind | Operators | Example |
|---|---|---|
| Arithmetic | `+ - * / %` | `7 % 3` gives `1` |
| Relational | `< > <= >= == !=` | `a == b` |
| Logical | `&& || !` | `a > 0 && b > 0` |
| Assignment | `= += -= *= /= %=` | `x += 2` |
| Increment/decrement | `++ --` | `i++` |
| Conditional | `?:` | `a > b ? a : b` |
| Bitwise | `& | ^ ~ << >>` | `5 & 3` |

```c
int a = 7, b = 2;
printf("%d\n", a / b);      // 3: integer division
printf("%d\n", a % b);      // 1: remainder
printf("%d\n", a + b * 2);  // 11: multiplication first
```

**Important precedence (higher to lower, selected):** unary `!`/`++` → `* / %` → `+ -` → comparisons → `== !=` → `&&` → `||` → assignment. Use parentheses when unsure. **Precedence is not the same as evaluation order.**

**Easy recall:** `=` assigns; `==` compares. `&&` means AND; `||` means OR.

**Exam practice:** Differentiate `=` and `==`; explain `7/2` versus `7.0/2`.

## 5. Explain input and output functions (`printf`, `scanf`).

**Answer:** `printf()` displays formatted output; `scanf()` reads formatted input. Both are declared in `<stdio.h>`.

```c
#include <stdio.h>

int main(void) {
    int age;
    printf("Enter age: ");
    if (scanf("%d", &age) != 1) {
        printf("Invalid input\n");
        return 1;
    }
    printf("You are %d years old\n", age);
    return 0;
}
```

**Format specifiers:** `%d` (`int`), `%c` (`char`), `%f` (`printf` floating-point), `%lf` (`scanf` into `double`), `%s` (character string). `%zu` prints `size_t` (e.g., `sizeof`).

**Why `&age`?** `scanf` needs the address of `age` so it can write into it. For a character array used with `%s`, use the array name and provide a width limit.

**Easy recall:** `printf` = print; `scanf` = scan. `scanf("%d", &x)` uses `&` for ordinary scalar variables.

**Exam practice:** Write a program to input two integers and print their sum.

## 6. What is type conversion and type casting?

**Answer:** **Implicit conversion** is performed automatically by C when needed. **Explicit cast** asks C to convert a value to a specified type.

```c
int a = 5, b = 2;
double wrong = a / b;           // 2.0 (integer division happened first)
double right = (double)a / b;   // 2.5
```

**Easy recall:** Casting *before* division changes the arithmetic; storing into `double` afterward does not.

**Exam practice:** Explain implicit versus explicit conversion with examples.

---

# UNIT 2 — Decision Making & Loops

## 7. Explain `if`, `if-else`, `else-if`, and `switch`.

**Answer:** Decision statements select which code runs according to a condition.

```c
int marks = 72;
if (marks >= 75) {
    printf("Distinction\n");
} else if (marks >= 40) {
    printf("Pass\n");
} else {
    printf("Fail\n");
}
```

`switch` chooses between constant integral case labels:

```c
int choice = 2;
switch (choice) {
    case 1: printf("Add\n"); break;
    case 2: printf("Edit\n"); break;
    default: printf("Invalid\n");
}
```

**Key difference:** `if` handles ranges and complex Boolean conditions; `switch` checks equality against case labels. Missing `break` can cause fall-through to the next case.

**Easy recall:** **Ranges → if; fixed menu options → switch.**

**Exam practice:** Write a grade calculator and a menu-driven calculator.

## 8. Explain `for`, `while`, and `do-while` loops.

**Answer:** Loops repeat code as long as their condition permits.

```c
// for: convenient when the count is known
for (int i = 1; i <= 3; i++) printf("%d ", i);

// while: check condition before each iteration
int j = 1;
while (j <= 3) { printf("%d ", j); j++; }

// do-while: executes at least once
int k = 1;
do { printf("%d ", k); k++; } while (k <= 3);
```

| Loop | Condition checked | Minimum executions |
|---|---|---|
| `for` | Before body | 0 |
| `while` | Before body | 0 |
| `do-while` | After body | 1 |

**Easy recall:** `for` = counted repeat; `while` = repeat while true; `do-while` = do first, check later.

**Exam practice:** Print 1–100, sum 1–N, and multiplication table of N.

## 9. What are `break` and `continue`?

**Answer:** `break` exits the nearest enclosing loop or `switch`; `continue` skips the rest of the current loop iteration and proceeds to the next iteration.

```c
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    if (i == 5) break;
    printf("%d ", i);         // Output: 1 2 4
}
```

**Easy recall:** `break` = stop; `continue` = skip this round.

**Exam practice:** Predict outputs of loops that use `break` and `continue`.

## 10. Must-practice number programs

**Answer:** These are not separate theory chapters, but they are common practical and written-program questions.

**A. Factorial of a non-negative integer:**
```c
int n = 5;
unsigned long long fact = 1;
for (int i = 2; i <= n; i++) fact *= (unsigned)i;
printf("%llu\n", fact);  // 120
```
> For large `n`, factorial overflows even `unsigned long long`.

**B. Prime check:**
```c
int n = 29, prime = (n >= 2);
for (int i = 2; i <= n / i; i++) {
    if (n % i == 0) { prime = 0; break; }
}
printf("%s\n", prime ? "Prime" : "Not prime");
```

**C. Fibonacci sequence:**
```c
int a = 0, b = 1;
for (int i = 0; i < 7; i++) {
    printf("%d ", a);        // 0 1 1 2 3 5 8
    int next = a + b;
    a = b;
    b = next;
}
```

**Other high-yield programs to write yourself:** reverse digits; numeric palindrome; sum of digits; Armstrong number (often defined for 3-digit numbers as sum of cubes); greatest of three; leap year; multiplication table; simple star pattern.

**Easy recall:** Check boundary cases: `0`, `1`, negatives, and overflow.

---

# UNIT 3 — Arrays & Strings

## 11. What is an array? Explain one-dimensional and two-dimensional arrays.

**Answer:** An array stores multiple elements of the **same type** in contiguous memory. Indexing starts at **0**.

```c
int marks[5] = {75, 80, 68, 90, 87};
int sum = 0;
for (int i = 0; i < 5; i++) sum += marks[i];
printf("Sum = %d\n", sum); // 400
```

A 2D array is commonly used for matrices:
```c
int matrix[2][2] = {{1, 2}, {3, 4}};
printf("%d\n", matrix[1][0]); // 3
```

**Remember:** `marks[5]` is **out of bounds** here; valid indexes are `0` to `4`. C does not automatically check array bounds.

**Easy recall:** 1D = list; 2D = rows and columns.

**Exam practice:** Find largest element, array sum/average, linear search, and matrix addition.

## 12. What is a string in C? Explain common string functions.

**Answer:** A C string is a sequence of characters ending with the null character `\0`. It is commonly stored in a `char` array. String functions are declared in `<string.h>`.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char name[20] = "Hello";
    printf("%zu\n", strlen(name));    // 5 (not counting '\0')
    printf("%d\n", strcmp(name, "Hello")); // 0 means equal
    return 0;
}
```

| Function | Purpose | Important point |
|---|---|---|
| `strlen(s)` | Length | Excludes final `\0` |
| `strcmp(a,b)` | Compare strings | `0` means equal; not `1` |
| `strcpy(dest,src)` | Copy | Destination must have enough space |
| `strcat(dest,src)` | Append | Destination must have enough space |

**Safe word input example:** `scanf("%19s", name);` with `char name[20]` to reserve room for `\0`. For a full line containing spaces, prefer `fgets(name, sizeof name, stdin)`.

**Easy recall:** **String = char array + `\0`**. `==` is not a string-content comparison.

**Exam practice:** Reverse a string, check palindrome, count vowels, compare two strings.

---

# UNIT 4 — Functions & Recursion

## 13. What is a function? Explain declaration, definition, call, and arguments.

**Answer:** A function is a reusable block of code performing a task. A **declaration/prototype** states its signature, a **definition** supplies its body, and a **call** executes it.

```c
#include <stdio.h>

int add(int a, int b);           // Function prototype

int main(void) {
    int result = add(4, 6);      // Function call
    printf("%d\n", result);    // 10
    return 0;
}

int add(int a, int b) {          // Function definition
    return a + b;
}
```

**Important point:** C passes function arguments **by value**. To change a caller's variable, pass its address using a pointer.

**Easy recall:** **Declare → Call → Define** (definition may also appear before call).

**Exam practice:** Write functions for sum, maximum of two, and factorial.

## 14. What is recursion? Explain recursion versus iteration.

**Answer:** Recursion occurs when a function calls itself. Every correct recursive solution needs a **base case** to stop and a step that moves toward that base case.

```c
int factorial(int n) {
    if (n <= 1) return 1;        // Base case (use n >= 0)
    return n * factorial(n - 1); // Recursive case
}
```

For `factorial(4)`: `4 × 3 × 2 × 1 = 24`.

| Recursion | Iteration |
|---|---|
| Function calls itself | Uses loops |
| Needs a base case | Needs a loop termination condition |
| Uses call-stack frames | Often uses less stack space |

**Easy recall:** **Base case + smaller problem**. Very deep recursion may overflow the call stack.

**Exam practice:** Trace `factorial(4)` and write recursive sum of first N positive numbers.

---

# UNIT 5 — Pointers & Memory

## 15. What is a pointer? Explain `&` and `*`.

**Answer:** A pointer is a variable that stores the memory address of another object. The `&` operator obtains an address; unary `*` dereferences a pointer to access the pointed-to value.

```c
int x = 10;
int *p = &x;
printf("%d\n", *p);  // 10
*p = 25;
printf("%d\n", x);   // 25
```

**Crucial distinction:** `int *p` **declares** a pointer; `*p` **uses** it to read/write the value. Never dereference an uninitialized, `NULL`, or otherwise invalid pointer.

**Easy recall:** `&x` = address of x; `*p` = value at p's address.

**Exam practice:** Define pointer and show how it changes a variable's value.

## 16. What is the relationship between arrays and pointers?

**Answer:** In many expressions, an array name converts to a pointer to its first element. `arr[i]` and `*(arr + i)` refer to the same array element, when the index is valid. **An array is not itself a pointer variable.**

```c
int arr[] = {10, 20, 30};
printf("%d\n", *(arr + 1)); // 20
```

**Important:** Pointer arithmetic advances by elements, not single bytes: `p + 1` points to the next object of `p`'s pointed-to type.

**Easy recall:** `arr[i]` ↔ `*(arr + i)`.

**Exam practice:** Print array elements using pointer arithmetic.

## 17. Explain call by value and changing values using pointers.

**Answer:** C **always** passes arguments by value, including when the values being passed are addresses. A function can indirectly modify the caller's variables if it receives their addresses.

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main(void) {
    int x = 3, y = 8;
    swap(&x, &y);
    printf("%d %d\n", x, y); // 8 3
    return 0;
}
```

**Easy recall:** Pass numbers to *use* values; pass addresses to *modify* caller objects.

**Exam practice:** Write a swap program using pointers.

## 18. Explain dynamic memory allocation (`malloc`, `calloc`, `realloc`, `free`).

**Answer:** Dynamic allocation requests memory at runtime; the functions are declared in `<stdlib.h>`.

| Function | Purpose |
|---|---|
| `malloc(n)` | Allocate `n` bytes; contents uninitialized |
| `calloc(count,size)` | Allocate and zero-initialize the requested bytes |
| `realloc(ptr,n)` | Resize allocation; may move it |
| `free(ptr)` | Release previously allocated memory |

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n = 3;
    int *a = malloc((size_t)n * sizeof *a);
    if (a == NULL) return 1;
    for (int i = 0; i < n; i++) a[i] = i + 1;
    printf("%d\n", a[2]);  // 3
    free(a);
    a = NULL;
    return 0;
}
```

**Important:** Check allocation failures, avoid out-of-bounds access, free memory once, and do not use a pointer after its allocation has been freed.

**Easy recall:** **Allocate → check → use → free**.

**Exam practice:** Allocate an array at runtime and compute its sum.

---

# UNIT 6 — Structures, Storage & Files

## 19. What are structures and unions? Differentiate them.

**Answer:** A `struct` groups fields of possibly different types; its members have their own storage. A `union` contains members that share overlapping storage, so normally only the currently stored member's value should be used.

```c
struct Student {
    int roll;
    char grade;
};

struct Student s = {101, 'A'};
printf("%d %c\n", s.roll, s.grade);
```

| Structure | Union |
|---|---|
| Members have separate storage | Members overlap in storage |
| Can hold all members' values simultaneously | One member's stored representation overlaps the others |
| Size includes member layout and padding | Size accommodates its largest member (plus alignment) |

**Easy recall:** **Struct = together; union = shared memory.**

**Exam practice:** Store and display details of 3 students using an array of structures.

## 20. Explain local/global variables, scope, lifetime, and storage classes.

**Answer:** **Scope** describes where a name is visible; **storage duration** describes how long its object exists. A local automatic variable is normally created on block entry, while a file-scope variable has static storage duration.

```c
#include <stdio.h>

void counter(void) {
    static int calls = 0; // Initialized once, persists between calls
    calls++;
    printf("%d ", calls);
}

int main(void) {
    counter(); counter(); counter(); // 1 2 3
    return 0;
}
```

| Keyword | Key idea |
|---|---|
| `auto` | Default automatic storage for ordinary block-local objects |
| `register` | Hint for fast access (historically relevant); cannot apply `&` to such a declared object |
| `static` | Static storage duration for objects; at file scope can also give internal linkage |
| `extern` | Declares a name defined elsewhere, commonly a global object |

**Easy recall:** **Scope = where visible; lifetime = how long it exists.**

**Exam practice:** Differentiate local and global variables; explain `static` with output.

## 21. Explain file handling in C.

**Answer:** File handling lets a program store/read data using streams. Common library functions are `fopen`, `fprintf`, `fscanf`, `fgets`, `fputs`, `fclose`.

**Common modes:** `"r"` read existing file; `"w"` write (create or truncate); `"a"` append; `"r+"` read/write existing; `"w+"` read/write (truncate); `"a+"` read/append.

```c
#include <stdio.h>

int main(void) {
    FILE *fp = fopen("notes.txt", "w");
    if (fp == NULL) {
        perror("fopen");
        return 1;
    }
    fprintf(fp, "C programming\n");
    if (fclose(fp) != 0) return 1;
    return 0;
}
```

**Important:** Always check whether `fopen` succeeded. `"w"` overwrites existing contents. `fgetc()` returns an `int` so it can also represent `EOF`.

**Easy recall:** **Open → check → read/write → close**.

**Exam practice:** Write data to a file; read and display text from a file.

## 22. What are preprocessor directives, macros, and header files?

**Answer:** The preprocessor handles directives before compilation. `#include` brings in declarations from a header; `#define` defines a macro.

```c
#include <stdio.h>
#define SQUARE(x) ((x) * (x))

int main(void) {
    printf("%d\n", SQUARE(4)); // 16
    return 0;
}
```

**Important:** Avoid passing expressions with side effects such as `SQUARE(i++)`, since the macro may evaluate them more than once. Header files commonly declare functions, types, and macros.

**Easy recall:** `#include` = use header; `#define` = text-like macro substitution.

**Exam practice:** Compare a macro and a function; explain `#include <stdio.h>`.

---

# High-Yield Differences — 2-Mark / Viva Revision

| Question | Short answer |
|---|---|
| Compiler vs interpreter? | Compiler translates a program before execution; an interpreter generally executes via an interpretation process. C is usually compiled. |
| `=` vs `==`? | Assignment vs equality comparison. |
| `while` vs `do-while`? | Condition before body (0+ runs) vs after body (1+ runs). |
| `break` vs `continue`? | Exit loop/switch vs skip to next loop iteration. |
| Array vs structure? | Same-type indexed elements vs named mixed-type members. |
| `struct` vs `union`? | Distinct member storage vs shared/overlapping storage. |
| `strlen` vs `sizeof`? | Length before `\0` vs object/type size in bytes (when `sizeof` is applied to an actual array, not a pointer). |
| `malloc` vs `calloc`? | Uninitialized allocation vs zero-initialized bytes. |
| `NULL` vs `\0`? | Null pointer constant/macro vs zero character marking end of a C string. |
| Syntax vs logical error? | Invalid C grammar/constraints vs valid program producing wrong result. |
| Compile-time vs runtime error? | Detected during translation vs arising while executing. |
| Actual vs formal parameters? | Expressions passed at call vs parameter names declared in definition. |

---

# Most Important Programs — Practical Exam Checklist

Tick each when you can code it **without copying**:

- [ ] Input two numbers; sum, average, swap
- [ ] Odd/even; positive/negative/zero; largest of three
- [ ] Leap year; simple calculator using `switch`
- [ ] Multiplication table; sum of first N natural numbers
- [ ] Factorial using loop and function
- [ ] Prime number test
- [ ] Fibonacci series
- [ ] Reverse digits; numeric palindrome; sum of digits
- [ ] 3-digit Armstrong number; simple star/number pattern
- [ ] Array sum, maximum, minimum, linear search
- [ ] Bubble sort (ascending order)
- [ ] Matrix addition and transpose
- [ ] String length without `strlen`; reverse; palindrome; vowel count
- [ ] Functions with arguments/return value; recursive factorial
- [ ] Swap two numbers using pointers
- [ ] Student record with structure
- [ ] Write and read a text file

---

# Five Extra Solved Programs That Often Appear

## A. Bubble sort — ascending order
```c
#include <stdio.h>

int main(void) {
    int a[] = {5, 2, 4, 1, 3};
    int n = (int)(sizeof a / sizeof a[0]);
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (a[j] > a[j + 1]) {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }
    for (int i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
**Output:** `1 2 3 4 5`. **Remember:** Each pass moves a large element toward the end.

## B. Reverse a number
```c
#include <stdio.h>

int main(void) {
    int n = 1234, rev = 0;
    while (n > 0) {
        rev = rev * 10 + n % 10;
        n /= 10;
    }
    printf("%d\n", rev); // 4321
    return 0;
}
```
**Remember:** Last digit = `n % 10`; remove last digit = `n / 10` for non-negative integers.

## C. Linear search
```c
#include <stdio.h>

int main(void) {
    int a[] = {8, 4, 9, 2}, target = 9;
    int n = (int)(sizeof a / sizeof a[0]);
    int index = -1;
    for (int i = 0; i < n; i++) {
        if (a[i] == target) { index = i; break; }
    }
    printf("Index: %d\n", index); // 2
    return 0;
}
```
**Remember:** Search elements one by one; `-1` here means not found.

## D. Matrix addition
```c
#include <stdio.h>

int main(void) {
    int a[2][2] = {{1, 2}, {3, 4}};
    int b[2][2] = {{5, 6}, {7, 8}};
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++)
            printf("%d ", a[i][j] + b[i][j]);
        printf("\n");
    }
    return 0;
}
```
**Output:** First row `6 8`, second row `10 12`.

## E. String palindrome
```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char s[] = "madam";
    size_t left = 0, right = strlen(s);
    int palindrome = 1;
    while (left < right) {
        if (s[left] != s[right - 1]) {
            palindrome = 0;
            break;
        }
        left++;
        right--;
    }
    printf("%s\n", palindrome ? "Palindrome" : "Not palindrome");
    return 0;
}
```
**Remember:** Compare opposite ends while moving toward the center.

---

# Common Mistakes That Lose Marks

1. Writing `if (x = 5)` instead of `if (x == 5)` when testing equality.
2. Forgetting `&` in `scanf("%d", &x)` for an integer.
3. Using an array index outside `0` to `n-1`.
4. Forgetting to update a loop variable, creating an infinite loop.
5. Forgetting the null terminator or space for it in strings.
6. Comparing strings using `==` instead of `strcmp`.
7. Dividing two integers when a decimal answer is needed.
8. Dereferencing an uninitialized pointer.
9. Forgetting to check `fopen`/`malloc` results.
10. Forgetting that `"w"` mode truncates an existing file.
11. Assuming `sizeof(int)` is always 4 bytes.
12. Forgetting a base case in recursion.

---

# Last-Minute Revision Plan

**If you have 1 day:**
- **Session 1:** Questions 1–9 — fundamentals, input/output, conditions, loops.
- **Session 2:** Questions 10–14 — number programs, arrays, strings, functions.
- **Session 3:** Questions 15–22 — pointers, structures, files, memory, remaining theory.
- **Session 4:** Write the checklist programs you cannot solve, then revise the differences table.

**If you have only 2 hours:**
1. Revise key definitions and differences (25 minutes).
2. Handwrite any five: prime, factorial, array max, string reverse, pointer swap (55 minutes).
3. Revise functions, recursion, structures, and file handling (25 minutes).
4. Review mistakes and outputs (15 minutes).

## Final memory map

**Input → Decision → Repetition → Collections → Reuse → Addresses → Records → Files**

`scanf/printf` → `if/switch` → `for/while` → `array/string` → `function/recursion` → `pointer/malloc` → `struct/union` → `fopen/fclose`

> **Exam rule:** For a theory answer, write **definition → key points → small code example → output/use**. For a program, write **header → main → variables → logic → output → return**. Compile and test code rather than memorizing syntax blindly.
