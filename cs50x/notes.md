# CS50x — Introduction to Computer Science

My personal notes from Harvard's CS50x course, covering computational thinking, programming fundamentals, data structures, algorithms, and web development.

---

## Section 0 — Scratch

### Number Systems

**Base-1 (Unary notation)**
- Example: counting on a human hand
- Pattern of fingers, symbols of different hand signals
- Up to 31 different numbers can be represented (on 5 fingers, binary)

**Base-2 (Binary system)**
- Binary digits — different number patterns mean different numbers or phrases
- **Bits:** elements of code, binary values (0s or 1s)
- Similar to how Roman numerals use "X, V, I" to create numbers
- A small set of characters can define multiple numbers and items

**Base-10 (Decimal)**
- The common base we use daily
- Each digit position has significance (e.g., 123 = hundred-twenty-three)
- Computers use binary (on/off switch) to distinguish information

### Bytes

A byte is 8 bits of binary:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|
| 0   | 0  | 0  | 0  | 0 | 0 | 0 | 0 |

**ASCII values:**
- Uppercase letters start from "A" = 65, "B" = 66, "C" = 67...
- Lowercase letters start from "a" = 97, "b" = 98, "c" = 99...
- Computers use bytes to represent the alphabet
- Some languages require more bits (up to 32 bytes per character in some encodings)

### Unicode and RGB

- **Unicode:** code that represents non-letter symbols such as emojis
- **RGB:** code that represents a color
- Computers pay attention to each pixel of color
- Usually uses 3 bytes (one per color), max value 255 per color
- Example: (72, 72, 33) = faint yellow

### Core Concepts

**Algorithm:** step-by-step instructions for how a computer stores data, processes bytes, and converts information. Computers often sort by dividing in the middle first, then working outward to minimize time/energy.

**Pseudocode:** a step-by-step plan for how to achieve a goal or assignment.
- Example: a "how-to" for finding a specific item in a phonebook using divide-and-conquer
- Actions command the computer to do specific things
- Indentation matters for control flow
- Loops tell a computer to run code repeatedly

**Rubber Duck Debugging:** decoding and looking for errors by explaining your code line-by-line.

### Scratch

- Drag-and-drop coding for beginners
- Functions in Scratch are a form of pseudocode
- **Inputs (arguments)** and **outputs**
- **Return values:** values returned and stored for future use
- You can create reusable blocks (functions)
- Forever loops continue until a stop condition is met

---

## Section 1 — C

### Development Environment

- **GUI (Graphical User Interface):** items the user can interact with visually
- **CUI/CLI (Command-Line Interface):** typing commands instead of clicking
- Run programs through the CLI

### Writing C Code

1. Create the program file with `.c` extension
2. Run the compiler with `make`
3. Execute and run the file

### Key Concepts

- `\n` indicates a new line
- **Header files:** definitions and structures others made for you (e.g., `stdio.h`)
- Without header files, you cannot use library functions
- **Library:** collection of code someone else wrote (functions like `get`, `set`, `print`)
- Variables can be used with functions for reuse
- `$` in the terminal signifies a change has been made within the program

### Conditionals

- `if`/`else` test variables against conditions
- Allow you to write less code and run programs more efficiently
- `const` (constant) locks a variable's value so it cannot be edited

### Data Types and Formatting

- `long` (longer int) can hold 64 bits, extends range for large numbers
- **Format specifiers:**
  - `%s` — string placeholder
  - `%f` — float
  - `%i` — integer
- **Casting:** combining different data types (e.g., int with string) requires casting

### Loops

- **Do-while loop:** runs at least once (a regular while loop only runs if the condition is true)
- Variables declared in loops must be accessible outside if needed
- For loops can create rows and columns (nested loops)
- `printf` can be used inside or outside loops
- Use `,` (commas) to join variables with strings in print functions

---

## Section 2 — Arrays

### Compilation Process

1. **Preprocessing:** handles `#include` directives
2. **Compiling:** translates code to assembly
3. **Assembly:** converts assembly to machine code (binary)
4. **Linking:** combines your code with library code into one executable

### Debugging

- **debug50:** CS50 library function that creates breakpoints to find errors
- **Step Over:** skips a line of code
- **Step Into:** rechecks a specific line of code
- Play/Stop buttons run or halt the debugger

### Data Types

- String
- Int
- Long
- Float
- Char
- Double
- Bool

**Important:** Cast to float when dividing two ints to avoid truncation: `(float)(int/int)`

### Arrays

- An array is a sequence of memory holding multiple values of the same data type
- Use for loops to populate arrays with user input
- Use `const` to prevent the array size from changing
- For dynamic size, use a variable based on user input
- Declare empty array: `int array[];`

### Strings as Arrays

- A string is a contiguous sequence of memory (chars in an array)
- All strings have an extra byte at the end: `\0` (NUL terminator)
- Use a loop to find string length
- Access characters with double brackets: `words[0][1]` gets the 2nd character of the 1st word

### String Libraries

- `<string.h>` contains `strlen` (string length)
- `<ctype.h>` contains:
  - `isNum`
  - `isAlpha`
  - `toupper()` — converts to uppercase

### For Loop Optimization

You can declare multiple variables in a for loop:

```c
for (int i = 0, n = strlen(s); i < n; i++)
```

This calculates the string length once instead of each iteration.

### Manual Case Conversion

- Difference between uppercase and lowercase ASCII values is 32
- Subtract 32 from a lowercase letter to make it uppercase (without using a library)

### Command Line Arguments

- Allows the user to input arguments directly into `main`
- Example: `int main(int argc, string argv[])`
- `argc` = argument count, `argv` = argument vector (array of strings)
- Check exit status with `echo $?`

### Cryptography

- **Encryption:** scrambles text for security/privacy
- **Cipher:** scrambles the text
- **Ciphertext:** the scrambled output
- Example: "HI" with cipher 13 = "UV" (Caesar cipher)
- **Decryption:** reverses the cipher (subtract instead of add)

---

## Section 3 — Sorting

### Running Time

The amount of time it takes the computer to find a specific value. Sorting data in an organized way makes computation faster.

### Searching

- **Linear search:** check each element one by one (worst case: element at the end)
- **Binary search:** divide and conquer on sorted data (worst case: element at the start)

### Comparing Strings

- Cannot use `==` for strings (compares memory addresses)
- Use `strcmp()` from `<string.h>`
- Returns 0 if strings match: `if (strcmp(strings[i], s) == 0)`

### Data Structures (structs)

Custom data types that bundle variables together:

```c
typedef struct
{
    string name;
    string number;
}
person;
```

- Access struct members with dot notation: `person[1].name`, `person[1].number`
- Populate with for loops and user input

### Sorting Algorithms

**Selection Sort**
- Find the smallest element and swap it to the front
- Repeat for the rest of the array
- Works "blindly" starting from the first element

**Bubble Sort**
- Compare adjacent elements `[i]` and `[i+1]`
- Swap if out of order
- Each pass "bubbles" the largest element to the end

**Recursion**
- A function that calls itself
- Has two parts: **base case** and **recursive case**
- For factorials: multiply by `(n-1)` until base case
- Creates a pyramid-like call stack

**Merge Sort**
- Sort the left half, then the right half, then merge them
- Example: `[3 1 4 6 0 2 5 7]` → `[3 1 4 6][0 2 5 7]` → keep splitting → merge sorted halves
- Much faster: O(n log n) time
- Requires an additional array for merging

### Summary
- Selection sort = front-half focused
- Bubble sort = back-half focused
- Merge sort = middle-out (divide and conquer)

---

## Section 4 — Memory

### Pixel Art and Color

- Images are composed of 0s and 1s (binary)
- **RGB:** colors picked from 3 values
- **Hexadecimal:** base-16 (0-9, A-F) for representing colors
- Hex prefix: `0x` (the "x" just indicates hexadecimal)

### Pointers

- `&` — gets the address of a variable
- `*` — dereference operator, goes to the location in memory
- `%p` — prints a pointer (memory address)

**Pointer syntax:**

```c
int n = 0;
int *p = &n;  // p stores the address of n
```

- The pointer is like a "treasure map" — it points to the treasure (variable)
- Everything in memory has a pointer because everything has an address
- Dereferencing a NULL pointer crashes the program (intentionally — prevents worse errors)
- All primitive data types with pointers are 4 or 8 bytes (depending on system)

### Strings in C

- Strings are arrays of characters, each with its own memory address
- A string's "address" is the address of its first character
- The string ends at the NUL terminator (`\0`)
- You can replace the CS50 `string` type with `typedef char *string;`

### typedef

Create shorthand names for data types:

```c
typedef <oldname> <newname>;
```

Combined with structs, allows custom data types.

### Pointer Arithmetic

Math on addresses:

```c
printf("%c\n", s[0]);      // traditional
printf("%c\n", *s);        // dereference
printf("%c\n", *(s + 1));  // pointer arithmetic
printf("%s\n", s + 2);     // prints from s[2] onward
```

### Why `strcmp` Exists

- Strings can't be compared with `==` because that compares memory addresses, not content
- `strcmp` iterates through each character to compare values
- Setting two strings equal makes them share a memory address (one change affects both)

### Dynamic Memory

**`malloc`** — allocates memory in bytes

```c
int* b = malloc(sizeof(int));
```

- Returns a pointer to the allocated memory
- Returns NULL if there's no memory available

**`free`** — releases allocated memory back to the system

```c
free(b);
```

- Every `malloc` must have a matching `free`
- Without freeing, you cause memory leaks

**`<strcpy>`** — in `<string.h>`, copies a string's value to a new memory location

### Valgrind

A tool to detect memory leaks and bugs in malloc usage. Run with:

```bash
valgrind ./program
```

### Garbage Values

When variables aren't initialized, they contain "garbage" — leftover data from memory. Always initialize pointers and numeric variables.

### Swapping Variables

Requires a temporary variable:

```c
int temp = x;
x = y;
y = temp;
```

### Scope and Pass by Reference

- Variables are normally passed by **value** (function gets a copy)
- To modify the original, pass by **reference** using pointers

```c
void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

int main(void)
{
    int x = 1;
    int y = 2;
    swap(&x, &y);
}
```

### Memory Layout

A program's memory is organized as:
- Machine code
- Global variables
- Heap (grows down) ↓
- ↑ Stack (grows up)

### Overflow Types

- **Heap overflow:** touching memory you shouldn't (heap-side)
- **Stack overflow:** too many function calls (stack-side)

### `scanf`

Scans user input — works like `get_int` but with pointers. Less safe than CS50's `get_string` for strings (can cause crashes from buffer overflows).

### File I/O

```c
FILE *src = fopen(argv[1], "rb");  // read binary
FILE *dst = fopen(argv[2], "wb");  // write binary
BYTE b;
while (fread(&b, sizeof(b), 1, src) != 0)
{
    fwrite(&b, sizeof(b), 1, dst);
}
fclose(dst);
fclose(src);
```

**Key functions:**
- `fopen` — opens a file
- `fclose` — closes a file
- `fread` — reads data
- `fwrite` — writes data
- `fgetc` — reads a single character
- `fputc` — writes a single character
- `fgets` / `fputs` — string versions
- `fprintf` — formatted write
- `fseek` — move within a file
- `ftell` — current byte position
- `feof` — check if at end of file
- `ferror` — check for errors

### Call Stack

- Function calls create stack frames
- New function = new active frame on top
- When a frame finishes, it pops off and control returns to the frame below
- This is what enables recursion

---

## Section 5 — Data Structures (hardest week)

### Abstract Data Types

Ways of structuring information that don't rely on specific implementation details — customizable to the creator.

### Queues (FIFO — First In, First Out)

Like a line at a store. Operations:
- **Enqueue:** add to the end
- **Dequeue:** remove from the front

```c
typedef struct
{
    VALUE array[CAPACITY];
    int front;
    int size;
}
queue;
```

The `front` index tracks where the oldest element is. We use modulo to wrap around the array.

### Stacks (LIFO — Last In, First Out)

Like a stack of plates. Operations:
- **Push:** add to the top
- **Pop:** remove from the top

```c
typedef struct
{
    VALUE array[CAPACITY];
    int top;
}
stack;
```

### Linked Lists

Using pointers to link nodes together — no need for contiguous memory.

```c
typedef struct node
{
    int number;
    struct node *next;
}
node;
```

**Building a list:**

```c
node *list = NULL;

for (int i = 0; i < 3; i++)
{
    node *n = malloc(sizeof(node));
    if (n == NULL) return 1;

    n->number = get_int("Number: ");
    n->next = NULL;

    // Prepend node to list
    n->next = list;
    list = n;
}
```

- `->` is shorthand for `(*n).` — dereferences and accesses field
- This creates a backwards list (LIFO behavior)
- To make it a queue (FIFO), append to the end instead

### Singly Linked Lists

- Each node has a value and a `next` pointer
- Can only traverse forward
- Operations: `find`, `insert`, `destroy`
- `destroy` is often implemented recursively

### Doubly Linked Lists

- Each node has `next` AND `prev` pointers
- Can traverse both directions
- More complex insertion/deletion (must update both pointers)

### Trees

Hierarchical data structure (like a family tree).

### Binary Search Trees

- Left subtree = values less than current node
- Right subtree = values greater than current node
- Enables fast searching

### Dictionaries

Key-value pairs (like a phonebook: name → number).
- Keys usually strings
- Values can be any type
- Fast lookup when implemented with hashing

### Hash Tables

A combination of arrays and linked lists.

**Hash function:** decides where a value goes in memory.

**Collisions:** when two values hash to the same location.

**Solutions:**
- **Linear probing:** find the next open slot (causes clustering — defeats the purpose)
- **Chaining:** use linked lists at each slot (better, maintains O(1) average)

Example hash function:

```c
unsigned int hash(const char *word)
{
    return toupper(word[0]) - 'A';
}
```

### Tries

A tree of arrays — always searchable in constant time, but memory-heavy.

- Each node is an array of pointers (one per possible character)
- Path from root to leaf spells out a word/value

```c
typedef struct trie
{
    char university[20];
    struct trie *paths[10];
}
trie;
```

### Data Structure Comparison

| Structure | Insertion | Deletion | Lookup | Sorting | Size |
|-----------|-----------|----------|--------|---------|------|
| Arrays | Bad (shifting needed) | Bad (shifting needed) | Great | Easy | Fixed |
| Linked Lists | Easy (front) | Easy (once found) | Bad (linear) | Hard | Dynamic |
| Hash Tables | Easy (hash + add) | Easy (once found) | Better than linked lists | Not ideal | Depends on data |
| Tries | Complex (malloc needed) | Easy (free a node) | Fast | Pre-sorted | Large |

---

## Section 6 — Python

### Running Python

```bash
python file.py
```

### C vs. Python — Printing

```c
// C
printf("hello, world\n");
```

```python
# Python
print("hello, world")
```

### Libraries

```python
import cs50
# Or individually:
from cs50 import get_float, get_int, get_string
```

### Strings

Three ways to combine strings:

```python
print("hello, " + name)        # concatenation
print("hello,", name)           # comma separator
print(f"hello, {name}")         # f-string (formatting)
```

Python detects the variable type automatically — no need to declare.

### Differences from C

- Auto-newline on print (no need for `\n`)
- Use `end=""` to suppress the newline
- `"` and `'` both create strings (no difference)
- No `counter++` or `counter--` — use `counter += 1`
- Comments use `#`, not `//`

### Data Types

Same as C, but:
- No `char` (use strings)
- No `long` or `double`
- Adds: `range`, `list`, `tuple`, `dict`, `set`

### Conditionals

```python
if x < y:
    # do something
elif x == y:
    # do something else
else:
    # otherwise
```

- Indentation matters (no curly braces)
- Use `and`/`or` instead of `&&`/`||`
- Use `not` instead of `!`
- `in` checks membership: `if s in ["y", "yes"]:`
- `True`/`False` are capitalized

### Object-Oriented Programming (OOP)

Instead of structs in C, Python has objects.

- **Methods:** functions associated with a data type
- Example:
  ```python
  s = input("s: ")
  t = s.capitalize()
  ```
- `def __init__` initializes class variables
- Use `self.item = item` inside class methods

### Loops

```python
for i in range(3):
    print("meow")
```

- `range()` generates a sequence of numbers
- No need to manually increment

String methods:
```python
before = input("Before: ")
after = before.upper()
print(f"After: {after}")
```

### Functions

```python
def square(x):
    result = 0
    for i in range(0, x):
        result += x
    return result
```

- `def` defines a function
- No return type needed

### Truncation and Floating Point

- Python auto-floats when dividing two integers
- No need to cast (unlike C)

### Exception Handling

```python
try:
    n = int(input("Input: "))
    print("Integer.")
except ValueError:
    print("Not integer.")
```

- Use `.isnumeric()` method to check if a string is a number
- `try`/`except` overrides errors gracefully

### Lists

Built-in functions:
- `sum(list)` — adds elements
- `len(list)` — length
- `list.append(x)` — add at end (or `list += [x]`)
- `list.insert(x, y)` — insert `y` at position `x`

### Tuples

Ordered, immutable sets (similar to structs in C). Indicated by parentheses.

```python
for x, y in tuple_name:
    # iterate
```

### Dictionaries

Key-value collections:

```python
people = {
    "Yuliia": "+1-617-495-1000",
    "David": "+1-617-495-1000",
    "John": "+1-949-468-2750",
}

name = input("Name: ")
if name in people:
    print(f"Number: {people[name]}")
else:
    print("Not found")
```

- Use `.items()` to iterate keys and values together
- Built-in `in` operator for searching

### Command Line Arguments

```python
from sys import argv

if len(argv) == 2:
    print(f"hello, {argv[1]}")
else:
    print("hello, world")
```

### Exit Status

```python
import sys

if len(sys.argv) != 2:
    print("Missing command-line argument")
    sys.exit(1)
print(f"hello, {sys.argv[1]}")
sys.exit(0)
```

Similar to `return 0`/`return 1` in C.

### CSV Files

```python
import csv

name = input("Name: ")
number = input("Number: ")

with open("phonebook.csv", "a") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "number"])
    writer.writerow({"name": name, "number": number})
```

`with` statement automatically opens/closes the file.

### Third-Party Libraries

Use `pip install <library>`:

```bash
pip install cs50
```

---

## Section 7 — SQL: Structured Query Language

### Purpose

SQL is designed to query databases (ask questions of stored data).

### Data Types

- `VARCHAR(n)` — variable-length string (no fixed CHAR type in SQLite)
- Must specify length for strings
- Specify a primary key for unique identification
- Set columns to autoincrement to avoid duplicate IDs

### Flat-File Databases

Data shown as rows and columns:
- **CSV** — comma-separated values (Excel, Google Sheets)
- Python natively supports CSV files

### Relational Databases

The ability to relate one type of data to another.

### CRUD Operations

- **Create** — `INSERT INTO`
- **Read** — `SELECT`
- **Update** — `UPDATE`
- **Delete** — `DELETE`

### Creating Tables

```sql
CREATE TABLE table_name (column_name TYPE, ...);
```

### Using SQLite

```bash
sqlite3 FILE
```

Inside SQLite:
- `.schema` — view database structure

### Reading Data

```sql
SELECT columns FROM table;
SELECT language FROM favorites;
```

**Aggregate functions:**
- `AVG`, `COUNT`, `DISTINCT`, `LOWER`, `MAX`, `MIN`, `UPPER`

```sql
SELECT COUNT(*) FROM favorites;
```

**Filtering and sorting:**
- `WHERE` — filter by condition
- `LIKE` — pattern matching
- `ORDER BY` — sort
- `LIMIT` — restrict results
- `GROUP BY` — aggregate by category

### Filtering Examples

```sql
SELECT COUNT(*) FROM favorites
WHERE language = 'C' AND problem = 'Hello, World';

SELECT COUNT(*) FROM favorites
WHERE language = 'C' AND problem LIKE 'Hello, %';
```

- Single quotes are native to SQL (double quotes also work)
- `%` is a wildcard
- Escape apostrophes by doubling them: `'It''s Me'`

### Grouping and Sorting

```sql
SELECT language, COUNT(*) AS n FROM favorites
GROUP BY language
ORDER BY n DESC
LIMIT 1;
```

### Inserting Data

```sql
INSERT INTO favorites (language, problem)
VALUES ('SQL', 'Fiftyville');
```

### Deleting Data

```sql
DELETE FROM favorites WHERE Timestamp IS NULL;
```

**Always specify a condition!** Otherwise you'll delete the entire table.

### Updating Data

```sql
UPDATE favorites SET language = 'SQL', problem = 'Fiftyville'
WHERE id = 1;
```

### Comments

```sql
-- This is a comment
```

### Relationships

**IMDb example schema:**
- Tables: `shows`, `ratings`, `genres`, `writers`, `stars`, `people`
- Tables reference each other via foreign keys

**One-to-one:** each show has one rating
**One-to-many:** one show has many genres
**Many-to-many:** shows ↔ people (via `stars` join table)

### SQLite Data Types

- `BLOB` — binary large objects
- `INTEGER` — whole numbers
- `NUMERIC` — formatted numbers (dates)
- `REAL` — floating point
- `TEXT` — strings

**Column constraints:**
- `NOT NULL`
- `UNIQUE`

### Nested Queries

```sql
SELECT title FROM shows
WHERE id IN (
    SELECT show_id FROM ratings
    WHERE rating >= 6.0
    LIMIT 10
);
```

### Joins

```sql
SELECT * FROM shows
JOIN ratings ON shows.id = ratings.show_id
WHERE rating >= 6.0
LIMIT 10;
```

### Many-to-Many Query Example

```sql
SELECT name FROM people WHERE id IN
    (SELECT person_id FROM stars WHERE show_id =
        (SELECT id FROM shows WHERE title = 'The Office' AND year = 2005));
```

### Indexes

Speed up queries by pre-organizing data:

```sql
CREATE INDEX title_index ON shows (title);
CREATE INDEX name_index ON people (name);
```

- Implements a B-tree data structure
- Speeds up queries but uses extra memory

### Using SQL in Python

```python
from cs50 import SQL

db = SQL("sqlite:///favorites.db")

favorite = input("Favorite: ")
rows = db.execute("SELECT COUNT(*) AS n FROM favorites WHERE language = ?", favorite)
row = rows[0]
print(row["n"])
```

- `?` is a placeholder (prevents SQL injection)

### Race Conditions

Multiple users executing the same commands simultaneously can cause data loss.

**Solutions:**
- `BEGIN TRANSACTION`
- `COMMIT`
- `ROLLBACK`

These "lock" the database during execution.

### SQL Injection Attacks

Malicious users inject SQL code via input fields:

```python
# DANGEROUS:
rows = db.executef(f"SELECT * FROM users WHERE name = '{username}'")
```

If `username` is `' OR 1=1 --`, the query returns all users.

**Solution:** Always use placeholders (`?` in CS50's SQL library).

---

## Section 8 — HTML, CSS, JavaScript

### Networking Basics

**Routers:** transfer data from point A to point B via packets.

**TCP/IP:** two protocols that enable computers to communicate.

**IP (Internet Protocol):**
- Identifies computers on a network
- Connectionless protocol (no fixed path)
- IPv4 addresses: 32 bits (4 bytes), e.g., `192.168.1.1`

**TCP (Transmission Control Protocol):**
- Acknowledges packets received
- Handles packet sequencing
- Defines ports

**Ports:** Unique identifiers for different services (HTTP = 80, HTTPS = 443, etc.)

### DNS (Domain Name System)

Translates domain names to IP addresses (e.g., `google.com` → IP address).

### DHCP

Assigns IP addresses to devices when they connect to a network.

### HTTPS

HyperText Transfer Protocol Secure — encrypted communication.

### URL Anatomy

```
https://www.example.com/folder/file.html
```

- `https://` — protocol
- `www.example.com` — server (with TLD `.com`)
- `/folder/file.html` — path

### HTTP Methods

- `GET` — request data
- `POST` — send data

### HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 301 | Moved Permanently |
| 302 | Found |
| 304 | Not Modified |
| 307 | Temporary Redirect |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 418 | I'm a Teapot |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

### HTML Basics

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>hello, title</title>
    </head>
    <body>
        hello, body
    </body>
</html>
```

### Common Tags

**Paragraphs and headings:**

```html
<p>This is a paragraph.</p>
<h1>Heading 1</h1>
<h2>Heading 2</h2>
```

**Lists:**

```html
<ul>
    <li>Unordered item</li>
</ul>

<ol>
    <li>Ordered item</li>
</ol>
```

**Tables:**

```html
<table>
    <tr>
        <td>1</td>
        <td>2</td>
    </tr>
</table>
```

**Media:**

```html
<img alt="description" src="image.png">
<video controls muted>
    <source src="video.mp4" type="video/mp4">
</video>
```

**Hyperlinks:**

```html
<a href="https://www.harvard.edu">Harvard</a>
```

**Forms:**

```html
<form action="https://www.google.com/search" method="get">
    <input autocomplete="off" autofocus name="q" placeholder="Query" type="search">
    <button>Google Search</button>
</form>
```

### Regular Expressions (Regex)

Validate user input:

```html
<input pattern=".+@.+\.edu" type="email">
```

### CSS

**Inline styles:**

```html
<p style="font-size: large; text-align: center;">Hello</p>
```

**Internal stylesheet:**

```html
<style>
    .centered {
        text-align: center;
    }
    .large {
        font-size: large;
    }
</style>
```

**External stylesheet:**

```html
<link href="styles.css" rel="stylesheet">
```

CSS comments: `/* comment */`

### Frameworks (Bootstrap)

Pre-built CSS for clean designs:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
```

### JavaScript

- Derived from C syntax
- Runs in `.js` files or `<script>` tags
- Event-driven (responds to user actions)

**Variables:**
- `let` — block-scoped
- `var` — function-scoped (older)
- `const` — constant

**Conditionals:**

```javascript
if (x < y) {
    return true;
}
```

**Objects (similar to Python dicts):**

```javascript
var x = { "key1": 1, "key2": 2 };
```

**Loops:**

```javascript
for (var key in object) {
    // use object[key]
}

for (var value of array) {
    // use value
}
```

**Useful methods:**
- `console.log()` — print
- `parseInt()` — convert string to int
- `.map()` — apply function to each array element

### Event Listeners

```javascript
document.addEventListener('DOMContentLoaded', function() {
    document.querySelector('form').addEventListener('submit', function(e) {
        alert('hello, ' + document.querySelector('#name').value);
        e.preventDefault();
    });
});
```

- `DOMContentLoaded` — runs after page loads
- `addEventListener` — attaches a handler to an event
- `e.preventDefault()` — stops default form submission

### Live Input Example

```javascript
let input = document.querySelector('input');
input.addEventListener('keyup', function(event) {
    let name = document.querySelector('p');
    if (input.value) {
        name.innerHTML = `hello, ${input.value}`;
    } else {
        name.innerHTML = 'hello, whoever you are';
    }
});
```

### Color Button Example

```javascript
let body = document.querySelector('body');
document.querySelector('#red').addEventListener('click', function() {
    body.style.backgroundColor = 'red';
});
```

### Blink Toggle

```javascript
function blink() {
    let body = document.querySelector('body');
    if (body.style.visibility == 'hidden') {
        body.style.visibility = 'visible';
    } else {
        body.style.visibility = 'hidden';
    }
}
window.setInterval(blink, 500);
```

### DOM (Document Object Model)

The webpage as a tree of nodes.

**Properties:**
- `innerHTML` — HTML inside an element
- `nodeName` — element name
- `id` — element ID
- `parentNode` — node above in tree
- `childNodes` — nodes below in tree
- `attributes` — element attributes
- `style` — CSS styling

**Methods:**
- `getElementById(id)`
- `getElementsByTagName(tag)`
- `appendChild(node)`
- `removeChild(node)`

### jQuery

A JavaScript library that simplifies DOM manipulation:

```javascript
// Without jQuery
document.getElementById('colorDiv').style.backgroundColor = 'green';

// With jQuery
$('#colorDiv').css('background-color', 'green');
```

---

## Section 9 — Flask

### Why Flask?

HTML alone is static — everything must be hand-coded. Flask is a Python framework for building dynamic web applications.

### Basic Flask App

```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
    return "hello, world"
```

Run with:

```bash
flask run
```

### Routes and Decorators

`@app.route("/")` is a decorator that associates a function with a URL.

### Templates

Flask uses **Jinja** for templating:

```html
<!-- index.html -->
<body>
    hello, {{ name }}
</body>
```

```python
@app.route("/")
def index():
    name = request.args.get("name", "world")
    return render_template("index.html", name=name)
```

### Template Inheritance

**layout.html:**

```html
<body>
    {% block body %}{% endblock %}
</body>
```

**Other templates extend it:**

```html
{% extends "layout.html" %}

{% block body %}
    <form action="/greet" method="get">
        <input name="name" type="text">
        <button>Greet</button>
    </form>
{% endblock %}
```

### Request Methods

```python
@app.route("/greet", methods=["GET", "POST"])
def greet():
    return render_template("greet.html", name=request.form.get("name", "world"))
```

- `request.args` — GET parameters
- `request.form` — POST data

### Form Validation Example

```python
SPORTS = ["Basketball", "Soccer", "Ultimate Frisbee"]

@app.route("/register", methods=["POST"])
def register():
    name = request.form.get("name")
    if not name:
        return render_template("error.html", message="Missing name")

    sport = request.form.get("sport")
    if not sport:
        return render_template("error.html", message="Missing sport")
    if sport not in SPORTS:
        return render_template("error.html", message="Invalid sport")

    return redirect("/registrants")
```

### Using SQL with Flask

```python
from cs50 import SQL
from flask import Flask, redirect, render_template, request

app = Flask(__name__)
db = SQL("sqlite:///froshims.db")

@app.route("/register", methods=["POST"])
def register():
    name = request.form.get("name")
    sport = request.form.get("sport")
    db.execute("INSERT INTO registrants (name, sport) VALUES(?, ?)", name, sport)
    return redirect("/registrants")

@app.route("/registrants")
def registrants():
    registrants = db.execute("SELECT * FROM registrants")
    return render_template("registrants.html", registrants=registrants)
```

### Cookies and Sessions

**MVC pattern:**
- **C**ontroller — `app.py` (what we do)
- **V**iew — what the user sees (HTML)
- **M**odel — how data is stored (database)

**Cookies:** values stored on the user's computer to remember preferences/logins.

**Sessions:** per-user global variables for storing state (like a shopping cart).

### Session Configuration

```python
from flask import Flask, session
from flask_session import Session

app = Flask(__name__)
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)
```

### Shopping Cart Example

```python
@app.route("/cart", methods=["GET", "POST"])
def cart():
    if "cart" not in session:
        session["cart"] = []

    if request.method == "POST":
        book_id = request.form.get("id")
        if book_id:
            session["cart"].append(book_id)
        return redirect("/cart")

    books = db.execute("SELECT * FROM books WHERE id IN (?)", session["cart"])
    return render_template("cart.html", books=books)
```

### APIs and JSON

**API (Application Programming Interface):** specifications that allow services to interact.

**JSON (JavaScript Object Notation):** text format of key-value pairs.

### Fetching Data with JavaScript

```javascript
let input = document.querySelector('input');
input.addEventListener('input', async function() {
    let response = await fetch('/search?q=' + input.value);
    let shows = await response.json();
    let html = '';
    for (let id in shows) {
        let title = shows[id].title.replace('<', '&lt;').replace('&', '&amp;');
        html += '<li>' + title + '</li>';
    }
    document.querySelector('ul').innerHTML = html;
});
```

### Useful Flask Functions

- `url_for()` — dynamically generate URLs
- `redirect()` — redirect to another route
- `session()` — manage user state
- `render_template()` — render HTML templates

### AJAX

Asynchronous JavaScript and JSON — refresh parts of a page without reloading the whole page.

---

## Section 10 — The End

> **"Learn to teach yourself."**

### Next Steps

- Choose any topic for the final project
- Use AI tools, Google, Stack Overflow
- Set up VS Code on a personal computer
- Learn GitHub for hosting projects
- Explore cloud services:
  - GitHub Education
  - Heroku
  - Vercel
  - Google Cloud (Students)
  - Azure
  - AWS Educate

### Resources

- [ChatGPT](https://chat.openai.com)
- [GitHub Copilot](https://github.com/features/copilot)
- Reddit (r/programming)
- Stack Overflow
- TechCrunch

### Other CS50 Courses

- CS50 Python
- CS50 Web
- CS50 R
- CS50 AI
- CS50 SQL
- CS50 Cybersecurity

---

*Completed CS50x — Harvard University*
