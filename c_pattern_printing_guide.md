# Pattern Printing in the C Programming Language

A complete, easy-to-follow guide to the pattern programs that matter. Every line of code is explained in full words, and every pattern follows the same organized structure so you can find things fast.

---

## Table of Contents

1. [The Core Idea Behind Every Pattern](#part-1-the-core-idea-behind-every-pattern)
2. [The Reusable Program Template](#part-2-the-reusable-program-template-explained-once-in-depth)
3. [Group A: Square and Rectangle Patterns](#group-a-square-patterns)
4. [Group B: Triangle Patterns with Stars](#group-b-triangle-patterns-with-stars)
5. [Group C: Triangle Patterns with Numbers and Letters](#group-c-triangle-patterns-with-numbers-and-letters)
6. [Group D: Pyramid Patterns](#group-d-pyramid-patterns)
7. [Group E: Diamond and Butterfly Patterns](#group-e-diamond-and-butterfly-patterns)
8. [Group F: Special Famous Patterns](#group-f-special-famous-patterns)
9. [The Master Cheat Sheet](#the-master-cheat-sheet)
10. [Common Mistakes](#common-mistakes-and-how-to-avoid-them)
11. [Practice Challenges](#practice-challenges)

---

# Part 1: The Core Idea Behind Every Pattern

Every pattern you will ever print is a **grid of rows and columns**. A screen prints text from top to bottom, and inside each line from left to right. So to print a pattern you must answer only **three questions**:

| Question | What it decides | How it appears in code |
|---|---|---|
| **How many rows are there?** | The outer loop | One loop that repeats once per line |
| **In each row, how many things are printed?** | The inner loop | A loop inside the outer loop that repeats once per character |
| **What exactly is printed in each position?** | The print statement | A call to the print function inside the inner loop |

## The Golden Rule

> **The outer loop controls the rows. The inner loop controls what appears inside one row. After the inner loop finishes, move to the next line.**

Think of it like writing in a notebook: the outer loop is "go to the next line of the page", and the inner loop is "write each letter on that line".

## The Four-Step Method to Solve Any Pattern

1. **Count the rows.** Look at the pattern and count how many lines it has.
2. **For one row at a time, count the spaces and count the symbols.** Write them in a small table.
3. **Find the relationship.** Ask: "How does the count change when the row number changes?" The answer is a small formula using the row number.
4. **Turn each count into a loop.** One loop for spaces, one loop for symbols. Put them inside the row loop.

### Worked example of the method (right triangle with 4 rows)

```
*
* *
* * *
* * * *
```

| Row number | Symbols printed |
|---|---|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |

Relationship: **the number of symbols equals the row number.** So the inner loop runs from 1 up to the row number. That is the entire pattern.

---

# Part 2: The Reusable Program Template (Explained Once, In Depth)

Almost every program in this guide uses this skeleton. Learn it once here, and later sections will only explain what is new.

```c
#include <stdio.h>

int main(void)
{
    int numberOfRows;

    printf("Enter the number of rows: ");
    scanf("%d", &numberOfRows);

    for (int row = 1; row <= numberOfRows; row++)
    {
        for (int column = 1; column <= row; column++)
        {
            printf("* ");
        }
        printf("\n");
    }

    return 0;
}
```

## Line-by-line explanation

**`#include <stdio.h>`**
The hash symbol begins a *preprocessor directive*, which is an instruction that is handled before the real compilation begins. The word `include` means "copy the contents of another file into this file". The name `stdio.h` stands for the *standard input and output header file*. It contains the descriptions of the functions we use to show text on the screen (`printf`) and to read values typed by the person using the program (`scanf`). Without this line the compiler would not know what `printf` and `scanf` are.

**`int main(void)`**
Every C program begins running from a function named `main`. The word `int` means *integer*: it says this function gives back a whole number when it finishes. The word `void` inside the parentheses means this function accepts no input values.

**`{` and `}` (curly braces)**
Curly braces mark the beginning and the end of a block of code. Everything between the opening brace after `main` and the matching closing brace belongs to the `main` function.

**`int numberOfRows;`**
This creates a *variable*, which is a named storage box in the computer memory. The word `int` means the box holds a whole number. The name `numberOfRows` is chosen by us; a descriptive name makes the program easy to read. The semicolon ends the statement.

**`printf("Enter the number of rows: ");`**
The function `printf` shows text on the screen. Whatever is inside the double quotation marks is displayed exactly as written. This line is simply a message asking the person for a value.

**`scanf("%d", &numberOfRows);`**
The function `scanf` waits for the person to type something and then stores it. The symbol `%d` is a *format specifier* meaning "expect a decimal whole number". The ampersand `&` means "the memory address of". So the whole line means: "read a whole number and place it inside the box named `numberOfRows`". The ampersand is required because `scanf` must know *where* in memory to put the value.

**`for (int row = 1; row <= numberOfRows; row++)`**
This is the **outer loop**. A `for` loop has three parts separated by semicolons:
1. `int row = 1` is the *initialization*: it creates a variable named `row` and sets it to 1. This runs once, before the loop starts.
2. `row <= numberOfRows` is the *condition*: before every repetition, the computer checks this. If it is true, the loop body runs. If it is false, the loop stops. The symbol `<=` means "less than or equal to".
3. `row++` is the *update*: after each repetition, the value of `row` increases by 1. The symbol `++` means "add one".

So this loop runs once for each row: row 1, row 2, and so on until `numberOfRows`.

**`for (int column = 1; column <= row; column++)`**
This is the **inner loop**. It is written inside the outer loop, so it starts fresh on every row. It creates a variable named `column` that begins at 1 and counts up to the current value of `row`. In row 3 it runs 3 times, so three symbols are printed.

**`printf("* ");`**
This prints one star followed by one space. The space keeps the stars from touching, which makes the pattern look neat. Because there is no newline here, the next symbol appears on the same line.

**`printf("\n");`**
The two characters `\n` together mean *newline*. This moves the cursor to the beginning of the next line. It sits **after** the inner loop and **inside** the outer loop, so it runs exactly once per row.

**`return 0;`**
This ends the `main` function and tells the operating system that the program finished successfully. The number zero is the traditional signal for "no error".

## Where each part belongs (memorize this shape)

```
for each row                      <- outer loop: controls the lines
{
    (print spaces, if needed)     <- inner loop 1: empty space on the left
    (print symbols)               <- inner loop 2: stars, numbers or letters
    move to the next line         <- one newline per row
}
```

> **Note on the rest of this guide:** To save space, each program below shows only the part **inside `main`** after the number of rows is read. Wrap it with the template above (the include line, the `main` function, the variable, the `scanf` call, and the `return`) to make a full program.

---

# Group A: Square Patterns

## Pattern 1: Solid Square

**Output (rows = 4):**
```
* * * *
* * * *
* * * *
* * * *
```

**Logic:** Every row has the same number of stars as the total number of rows.

| Row | Stars |
|---|---|
| 1 | 4 |
| 2 | 4 |
| 3 | 4 |
| 4 | 4 |

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= numberOfRows; column++)
    {
        printf("* ");
    }
    printf("\n");
}
```

**Explanation:**
- The outer loop repeats `numberOfRows` times, producing that many lines.
- The inner loop's condition is `column <= numberOfRows`, not `column <= row`. Because the limit never changes, each line holds the same count of stars. This is the single difference between a square and a triangle.
- `printf("* ")` places one star and one space.
- `printf("\n")` ends the line after all the stars of that row are printed.

---

## Pattern 2: Hollow Square

**Output (rows = 5):**
```
* * * * *
*       *
*       *
*       *
* * * * *
```

**Logic:** A star is printed only on the **border**: the first row, the last row, the first column, or the last column. Everywhere else a blank space is printed.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= numberOfRows; column++)
    {
        if (row == 1 || row == numberOfRows || column == 1 || column == numberOfRows)
        {
            printf("* ");
        }
        else
        {
            printf("  ");
        }
    }
    printf("\n");
}
```

**Explanation:**
- The two loops are the same as the solid square. The new idea is the decision inside the inner loop.
- The `if` statement asks a question. The double vertical bar `||` means **or**. The question is: "Is this the first row, or the last row, or the first column, or the last column?" If any one of these is true, the position is on the border, so a star is printed.
- The double equals sign `==` means "is equal to". (A single equals sign `=` would store a value instead of comparing, which is a very common mistake.)
- The `else` part runs when the position is **not** on the border. It prints **two spaces**, which has the same width as `"* "`. Using two spaces is important: it keeps all the columns aligned.

---

# Group B: Triangle Patterns with Stars

## Pattern 3: Right Triangle

**Output (rows = 5):**
```
*
* *
* * *
* * * *
* * * * *
```

**Logic:** The count of stars equals the row number.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        printf("* ");
    }
    printf("\n");
}
```

**Explanation:**
- The inner loop runs from 1 up to the current `row`. In row 1 it runs once, in row 2 twice, and so on. This growth is what shapes the triangle.
- Everything else follows the template explained in Part 2.

---

## Pattern 4: Inverted Right Triangle

**Output (rows = 5):**
```
* * * * *
* * * *
* * *
* *
*
```

**Logic:** The first row has the most stars and each following row has one fewer.

| Row | Stars | Formula |
|---|---|---|
| 1 | 5 | numberOfRows − row + 1 |
| 2 | 4 | |
| 3 | 3 | |

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= numberOfRows - row + 1; column++)
    {
        printf("* ");
    }
    printf("\n");
}
```

**Explanation:**
- The inner loop limit is `numberOfRows - row + 1`. When `row` is 1, the limit is the full `numberOfRows`. As `row` grows, the limit shrinks by one each time.
- *Alternative idea:* you could also run the outer loop backwards (from `numberOfRows` down to 1) and keep the inner limit as `row`. Both ways give the same picture.

---

## Pattern 5: Right-Aligned Triangle (Mirror Triangle)

**Output (rows = 5):**
```
        *
      * *
    * * *
  * * * *
* * * * *
```

**Logic:** Each row has two parts: empty space on the left, then stars. The spaces decrease while the stars increase.

| Row | Spaces (each is two characters wide) | Stars |
|---|---|---|
| 1 | 4 | 1 |
| 2 | 3 | 2 |
| 3 | 2 | 3 |
| 4 | 1 | 4 |
| 5 | 0 | 5 |

Formula for spaces: `numberOfRows - row`. Formula for stars: `row`.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf("  ");
    }
    for (int star = 1; star <= row; star++)
    {
        printf("* ");
    }
    printf("\n");
}
```

**Explanation:**
- **First inner loop (named `space`)** prints the blank area. It repeats `numberOfRows - row` times, and each repetition prints two blank characters so it matches the width of `"* "`.
- **Second inner loop (named `star`)** prints the stars. It repeats `row` times.
- The order matters: spaces are printed **first** (the left side), then stars. A newline finishes the row.
- This "spaces first, then symbols" structure is the foundation for **all pyramids and diamonds**, so make sure you understand it fully.

---

# Group C: Triangle Patterns with Numbers and Letters

## Pattern 6: Number Triangle (Counting Up from One in Each Row)

**Output (rows = 5):**
```
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
```

**Logic:** Each row prints the column numbers from 1 up to the row number. So we print the **column variable itself**.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        printf("%d ", column);
    }
    printf("\n");
}
```

**Explanation:**
- The only change from the star triangle is the print statement.
- `%d` is the placeholder for a whole number. The value after the comma (`column`) replaces the placeholder when printing.
- A space after `%d` separates the numbers.

---

## Pattern 7: Repeated Row Number Triangle

**Output (rows = 5):**
```
1
2 2
3 3 3
4 4 4 4
5 5 5 5 5
```

**Logic:** Every number in a row equals the row number.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        printf("%d ", row);
    }
    printf("\n");
}
```

**Explanation:**
- The inner loop still runs `row` times, giving the triangle shape.
- We print `row` instead of `column`. That single change repeats the row number across the line.
- **Lesson:** to control the shape, change the loop limits. To control the content, change what is printed.

---

## Pattern 8: Inverted Number Triangle

**Output (rows = 5):**
```
1 2 3 4 5
1 2 3 4
1 2 3
1 2
1
```

**Code:**
```c
for (int row = numberOfRows; row >= 1; row--)
{
    for (int column = 1; column <= row; column++)
    {
        printf("%d ", column);
    }
    printf("\n");
}
```

**Explanation:**
- The outer loop here **counts downward**. It starts at `numberOfRows`, continues while `row >= 1` (greater than or equal to one), and uses `row--` which means "subtract one" after each repetition.
- The inner loop is the same as in Pattern 6: it counts from 1 up to `row`. Since `row` now shrinks, each line is shorter than the one before.

---

## Pattern 9: Floyd's Triangle (Continuous Numbers)

**Output (rows = 5):**
```
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

**Logic:** Numbers continue in order and never restart. We need a separate variable that remembers the next number to print.

**Code:**
```c
int nextNumber = 1;

for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        printf("%d ", nextNumber);
        nextNumber++;
    }
    printf("\n");
}
```

**Explanation:**
- `int nextNumber = 1;` creates a variable **outside both loops**, which is essential. If it were created inside the loops, it would reset to 1 again and again.
- Inside the inner loop we print the current value, then `nextNumber++` increases it by one so the next print shows the following number.
- Because the variable survives from one row to the next, the counting never restarts.

---

## Pattern 10: Alphabet Triangle

**Output (rows = 5):**
```
A
A B
A B C
A B C D
A B C D E
```

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        printf("%c ", 'A' + column - 1);
    }
    printf("\n");
}
```

**Explanation:**
- Inside the computer, every character is stored as a number. The letters of the alphabet are stored in order: the code of `'B'` is exactly one more than the code of `'A'`, and so on.
- `'A'` (with single quotation marks) is a *character constant*. We add `column - 1` to it. When `column` is 1 we add 0 and get `A`. When `column` is 2 we add 1 and get `B`.
- `%c` is the placeholder for a **single character**. It converts the number back into its letter for display.
- *Variation:* use `'A' + row - 1` instead to print the same letter across a whole row.

---

## Pattern 11: Binary Triangle (Zeros and Ones)

**Output (rows = 5):**
```
1
1 0
1 0 1
1 0 1 0
1 0 1 0 1
```

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= row; column++)
    {
        if (column % 2 == 1)
        {
            printf("1 ");
        }
        else
        {
            printf("0 ");
        }
    }
    printf("\n");
}
```

**Explanation:**
- The percent sign `%` in this context is the **remainder operator**, which gives what is left over after division. `column % 2` is 1 for odd numbers and 0 for even numbers.
- If the column is odd, print `1`. Otherwise print `0`. This alternates along each row.
- Do not confuse this `%` (an operator in the code) with the `%` inside the quotation marks of `printf` (a placeholder marker). They are different things in different places.

---

# Group D: Pyramid Patterns

A pyramid is the right-aligned triangle idea (spaces first, then symbols) with one change: the stars grow by **two** each row so both sides look symmetrical.

## Pattern 12: Full Pyramid

**Output (rows = 5):**
```
        *
      * * *
    * * * * *
  * * * * * * *
* * * * * * * * *
```

Here a simpler and cleaner version is used with single-character spacing:

```
    *
   ***
  *****
 *******
*********
```

**Logic table (rows = 5):**

| Row | Spaces | Stars | Formula for spaces | Formula for stars |
|---|---|---|---|---|
| 1 | 4 | 1 | numberOfRows − row | 2 × row − 1 |
| 2 | 3 | 3 | | |
| 3 | 2 | 5 | | |
| 4 | 1 | 7 | | |
| 5 | 0 | 9 | | |

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * row - 1; star++)
    {
        printf("*");
    }
    printf("\n");
}
```

**Explanation:**
- **Space loop:** prints `numberOfRows - row` single blank characters. The top row gets the most spaces, which pushes its star toward the center.
- **Star loop:** prints `2 * row - 1` stars. The asterisk `*` in `2 * row` is multiplication. This produces the odd sequence 1, 3, 5, 7, 9, which makes the pyramid widen evenly on both sides.
- Here the stars are printed without a trailing space so the result looks solid. If you want the spaced look, print `"* "` and increase the space characters to two per unit.

---

## Pattern 13: Inverted Pyramid

**Output (rows = 5):**
```
*********
 *******
  *****
   ***
    *
```

**Logic table:**

| Row | Spaces | Stars | Formula for spaces | Formula for stars |
|---|---|---|---|---|
| 1 | 0 | 9 | row − 1 | 2 × (numberOfRows − row) + 1 |
| 2 | 1 | 7 | | |
| 3 | 2 | 5 | | |
| 4 | 3 | 3 | | |
| 5 | 4 | 1 | | |

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= row - 1; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * (numberOfRows - row) + 1; star++)
    {
        printf("*");
    }
    printf("\n");
}
```

**Explanation:**
- Spaces now **increase** with the row (`row - 1`), because each lower line sits farther to the right.
- Stars **decrease** by two each row. The formula `2 * (numberOfRows - row) + 1` gives 9, 7, 5, 3, 1 for five rows.
- The parentheses force the subtraction to be calculated first, before multiplying.

---

## Pattern 14: Hollow Pyramid

**Output (rows = 5):**
```
    *
   * *
  *   *
 *     *
*********
```

**Logic:** In each row, print a star only at the **first position**, the **last position**, or anywhere in the **last row**. Otherwise print a blank space.

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int column = 1; column <= 2 * row - 1; column++)
    {
        if (column == 1 || column == 2 * row - 1 || row == numberOfRows)
        {
            printf("*");
        }
        else
        {
            printf(" ");
        }
    }
    printf("\n");
}
```

**Explanation:**
- The space loop is the same as in the full pyramid.
- The second loop walks through every position of the row, from 1 to `2 * row - 1`.
- The condition checks three cases joined by **or**:
  - `column == 1`: the left edge of this row.
  - `column == 2 * row - 1`: the right edge of this row (the last position).
  - `row == numberOfRows`: the base of the pyramid, which is completely filled.
- For all other positions (the inside), a single space is printed to make the hollow area.

---

## Pattern 15: Number Pyramid (Palindrome Style)

**Output (rows = 5):**
```
    1
   121
  12321
 1234321
123454321
```

**Logic:** Each row counts **up** from 1 to the row number, and then counts **down** back to 1, skipping the peak so it is not shown twice. (Works correctly for up to 9 rows, because after 9 the numbers have two digits and break the alignment.)

**Code:**
```c
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int number = 1; number <= row; number++)
    {
        printf("%d", number);
    }
    for (int number = row - 1; number >= 1; number--)
    {
        printf("%d", number);
    }
    printf("\n");
}
```

**Explanation:**
- **Space loop:** the familiar pyramid indentation.
- **First number loop (counting up):** prints 1, 2, 3, up to and including `row`.
- **Second number loop (counting down):** starts at `row - 1` (one below the peak, so the peak is not repeated) and goes down to 1. The `number--` part subtracts one each time.
- Joined together, the two loops form a mirror-image sequence like `12321`.

---

# Group E: Diamond and Butterfly Patterns

These combine two earlier patterns: **a diamond is a pyramid on top of an inverted pyramid**.

## Pattern 16: Diamond

**Output (rows = 5 for the upper half):**
```
    *
   ***
  *****
 *******
*********
 *******
  *****
   ***
    *
```

**Logic:** Print the full pyramid with `numberOfRows` lines. Then print an inverted pyramid with `numberOfRows - 1` lines. The widest row appears only once, which is why the second half has one row fewer.

**Code:**
```c
/* Upper half: a normal pyramid */
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * row - 1; star++)
    {
        printf("*");
    }
    printf("\n");
}

/* Lower half: an inverted pyramid, one row shorter */
for (int row = numberOfRows - 1; row >= 1; row--)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * row - 1; star++)
    {
        printf("*");
    }
    printf("\n");
}
```

**Explanation:**
- **Text between `/*` and `*/`** is a *comment*. The computer ignores comments completely; they are notes for human readers.
- **Upper half** is identical to Pattern 12.
- **Lower half** reuses the **same formulas** for spaces and stars but runs the row variable **backwards**, starting at `numberOfRows - 1`. Since the formulas depend on `row`, counting down makes the shape shrink.
- Starting from `numberOfRows - 1` (not `numberOfRows`) prevents the widest row from appearing twice.
- **Big idea:** you do not need new formulas to reverse a shape. Run the same loop in the opposite direction.

---

## Pattern 17: Hollow Diamond

**Output (rows = 5 for the upper half):**
```
    *
   * *
  *   *
 *     *
*       *
 *     *
  *   *
   * *
    *
```

**Code:**
```c
/* Upper half */
for (int row = 1; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int column = 1; column <= 2 * row - 1; column++)
    {
        if (column == 1 || column == 2 * row - 1)
        {
            printf("*");
        }
        else
        {
            printf(" ");
        }
    }
    printf("\n");
}

/* Lower half */
for (int row = numberOfRows - 1; row >= 1; row--)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int column = 1; column <= 2 * row - 1; column++)
    {
        if (column == 1 || column == 2 * row - 1)
        {
            printf("*");
        }
        else
        {
            printf(" ");
        }
    }
    printf("\n");
}
```

**Explanation:**
- It is the diamond with the hollow trick from Pattern 14 applied to both halves.
- A star is printed only at the first and last position of each row. The inside prints blank spaces.
- Notice there is no `row == numberOfRows` check this time, because the middle row of a diamond is also hollow with only two stars at its edges.

---

## Pattern 18: Butterfly

**Output (rows = 4):**
```
*      *
**    **
***  ***
********
********
***  ***
**    **
*      *
```

**Logic:** Each row has three parts: left stars, middle spaces, right stars.

| Row (upper half, rows = 4) | Left stars | Middle spaces | Right stars |
|---|---|---|---|
| 1 | 1 | 6 | 1 |
| 2 | 2 | 4 | 2 |
| 3 | 3 | 2 | 3 |
| 4 | 4 | 0 | 4 |

Formulas: left stars = `row`, middle spaces = `2 * (numberOfRows - row)`, right stars = `row`.

**Code:**
```c
/* Upper half: stars grow, spaces shrink */
for (int row = 1; row <= numberOfRows; row++)
{
    for (int leftStar = 1; leftStar <= row; leftStar++)
    {
        printf("*");
    }
    for (int space = 1; space <= 2 * (numberOfRows - row); space++)
    {
        printf(" ");
    }
    for (int rightStar = 1; rightStar <= row; rightStar++)
    {
        printf("*");
    }
    printf("\n");
}

/* Lower half: stars shrink, spaces grow (same formulas, row runs backwards) */
for (int row = numberOfRows; row >= 1; row--)
{
    for (int leftStar = 1; leftStar <= row; leftStar++)
    {
        printf("*");
    }
    for (int space = 1; space <= 2 * (numberOfRows - row); space++)
    {
        printf(" ");
    }
    for (int rightStar = 1; rightStar <= row; rightStar++)
    {
        printf("*");
    }
    printf("\n");
}
```

**Explanation:**
- **Left star loop** prints `row` stars, forming the left wing.
- **Space loop** prints `2 * (numberOfRows - row)` blanks. The doubling is needed because the gap opens equally from both wings.
- **Right star loop** prints `row` stars, forming the right wing.
- The second block reverses the direction of `row` to create the lower wings. Starting the lower half at `numberOfRows` makes the two middle lines identical, which is the correct look for a butterfly.

---

# Group F: Special Famous Patterns

## Pattern 19: Pascal's Triangle

**Output (rows = 5):**
```
          1
        1   1
      1   2   1
    1   3   3   1
  1   4   6   4   1
```

**Logic:** Each number is the sum of the two numbers above it. These numbers are also the **binomial coefficients** (the counts of ways to choose items from a group). Instead of adding rows, we use a formula that produces each number from the one before it in the same row:

```
next coefficient = current coefficient × (row − column) ÷ (column + 1)
```

Here `row` and `column` begin counting from zero.

**Code:**
```c
for (int row = 0; row < numberOfRows; row++)
{
    int coefficient = 1;

    for (int space = 1; space <= numberOfRows - row - 1; space++)
    {
        printf("  ");
    }

    for (int column = 0; column <= row; column++)
    {
        printf("%4d", coefficient);
        coefficient = coefficient * (row - column) / (column + 1);
    }
    printf("\n");
}
```

**Explanation:**
- **`int row = 0; row < numberOfRows`** starts counting at zero this time, because the mathematical formula expects zero-based counting.
- **`int coefficient = 1;`** is created **inside** the outer loop so it resets to 1 at the beginning of every row. Every row of Pascal's triangle starts with 1.
- **Space loop** prints two blank characters per unit, pushing the row toward the center. The count `numberOfRows - row - 1` shrinks as the rows grow.
- **`printf("%4d", coefficient)`** prints the number in a field **four characters wide**. The `4` in `%4d` reserves space so the numbers stay lined up even when they have two digits.
- **`coefficient = coefficient * (row - column) / (column + 1);`** calculates the next number in the row from the current one. Multiplication happens first, then division, and because the result is always an exact whole number, nothing is lost.

---

## Pattern 20: Hourglass

**Output (rows = 5 for each half):**
```
*********
 *******
  *****
   ***
    *
   ***
  *****
 *******
*********
```

**Logic:** An inverted pyramid on top of a normal pyramid that shares the single-star middle row.

**Code:**
```c
/* Upper half: inverted pyramid */
for (int row = numberOfRows; row >= 1; row--)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * row - 1; star++)
    {
        printf("*");
    }
    printf("\n");
}

/* Lower half: normal pyramid, starting from row 2 so the middle is not repeated */
for (int row = 2; row <= numberOfRows; row++)
{
    for (int space = 1; space <= numberOfRows - row; space++)
    {
        printf(" ");
    }
    for (int star = 1; star <= 2 * row - 1; star++)
    {
        printf("*");
    }
    printf("\n");
}
```

**Explanation:**
- The upper half runs `row` **downward** from `numberOfRows` to 1. Using the pyramid formulas with a decreasing `row` makes the shape narrower toward the bottom.
- The lower half runs `row` **upward** from 2 to `numberOfRows`. It begins at 2 because row 1 (the single star in the middle) was already printed by the upper half.
- Same formulas, opposite directions: this is the reversing trick again.

---

## Pattern 21: Solid Rectangle with Custom Rows and Columns

**Output (rows = 3, columns = 6):**
```
* * * * * *
* * * * * *
* * * * * *
```

**Code:**
```c
int numberOfRows;
int numberOfColumns;

printf("Enter the number of rows: ");
scanf("%d", &numberOfRows);
printf("Enter the number of columns: ");
scanf("%d", &numberOfColumns);

for (int row = 1; row <= numberOfRows; row++)
{
    for (int column = 1; column <= numberOfColumns; column++)
    {
        printf("* ");
    }
    printf("\n");
}
```

**Explanation:**
- A square is a rectangle whose width equals its height. To allow different widths and heights, we ask for **two** separate numbers and use each as a separate loop limit.
- The outer loop uses `numberOfRows` (height). The inner loop uses `numberOfColumns` (width).

---

# The Master Cheat Sheet

## Quick reference table

| Pattern | Spaces in each row | Symbols in each row | Direction of rows |
|---|---|---|---|
| Solid square | none | `numberOfRows` | up |
| Right triangle | none | `row` | up |
| Inverted right triangle | none | `numberOfRows - row + 1` | up |
| Right-aligned triangle | `numberOfRows - row` | `row` | up |
| Full pyramid | `numberOfRows - row` | `2 * row - 1` | up |
| Inverted pyramid | `row - 1` | `2 * (numberOfRows - row) + 1` | up |
| Diamond (upper half) | `numberOfRows - row` | `2 * row - 1` | up |
| Diamond (lower half) | `numberOfRows - row` | `2 * row - 1` | **down**, starting at `numberOfRows - 1` |
| Butterfly | middle: `2 * (numberOfRows - row)` | each side: `row` | up, then **down** |

## Decision guide: which tool do I need?

| If the picture needs... | Use this |
|---|---|
| A shape that grows each line | Inner loop limit that includes `row` |
| A shape that shrinks each line | Inner loop limit using `numberOfRows - row`, or a downward outer loop |
| Empty area on the left | A separate loop that prints blanks **before** the symbols |
| Only the outline of a shape | An `if` statement checking for the edges, with `else` printing a blank |
| Numbers that restart each row | Print `column` |
| The same number across a row | Print `row` |
| Numbers that never restart | A counter variable created **outside** the loops |
| Letters | `'A' + offset` printed with `%c` |
| A symmetrical top and bottom | Two blocks of loops, the second with the row direction reversed |

## Printing placeholders you used

| Placeholder | Meaning |
|---|---|
| `%d` | Print a whole number |
| `%c` | Print a single character |
| `%4d` | Print a whole number inside a field four characters wide |
| `\n` | Move to the next line |

---

# Common Mistakes and How to Avoid Them

1. **Forgetting the newline.** If you forget `printf("\n");`, all the rows join into one long line. The newline must be **outside** the inner loop but **inside** the outer loop.
2. **Placing the newline inside the inner loop.** This puts every single symbol on its own line.
3. **Using one equals sign in a condition.** Writing `if (row = 1)` stores the value instead of comparing. Always use two equals signs `==` to compare.
4. **Mismatched widths.** If stars are printed as `"* "` (two characters wide), the blank space for alignment must also be two characters wide (`"  "`). A mismatch makes the pattern crooked.
5. **Off-by-one errors.** Starting at 0 instead of 1, or using `<` instead of `<=`, will give one row or column too many or too few. Test with a small number such as 3 and check by hand.
6. **Creating the counter inside the loop.** For continuous numbering (Floyd's Triangle) the counter must live outside the loops, otherwise it resets.
7. **Forgetting to reset a value for each row.** In Pascal's Triangle, `coefficient` must be set back to 1 at the start of each row, so it belongs inside the outer loop.
8. **Using the wrong loop variable name inside nested loops.** Always give the outer and inner loops different names (`row` and `column`), or the loops will interfere with each other.

---

# Practice Challenges

Try these without looking at the solutions above. Use the four-step method from Part 1: count the rows, tabulate spaces and symbols per row, find the formula, and convert each into a loop.

1. Print a hollow right triangle.
2. Print an inverted hollow pyramid.
3. Print a number diamond (the numbers `1` to the row number, mirrored).
4. Print a letter pyramid: `A`, `ABA`, `ABCBA`, and so on.
5. Print a hollow rectangle with a custom number of rows and columns.
6. Print the letter `X` shape using stars on both diagonals.
7. Print a right triangle made of a continuous alphabet: `A`, `BC`, `DEF`, `GHIJ`.

> **Final tip:** Every pattern in this guide is built from only **three ingredients**: a row loop, one or more symbol or space loops, and a newline. If you can identify the counts for each row, you can print any pattern.
