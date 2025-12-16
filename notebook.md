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

---

## Question 3: Explain Dynamic Memory Management

**Asked on:** 2025-12-16

### What is Dynamic Memory Management?

**Dynamic Memory** = Memory allocated at **runtime** (while program is running) from the **heap**.

**Static Memory** (regular variables) = Size fixed at **compile time**, stored on **stack**.

```
Why do we need it?
- When we don't know the size of array beforehand
- When we need memory to persist beyond function scope
- When we need large amounts of memory
```

---

### Stack vs Heap Memory

```
+------------------+
|      STACK       |  ← Automatic allocation
|   (Local vars)   |  ← Fast, but limited size
|   int x = 10;    |  ← Automatically freed
+------------------+
|       HEAP       |  ← Manual allocation (new/delete)
|  (Dynamic mem)   |  ← Larger, but slower
|  int *p = new int|  ← Must be freed manually
+------------------+
```

| Aspect       | Stack            | Heap            |
| ------------ | ---------------- | --------------- |
| Allocation   | Automatic        | Manual (new)    |
| Deallocation | Automatic        | Manual (delete) |
| Size         | Limited (few MB) | Large (GBs)     |
| Speed        | Fast             | Slower          |
| Lifetime     | Function scope   | Until deleted   |

---

### The `new` Operator

Allocates memory on the heap and returns a pointer to it.

**Syntax:**

```cpp
pointer = new datatype;           // Single variable
pointer = new datatype[size];     // Array
```

**Examples:**

```cpp
// Single variable
int *ptr = new int;       // Allocate space for 1 integer
*ptr = 10;                // Store value

// With initialization
int *ptr = new int(25);   // Allocate and initialize to 25

// Array
int *arr = new int[5];    // Allocate array of 5 integers
arr[0] = 10;
arr[1] = 20;

// Dynamic 2D array
int **matrix = new int*[3];       // 3 rows
for (int i = 0; i < 3; i++) {
    matrix[i] = new int[4];       // 4 columns each
}
```

---

### The `delete` Operator

Frees memory that was allocated with `new`.

**Syntax:**

```cpp
delete pointer;       // Single variable
delete[] pointer;     // Array
```

**Examples:**

```cpp
// Single variable
int *ptr = new int(10);
cout << *ptr;         // Use it
delete ptr;           // Free it
ptr = nullptr;        // Good practice: set to null after delete

// Array
int *arr = new int[5];
// ... use array ...
delete[] arr;         // Use delete[] for arrays!
arr = nullptr;

// 2D array
for (int i = 0; i < 3; i++) {
    delete[] matrix[i];   // Delete each row
}
delete[] matrix;          // Delete the array of pointers
```

---

### Common Mistakes and Problems

#### 1. Memory Leak

Forgetting to delete allocated memory.

```cpp
void leak() {
    int *ptr = new int(10);
    // Forgot to delete!
}   // ptr goes out of scope, but memory is still allocated

// This is a MEMORY LEAK - memory is occupied but inaccessible
```

#### 2. Dangling Pointer

Using a pointer after the memory has been deleted.

```cpp
int *ptr = new int(10);
delete ptr;
cout << *ptr;   // DANGER! Dangling pointer - undefined behavior
```

**Solution:**

```cpp
int *ptr = new int(10);
delete ptr;
ptr = nullptr;  // Set to null after delete
if (ptr != nullptr) {
    cout << *ptr;  // Now we can check before using
}
```

#### 3. Double Delete

Deleting the same memory twice.

```cpp
int *ptr = new int(10);
delete ptr;
delete ptr;   // CRASH! Double delete
```

**Solution:**

```cpp
delete ptr;
ptr = nullptr;  // Set to null
delete ptr;     // delete nullptr is safe (does nothing)
```

#### 4. Using delete instead of delete[]

```cpp
int *arr = new int[10];
delete arr;     // WRONG! Should be delete[]
delete[] arr;   // CORRECT
```

---

### Memory Allocation Diagram

```
int *ptr = new int(42);

Step 1: new int(42)
        +--------+
  HEAP: |   42   |  ← Memory allocated at address 0x1000
        +--------+

Step 2: ptr = ...
        +--------+
 STACK: |  0x1000|  ← ptr stores the address
        +--------+

After delete ptr:
        +--------+
  HEAP: |  ????  |  ← Memory freed (available for reuse)
        +--------+
```

---

### Dynamic Arrays vs Static Arrays

```cpp
// Static array - size must be known at compile time
int arr[100];               // OK
int n = 10;
int arr2[n];                // ERROR in standard C++ (VLA not allowed)

// Dynamic array - size can be determined at runtime
int n;
cin >> n;
int *arr = new int[n];      // OK! Size determined at runtime
// ... use array ...
delete[] arr;
```

---

### Dynamic Objects

```cpp
class Student {
public:
    string name;
    Student(string n) : name(n) {
        cout << "Constructor: " << name << endl;
    }
    ~Student() {
        cout << "Destructor: " << name << endl;
    }
};

int main() {
    // Dynamic object
    Student *s = new Student("John");
    cout << s->name << endl;   // Use arrow operator for pointers
    delete s;                   // Destructor called here

    // Dynamic array of objects
    Student *students = new Student[3] {
        Student("A"), Student("B"), Student("C")
    };
    delete[] students;  // All 3 destructors called

    return 0;
}
```

---

### new vs malloc (C vs C++)

| Aspect       | new (C++)         | malloc (C)                  |
| ------------ | ----------------- | --------------------------- |
| Syntax       | `new int`         | `(int*)malloc(sizeof(int))` |
| Returns      | Typed pointer     | `void*` (needs cast)        |
| Constructor  | Calls constructor | Doesn't call                |
| Failure      | Throws exception  | Returns NULL                |
| Deallocation | `delete`          | `free()`                    |
| Type-safe    | Yes               | No                          |

**Always use new/delete in C++, not malloc/free!**

---

### Best Practices

1. **Always delete what you new**

   ```cpp
   int *p = new int;
   // ... use p ...
   delete p;
   ```

2. **Set pointer to nullptr after delete**

   ```cpp
   delete p;
   p = nullptr;
   ```

3. **Use delete[] for arrays**

   ```cpp
   int *arr = new int[10];
   delete[] arr;  // Not delete arr
   ```

4. **Check for nullptr before using**

   ```cpp
   if (ptr != nullptr) {
       *ptr = 10;
   }
   ```

5. **Use smart pointers (C++11+) when possible**
   ```cpp
   #include <memory>
   unique_ptr<int> ptr = make_unique<int>(10);
   // Automatically deleted when out of scope!
   ```

---

### Quick Summary Table

| Operation  | Single Variable | Array          |
| ---------- | --------------- | -------------- |
| Allocate   | `new int`       | `new int[n]`   |
| Initialize | `new int(10)`   | -              |
| Access     | `*ptr`          | `ptr[i]`       |
| Deallocate | `delete ptr`    | `delete[] ptr` |

---

### Memory Lifecycle

```
1. ALLOCATE    →    int *p = new int;
                          ↓
2. USE         →    *p = 10; cout << *p;
                          ↓
3. DEALLOCATE  →    delete p;
                          ↓
4. NULLIFY     →    p = nullptr;
```

---

> **Remember:**
>
> - `new` allocates memory from HEAP
> - `delete` frees memory back to HEAP
> - Always match: `new` ↔ `delete`, `new[]` ↔ `delete[]`
> - Memory leaks = allocated but never freed = bad!

---

## Question 4: Explain Polymorphism - Types and Use-Cases

**Asked on:** 2025-12-16

### What is Polymorphism?

**Polymorphism** (meaning "many forms") is one of the four pillars of OOP. It allows objects to be treated as instances of their parent class while executing behavior specific to their actual type.

---

### Types of Polymorphism

```
                    POLYMORPHISM
                         |
         +---------------+---------------+
         |                               |
   COMPILE-TIME                     RUN-TIME
   (Static)                         (Dynamic)
         |                               |
   +-----+-----+                   +-----+-----+
   |           |                   |           |
Function   Operator            Function    Virtual
Overloading Overloading       Overriding  Functions
```

---

## 1. Compile-Time (Static) Polymorphism

This is resolved **during compilation** — the compiler knows exactly which function to call based on the function signature.

### **Function Overloading**

Multiple functions with the **same name** but **different parameters**.

```cpp
#include <iostream>
using namespace std;

void print(int x) {
    cout << "Integer: " << x << endl;
}

void print(double x) {
    cout << "Double: " << x << endl;
}

void print(string x) {
    cout << "String: " << x << endl;
}

int main() {
    print(5);           // Calls print(int)
    print(3.14);        // Calls print(double)
    print("Hello");     // Calls print(string)
    return 0;
}
```

**Output:**

```
Integer: 5
Double: 3.14
String: Hello
```

> **Why static?** The compiler sees `print(5)` and immediately knows to call `print(int)` based on the argument type.

**Rules for Function Overloading:**

1. Functions must have the **same name**
2. Functions must have **different parameter lists** (number, type, or order)
3. Return type alone is NOT enough to overload

```cpp
// VALID overloading
void func(int a);
void func(double a);
void func(int a, int b);

// INVALID - only return type differs
int func(int a);
double func(int a);  // ERROR!
```

---

### **Operator Overloading**

Redefining how operators work for user-defined types.

```cpp
#include <iostream>
using namespace std;

class Complex {
public:
    double real, imag;

    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // Overloading the + operator
    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }

    // Overloading the - operator
    Complex operator-(const Complex& other) {
        return Complex(real - other.real, imag - other.imag);
    }

    // Overloading << for output
    friend ostream& operator<<(ostream& out, const Complex& c) {
        out << c.real << " + " << c.imag << "i";
        return out;
    }
};

int main() {
    Complex c1(3, 4), c2(1, 2);
    Complex c3 = c1 + c2;  // Uses overloaded + operator
    Complex c4 = c1 - c2;  // Uses overloaded - operator

    cout << "c1 = " << c1 << endl;
    cout << "c2 = " << c2 << endl;
    cout << "c1 + c2 = " << c3 << endl;
    cout << "c1 - c2 = " << c4 << endl;

    return 0;
}
```

**Output:**

```
c1 = 3 + 4i
c2 = 1 + 2i
c1 + c2 = 4 + 6i
c1 - c2 = 2 + 2i
```

> **Why static?** The compiler knows at compile time that `c1 + c2` should call `Complex::operator+()`.

**Operators that CAN be overloaded:**

```
+  -  *  /  %  ^  &  |  ~  !  =  <  >  +=  -=  *=  /=  %=
^=  &=  |=  <<  >>  <<=  >>=  ==  !=  <=  >=  &&  ||  ++
--  ->*  ,  ->  []  ()  new  delete  new[]  delete[]
```

**Operators that CANNOT be overloaded:**

```
::  .  .*  ?:  sizeof
```

---

## 2. Run-Time (Dynamic) Polymorphism

This is resolved **during execution** — the actual function to call is determined at runtime based on the object's actual type.

### **Virtual Functions & Function Overriding**

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void speak() {  // Virtual function
        cout << "Animal speaks" << endl;
    }

    virtual ~Animal() {}  // Virtual destructor (important!)
};

class Dog : public Animal {
public:
    void speak() override {  // Override base class function
        cout << "Dog barks: Woof!" << endl;
    }
};

class Cat : public Animal {
public:
    void speak() override {
        cout << "Cat meows: Meow!" << endl;
    }
};

class Cow : public Animal {
public:
    void speak() override {
        cout << "Cow moos: Moo!" << endl;
    }
};

int main() {
    Animal* ptr;           // Base class pointer

    Dog dog;
    Cat cat;
    Cow cow;

    ptr = &dog;
    ptr->speak();          // Output: Dog barks: Woof!

    ptr = &cat;
    ptr->speak();          // Output: Cat meows: Meow!

    ptr = &cow;
    ptr->speak();          // Output: Cow moos: Moo!

    return 0;
}
```

> **Why dynamic?** The pointer `ptr` is of type `Animal*`, but the actual object it points to determines which `speak()` is called. This decision happens **at runtime**.

---

### How Virtual Functions Work (vtable)

When you use `virtual`, the compiler creates a **virtual table (vtable)**:

```
+------------------+
|     Animal       |
+------------------+
| vtable pointer --|---> [speak() -> Animal::speak]
+------------------+

+------------------+
|       Dog        |
+------------------+
| vtable pointer --|---> [speak() -> Dog::speak]
+------------------+

+------------------+
|       Cat        |
+------------------+
| vtable pointer --|---> [speak() -> Cat::speak]
+------------------+
```

When `ptr->speak()` is called:

1. Go to the object's vtable
2. Look up the function address
3. Call that function

This lookup happens at **runtime**, hence "dynamic" polymorphism.

---

### Without `virtual` Keyword (Static Binding)

```cpp
class Animal {
public:
    void speak() {  // NOT virtual
        cout << "Animal speaks" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() {
        cout << "Dog barks" << endl;
    }
};

int main() {
    Animal* ptr = new Dog();
    ptr->speak();  // Output: Animal speaks (NOT Dog barks!)
    delete ptr;
}
```

Without `virtual`, the compiler uses the **pointer type** to decide which function to call, not the actual object type.

---

### Pure Virtual Functions & Abstract Classes

A **pure virtual function** has no implementation in the base class:

```cpp
class Shape {
public:
    virtual double area() = 0;  // Pure virtual function
    virtual void draw() = 0;    // Pure virtual function

    virtual ~Shape() {}
};

class Circle : public Shape {
    double radius;
public:
    Circle(double r) : radius(r) {}

    double area() override {
        return 3.14159 * radius * radius;
    }

    void draw() override {
        cout << "Drawing Circle" << endl;
    }
};

class Rectangle : public Shape {
    double width, height;
public:
    Rectangle(double w, double h) : width(w), height(h) {}

    double area() override {
        return width * height;
    }

    void draw() override {
        cout << "Drawing Rectangle" << endl;
    }
};

int main() {
    // Shape s;  // ERROR! Cannot instantiate abstract class

    Shape* shapes[2];
    shapes[0] = new Circle(5);
    shapes[1] = new Rectangle(4, 6);

    for (int i = 0; i < 2; i++) {
        shapes[i]->draw();
        cout << "Area: " << shapes[i]->area() << endl;
    }

    // Clean up
    delete shapes[0];
    delete shapes[1];

    return 0;
}
```

**Output:**

```
Drawing Circle
Area: 78.5398
Drawing Rectangle
Area: 24
```

---

### Comparison Table

| Aspect          | Compile-Time                  | Run-Time                          |
| --------------- | ----------------------------- | --------------------------------- |
| **Resolution**  | At compilation                | At execution                      |
| **Mechanism**   | Function/Operator Overloading | Virtual Functions + Overriding    |
| **Keyword**     | None required                 | `virtual`, `override`             |
| **Speed**       | Faster (no runtime overhead)  | Slightly slower (vtable lookup)   |
| **Flexibility** | Less flexible                 | More flexible (true polymorphism) |
| **Binding**     | Early/Static binding          | Late/Dynamic binding              |

---

### Key Differences: Overloading vs Overriding

| Aspect      | Overloading                     | Overriding                    |
| ----------- | ------------------------------- | ----------------------------- |
| Definition  | Same name, different parameters | Same name, same parameters    |
| Scope       | Same class                      | Base and derived classes      |
| Binding     | Compile-time                    | Run-time                      |
| Inheritance | Not required                    | Required                      |
| virtual     | Not required                    | Required for dynamic behavior |
| Return type | Can be different                | Should be same (or covariant) |

---

### Practical Use-Cases

**1. Function Overloading:**

```cpp
// Different ways to print data
void print(int x);
void print(string s);
void print(double d);

// Different ways to find max
int max(int a, int b);
double max(double a, double b);
int max(int a, int b, int c);
```

**2. Operator Overloading:**

```cpp
// String concatenation
String s1 = "Hello";
String s2 = " World";
String s3 = s1 + s2;  // "Hello World"

// Matrix addition
Matrix m3 = m1 + m2;

// Comparing objects
if (date1 < date2) { ... }
```

**3. Virtual Functions:**

```cpp
// GUI Framework
class Widget {
public:
    virtual void draw() = 0;
    virtual void onClick() = 0;
};

class Button : public Widget { ... };
class TextBox : public Widget { ... };
class CheckBox : public Widget { ... };

// All widgets can be stored in one container
vector<Widget*> widgets;
for (Widget* w : widgets) {
    w->draw();  // Each draws itself correctly
}
```

---

### Key Points to Remember

1. **`virtual` keyword** — Tells the compiler to use dynamic binding
2. **`override` keyword** — (C++11) Ensures you're actually overriding a base class function
3. **`= 0`** — Makes a function pure virtual (abstract)
4. **vtable** — Virtual table used internally for dynamic dispatch
5. **Base class pointer** — Essential for runtime polymorphism to work
6. **Virtual destructor** — Always use when you have virtual functions

---

### Common Interview Questions

**Q: What happens if we don't use virtual destructor?**

```cpp
class Base {
public:
    ~Base() { cout << "Base destructor" << endl; }  // Non-virtual
};

class Derived : public Base {
    int* data;
public:
    Derived() { data = new int[100]; }
    ~Derived() {
        delete[] data;  // This won't be called!
        cout << "Derived destructor" << endl;
    }
};

Base* ptr = new Derived();
delete ptr;  // Only Base destructor called - MEMORY LEAK!
```

**Solution:** Always use `virtual ~Base() {}` when using polymorphism.

---

> **Memory Tricks:**
>
> - **Overloading** = Same name, different signature, same class
> - **Overriding** = Same name, same signature, different class
> - **Virtual** = "Let the actual object decide"
> - **Pure virtual (= 0)** = "Derived classes MUST implement this"

---
