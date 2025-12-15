# OOP Notebook - Q&A

> Your personal notebook for explanations and clarifications

---

## Question 1: Explain Pointers in C++

**Asked on:** 2025-12-16

### What is a Pointer?

A **pointer** is a variable that stores the **memory address** of another variable, not the value itself.

Think of it like this:

- A variable is like a **house** (stores something inside)
- A pointer is like a **paper with the house address** (tells you where the house is)

---

### Breaking Down the Code:

```cpp
int x = 10;
int *ptr = &x;   // Pointer stores address
```

**Step-by-step:**

1. `int x = 10;`

   - Creates a variable `x` in memory
   - Stores the value `10` in it
   - Let's say `x` is stored at memory address `1000`

2. `int *ptr = &x;`
   - `int *ptr` → Declares a pointer named `ptr` that can point to an integer
   - `&x` → The `&` (address-of operator) gets the address of `x`, which is `1000`
   - So `ptr` now stores `1000` (the address of `x`)

**Memory Visualization:**

```
Memory Address    Variable    Value
--------------    --------    -----
1000              x           10
2000              ptr         1000  (stores address of x)
```

---

### The Two Key Operators:

#### 1. `&` - Address-of Operator

Gets the memory address of a variable.

```cpp
int x = 10;
cout << &x;   // Prints something like: 0x7fff5fbff8ac (memory address)
```

#### 2. `*` - Dereference Operator

Gets the value stored at an address (goes to the address and reads what's there).

```cpp
int x = 10;
int *ptr = &x;

cout << ptr;    // Prints: 0x7fff5fbff8ac (the address stored in ptr)
cout << *ptr;   // Prints: 10 (the value AT that address)
```

**Think of `*` as "go to the address and see what's inside"**

---

### Pointer Arithmetic:

```cpp
ptr++;   // Move to next int address
```

When you do `ptr++` on an integer pointer:

- It doesn't add 1 to the address
- It adds `sizeof(int)` (typically 4 bytes) to the address
- So if `ptr` was `1000`, after `ptr++` it becomes `1004`

**Why?** Because the next integer in memory starts 4 bytes later.

```
Address:  1000  1001  1002  1003  1004  1005  1006  1007
          |---- int x ----|      |---- next int ---|

ptr = 1000
ptr++ → ptr = 1004 (moved to next integer position)
```

---

### Complete Example with Output:

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    int *ptr = &x;

    cout << "Value of x: " << x << endl;           // 10
    cout << "Address of x: " << &x << endl;        // 0x7fff... (some address)
    cout << "Value in ptr: " << ptr << endl;       // 0x7fff... (same address)
    cout << "Value at *ptr: " << *ptr << endl;     // 10

    // Modify x through pointer
    *ptr = 20;
    cout << "New value of x: " << x << endl;       // 20

    return 0;
}
```

---

### Quick Summary Table:

| Expression | Meaning                        | Example Result        |
| ---------- | ------------------------------ | --------------------- |
| `x`        | Value of x                     | `10`                  |
| `&x`       | Address of x                   | `0x1000`              |
| `ptr`      | Value stored in ptr (address)  | `0x1000`              |
| `*ptr`     | Value at the address ptr holds | `10`                  |
| `ptr++`    | Move to next memory location   | Address + sizeof(int) |

---

### Why Are Pointers Useful?

1. **Dynamic Memory Allocation** - Create arrays of unknown size at runtime
2. **Pass by Reference** - Modify original variables in functions
3. **Data Structures** - Build linked lists, trees, graphs
4. **Efficiency** - Pass large data without copying

---

### Common Mistakes to Avoid:

```cpp
int *ptr;        // Uninitialized pointer - DANGEROUS!
*ptr = 10;       // Crash! Trying to write to random memory

int *ptr = NULL; // Safe - initialized to NULL
if (ptr != NULL) {
    *ptr = 10;   // Only use if not NULL
}
```

---

> **Remember:**
>
> - `&` = "give me the address"
> - `*` = "go to the address and give me the value"

---

---

## Question 2: Explain Storage Classes in Detail

**Asked on:** 2025-12-16

### What are Storage Classes?

Storage classes define **4 things** about a variable:

1. **Where** it's stored (memory/register)
2. **Scope** - Where can you access it?
3. **Lifetime** - How long does it exist?
4. **Default value** - What value if not initialized?

---

### 1. Automatic (`auto`)

**The default storage class for local variables.**

```cpp
void function() {
    auto int x = 10;  // 'auto' is optional, it's the default
    int y = 20;       // Same as above
}
```

| Property      | Value                             |
| ------------- | --------------------------------- |
| Storage       | RAM (Stack)                       |
| Scope         | Local (inside the block/function) |
| Lifetime      | Until function ends               |
| Default value | Garbage (random)                  |

**Note:** In modern C++ (C++11+), `auto` has a different meaning - it lets compiler deduce the type:

```cpp
auto x = 10;      // x is int
auto y = 3.14;    // y is double
auto z = "hello"; // z is const char*
```

---

### 2. Register (`register`)

**Request to store variable in CPU register for faster access.**

```cpp
void function() {
    register int counter = 0;
    for (register int i = 0; i < 1000000; i++) {
        counter++;
    }
}
```

| Property      | Value                       |
| ------------- | --------------------------- |
| Storage       | CPU Register (if available) |
| Scope         | Local                       |
| Lifetime      | Until function ends         |
| Default value | Garbage                     |

**Key Points:**

- It's a **request**, not a command - compiler may ignore it
- Cannot use `&` (address-of) on register variables
- Modern compilers optimize automatically, so rarely used now
- Best for: loop counters, frequently accessed variables

```cpp
register int x = 10;
// cout << &x;  // ERROR! Cannot take address of register variable
```

---

### 3. Static (`static`) - MOST IMPORTANT!

**Variable retains its value between function calls.**

```cpp
void counter() {
    static int count = 0;  // Initialized ONLY ONCE
    count++;
    cout << "Called " << count << " times" << endl;
}

int main() {
    counter();  // Output: Called 1 times
    counter();  // Output: Called 2 times
    counter();  // Output: Called 3 times
    return 0;
}
```

| Property      | Value                                |
| ------------- | ------------------------------------ |
| Storage       | RAM (Data segment, not stack)        |
| Scope         | Local (but value persists)           |
| Lifetime      | Entire program                       |
| Default value | 0 (for numbers), NULL (for pointers) |

**Memory Visualization:**

```
First call:
  static count = 0 → count++ → count = 1

Second call:
  count is still 1 → count++ → count = 2

Third call:
  count is still 2 → count++ → count = 3
```

**Use Cases:**

1. **Counting function calls**
2. **Maintaining state between calls**
3. **One-time initialization**

```cpp
void initialize() {
    static bool initialized = false;
    if (!initialized) {
        cout << "Initializing..." << endl;
        initialized = true;
    }
    cout << "Running..." << endl;
}

initialize();  // "Initializing..." then "Running..."
initialize();  // Only "Running..."
initialize();  // Only "Running..."
```

**Static in Classes:**

```cpp
class Student {
    static int totalStudents;  // Shared by ALL objects
public:
    Student() { totalStudents++; }
    static int getCount() { return totalStudents; }
};
int Student::totalStudents = 0;  // Must initialize outside class

Student s1, s2, s3;
cout << Student::getCount();  // Output: 3
```

---

### 4. External (`extern`)

**Declares a variable that is defined in another file.**

**File1.cpp:**

```cpp
int globalVar = 100;  // Definition (memory allocated here)
```

**File2.cpp:**

```cpp
extern int globalVar;  // Declaration (no memory, just tells compiler it exists)

void function() {
    cout << globalVar;  // Uses the variable from File1.cpp
}
```

| Property      | Value                 |
| ------------- | --------------------- |
| Storage       | RAM (Data segment)    |
| Scope         | Global (across files) |
| Lifetime      | Entire program        |
| Default value | 0                     |

**Key Points:**

- `extern` only **declares**, doesn't **define**
- Actual definition must exist somewhere
- Used to share variables between multiple files

**Common Mistake:**

```cpp
extern int x = 10;  // This is a DEFINITION (has initializer)
extern int x;       // This is a DECLARATION (no initializer)
```

---

### 5. Mutable (`mutable`)

**Allows modifying a member even in a const object/function.**

```cpp
class Student {
    string name;
    mutable int accessCount;  // Can be modified even in const context

public:
    Student(string n) : name(n), accessCount(0) {}

    string getName() const {
        accessCount++;  // OK! Because it's mutable
        return name;
    }

    int getAccessCount() const {
        return accessCount;
    }
};

int main() {
    const Student s("John");  // const object
    cout << s.getName();      // accessCount becomes 1
    cout << s.getName();      // accessCount becomes 2
    cout << s.getAccessCount();  // Output: 2
}
```

| Property      | Value           |
| ------------- | --------------- |
| Storage       | RAM             |
| Scope         | Class member    |
| Lifetime      | Object lifetime |
| Default value | -               |

**Use Cases:**

- Caching/memoization
- Access counters
- Mutex locks in const functions

---

### Comparison Table:

| Storage Class | Keyword    | Scope  | Lifetime | Default | Use Case                     |
| ------------- | ---------- | ------ | -------- | ------- | ---------------------------- |
| Automatic     | `auto`     | Local  | Function | Garbage | Regular local variables      |
| Register      | `register` | Local  | Function | Garbage | Fast access (loop counters)  |
| Static        | `static`   | Local  | Program  | 0       | Preserve value between calls |
| External      | `extern`   | Global | Program  | 0       | Share across files           |
| Mutable       | `mutable`  | Class  | Object   | -       | Modify in const context      |

---

### Visual Memory Layout:

```
+------------------+
|      STACK       |  ← auto, register variables
|   (Local vars)   |
+------------------+
|       HEAP       |  ← dynamic memory (new/delete)
+------------------+
|   DATA SEGMENT   |  ← static, extern variables
|  (Global/Static) |
+------------------+
|      CODE        |  ← Program instructions
+------------------+
```

---

### Quick Tips for Exams:

1. **Static** = Value survives function calls, initialized to 0
2. **Extern** = Variable defined elsewhere, just declaring here
3. **Auto** = Default for local variables
4. **Register** = Hint for faster access (rarely used now)
5. **Mutable** = Can change even in const objects

---

> **Memory trick:**
>
> - **S**tatic = **S**tays (value persists)
> - **E**xtern = **E**lsewhere (defined in another file)

---
