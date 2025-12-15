# OOP Theory Questions with Answers (Unit-Wise)

> Complete questions and answers for exam preparation

---

# UNIT 1: C++ Basics & OOP Principles

## Q1. What is Object-Oriented Programming? List its four main principles.

**Answer:**
Object-Oriented Programming (OOP) is a programming paradigm that organizes software design around objects rather than functions and logic. An object is a data field that has unique attributes and behavior.

**Four Main Principles:**

1. **Encapsulation** - Binding data and methods together, hiding internal details
2. **Abstraction** - Showing only essential features, hiding complexity
3. **Inheritance** - Creating new classes from existing ones (code reusability)
4. **Polymorphism** - Same interface, different implementations ("many forms")

---

## Q2. Differentiate between procedural programming and object-oriented programming.

**Answer:**

| Aspect     | Procedural Programming | Object-Oriented Programming    |
| ---------- | ---------------------- | ------------------------------ |
| Approach   | Top-down               | Bottom-up                      |
| Focus      | Functions/Procedures   | Objects and Classes            |
| Data       | Data is exposed        | Data is hidden (encapsulation) |
| Code Reuse | Limited                | High (through inheritance)     |
| Security   | Less secure            | More secure                    |
| Examples   | C, Pascal              | C++, Java, Python              |

---

## Q3. What are the different data types available in C++?

**Answer:**

**1. Primitive/Built-in Types:**

- `int` - Integer numbers (4 bytes)
- `float` - Single precision decimal (4 bytes)
- `double` - Double precision decimal (8 bytes)
- `char` - Single character (1 byte)
- `bool` - True/False (1 byte)
- `void` - No value

**2. Derived Types:**

- Arrays
- Pointers
- References
- Functions

**3. User-Defined Types:**

- Class
- Structure
- Union
- Enum

---

## Q4. Explain the difference between `const` and `#define`.

**Answer:**

| Aspect        | const                        | #define                         |
| ------------- | ---------------------------- | ------------------------------- |
| Type          | Keyword (variable qualifier) | Preprocessor directive          |
| Syntax        | `const int MAX = 100;`       | `#define MAX 100`               |
| Type checking | Yes                          | No                              |
| Scope         | Block scope                  | Global (from definition to end) |
| Memory        | Allocates memory             | No memory allocation            |
| Debugging     | Easier (has name)            | Harder (replaced by value)      |

---

## Q5. What is type conversion? Differentiate between implicit and explicit conversion.

**Answer:**

**Type Conversion:** Converting a value from one data type to another.

**Implicit Conversion (Automatic):**

- Done automatically by compiler
- Happens when types are compatible
- Smaller type → Larger type (no data loss)

```cpp
int a = 5;
double b = a;  // int automatically converted to double
```

**Explicit Conversion (Type Casting):**

- Done manually by programmer
- Required when automatic conversion may cause data loss

```cpp
double x = 3.14;
int y = (int)x;           // C-style cast
int z = static_cast<int>(x);  // C++ style cast
```

---

## Q6. What is a pointer? How is it declared and initialized?

**Answer:**

**Pointer:** A variable that stores the memory address of another variable.

**Declaration:**

```cpp
datatype *pointer_name;
int *ptr;      // Pointer to integer
char *cptr;    // Pointer to character
```

**Initialization:**

```cpp
int x = 10;
int *ptr = &x;   // ptr stores address of x

// Accessing
cout << ptr;     // Prints address of x
cout << *ptr;    // Prints value at address (10) - dereferencing
```

**Key Operators:**

- `&` - Address-of operator (gets address)
- `*` - Dereference operator (gets value at address)

---

## Q7. Differentiate between an array and a pointer.

**Answer:**

| Aspect       | Array                               | Pointer                          |
| ------------ | ----------------------------------- | -------------------------------- |
| Definition   | Collection of elements of same type | Variable storing memory address  |
| Memory       | Fixed size, contiguous allocation   | Stores single address            |
| Size         | Fixed at declaration                | Can point to different locations |
| `sizeof`     | Returns total array size            | Returns pointer size (4/8 bytes) |
| Reassignment | Cannot be reassigned                | Can be reassigned                |

```cpp
int arr[5] = {1,2,3,4,5};  // Array - fixed
int *ptr = arr;             // Pointer - can change
ptr = &arr[2];             // Reassigned
```

---

## Q8. What is a reference variable? How is it different from a pointer?

**Answer:**

**Reference Variable:** An alias (another name) for an existing variable.

```cpp
int x = 10;
int &ref = x;   // ref is alias for x
ref = 20;       // x is now 20
```

| Aspect         | Reference                        | Pointer                         |
| -------------- | -------------------------------- | ------------------------------- |
| Syntax         | `int &ref = x;`                  | `int *ptr = &x;`                |
| Initialization | Must be initialized              | Can be uninitialized            |
| NULL           | Cannot be NULL                   | Can be NULL                     |
| Reassignment   | Cannot refer to another variable | Can point to different variable |
| Memory         | No separate memory               | Has its own memory              |
| Dereferencing  | Not needed                       | Use `*` to access value         |

---

## Q9. Explain the different storage classes in C++.

**Answer:**

| Storage Class | Keyword    | Scope       | Lifetime           | Default Value |
| ------------- | ---------- | ----------- | ------------------ | ------------- |
| Automatic     | `auto`     | Local/Block | Function execution | Garbage       |
| Register      | `register` | Local/Block | Function execution | Garbage       |
| Static        | `static`   | Local/Block | Entire program     | 0             |
| External      | `extern`   | Global      | Entire program     | 0             |
| Mutable       | `mutable`  | Class       | Object lifetime    | -             |

**Static Example:**

```cpp
void counter() {
    static int count = 0;  // Initialized only once
    count++;
    cout << count << endl;
}
// Calling counter() 3 times prints: 1, 2, 3
```

---

## Q10. What is dynamic memory allocation? Explain `new` and `delete`.

**Answer:**

**Dynamic Memory Allocation:** Allocating memory at runtime from the heap.

**`new` operator:** Allocates memory

```cpp
int *ptr = new int;        // Single variable
int *arr = new int[10];    // Array of 10 integers
```

**`delete` operator:** Deallocates memory

```cpp
delete ptr;      // For single variable
delete[] arr;    // For array
```

**Why Important:**

- Prevents memory leaks
- Efficient memory usage
- Flexible array sizes

---

## Q11. Explain call by value, call by reference, and call by pointer.

**Answer:**

**1. Call by Value:**

- Copy of argument is passed
- Original value NOT modified

```cpp
void increment(int x) {
    x++;  // Only local copy changes
}
int a = 5;
increment(a);  // a is still 5
```

**2. Call by Reference:**

- Reference (alias) is passed
- Original value IS modified

```cpp
void increment(int &x) {
    x++;  // Original changes
}
int a = 5;
increment(a);  // a is now 6
```

**3. Call by Pointer:**

- Address is passed
- Original value IS modified

```cpp
void increment(int *x) {
    (*x)++;  // Value at address changes
}
int a = 5;
increment(&a);  // a is now 6
```

---

# UNIT 2: Classes, Objects & OOP Features

## Q1. What is a class? How is it different from a structure in C++?

**Answer:**

**Class:** A user-defined blueprint or template that defines the properties (data members) and behaviors (member functions) of objects.

```cpp
class Student {
private:
    int roll;
public:
    void display() { }
};
```

| Aspect         | Structure                  | Class                         |
| -------------- | -------------------------- | ----------------------------- |
| Default access | public                     | private                       |
| Keyword        | `struct`                   | `class`                       |
| Purpose        | Group related data         | Data + behavior, OOP concepts |
| Inheritance    | Supported (default public) | Supported (default private)   |

---

## Q2. What are access specifiers? Explain public, private, and protected.

**Answer:**

**Access Specifiers:** Keywords that define the accessibility of class members.

| Specifier   | Within Class | Derived Class | Outside Class |
| ----------- | ------------ | ------------- | ------------- |
| `public`    | ✓            | ✓             | ✓             |
| `protected` | ✓            | ✓             | ✗             |
| `private`   | ✓            | ✗             | ✗             |

```cpp
class Example {
private:
    int a;      // Only accessible within class
protected:
    int b;      // Accessible in class and derived classes
public:
    int c;      // Accessible everywhere
};
```

---

## Q3. What is encapsulation? Why is it important?

**Answer:**

**Encapsulation:** The bundling of data (attributes) and methods (functions) that operate on the data into a single unit (class), while restricting direct access to some components.

**Implementation:**

```cpp
class BankAccount {
private:
    double balance;  // Hidden data
public:
    double getBalance() { return balance; }
    void deposit(double amt) {
        if (amt > 0) balance += amt;
    }
};
```

**Benefits:**

1. Data protection/security
2. Control over data (validation in setters)
3. Flexibility to change internal implementation
4. Reduced complexity
5. Easier maintenance

---

## Q4. What is a constructor? List its characteristics.

**Answer:**

**Constructor:** A special member function that is automatically called when an object is created. Used to initialize objects.

**Characteristics:**

1. Same name as class
2. No return type (not even void)
3. Called automatically on object creation
4. Can be overloaded
5. Can have default arguments
6. Cannot be virtual
7. Cannot be inherited (but called in inheritance)

```cpp
class Student {
public:
    Student() {  // Constructor
        cout << "Object created";
    }
};
Student s;  // Constructor called automatically
```

---

## Q5. Explain the types of constructors with examples.

**Answer:**

**1. Default Constructor:**

```cpp
class Student {
public:
    Student() {
        cout << "Default constructor";
    }
};
Student s;  // Calls default constructor
```

**2. Parameterized Constructor:**

```cpp
class Student {
    int roll;
public:
    Student(int r) {
        roll = r;
    }
};
Student s(101);  // Passes 101 to constructor
```

**3. Copy Constructor:**

```cpp
class Student {
    int roll;
public:
    Student(const Student &s) {
        roll = s.roll;
    }
};
Student s1(101);
Student s2 = s1;  // Copy constructor called
```

---

## Q6. What is a destructor? When is it called?

**Answer:**

**Destructor:** A special member function that is automatically called when an object is destroyed. Used to release resources.

**Characteristics:**

- Same name as class with `~` prefix
- No return type, no parameters
- Cannot be overloaded
- Called automatically when object goes out of scope

```cpp
class Student {
public:
    ~Student() {
        cout << "Destructor called";
    }
};
```

**When Called:**

1. Object goes out of scope
2. `delete` is used for dynamically allocated object
3. Program ends

---

## Q7. Differentiate between shallow copy and deep copy.

**Answer:**

**Shallow Copy:**

- Copies only member values
- For pointers, copies address (both point to same memory)
- Default copy constructor behavior
- Problem: Double deletion, dangling pointers

**Deep Copy:**

- Creates new memory for pointers
- Copies actual data, not just addresses
- Safe for dynamic memory(

```cpp
class String {
    char *str;
public:
    // Deep copy constructor
    String(const String &s) {
        str = new char[strlen(s.str) + 1];  // New memory
        strcpy(str, s.str);                  // Copy content
    }
};
```

---

## Q8. What is the `this` pointer? Explain its uses.

**Answer:**

**`this` Pointer:** An implicit pointer available in every non-static member function that points to the object for which the function is called.

**Uses:**

**1. Resolve naming conflicts:**

```cpp
class Student {
    int roll;
public:
    void setRoll(int roll) {
        this->roll = roll;  // this->roll is member, roll is parameter
    }
};
```

**2. Return current object:**

```cpp
Student& setName(string n) {
    name = n;
    return *this;  // Return current object
}
```

**3. Method chaining:**

```cpp
obj.setName("John").setRoll(101).display();
```

---

## Q9. What is a virtual function? Why do we need it?

**Answer:**

**Virtual Function:** A member function declared in base class with `virtual` keyword that can be overridden in derived classes, enabling runtime polymorphism.

```cpp
class Base {
public:
    virtual void show() {
        cout << "Base";
    }
};

class Derived : public Base {
public:
    void show() override {
        cout << "Derived";
    }
};

Base *ptr = new Derived();
ptr->show();  // Output: "Derived" (runtime decision)
```

**Why Needed:**

- Without virtual, base class version is called (early binding)
- With virtual, derived class version is called (late binding)
- Enables polymorphic behavior

---

## Q10. What is an abstract class? What is a pure virtual function?

**Answer:**

**Pure Virtual Function:** A virtual function with no implementation, declared with `= 0`.

```cpp
virtual void draw() = 0;
```

**Abstract Class:** A class that has at least one pure virtual function.

- Cannot create objects of abstract class
- Used as base class/interface
- Derived classes must implement all pure virtual functions

```cpp
class Shape {  // Abstract class
public:
    virtual double area() = 0;  // Pure virtual
};

class Circle : public Shape {
public:
    double area() override {  // Must implement
        return 3.14 * r * r;
    }
};

// Shape s;  // ERROR: Cannot instantiate abstract class
Circle c;    // OK
```

---

# UNIT 3: Polymorphism & Operator Overloading

## Q1. What is polymorphism? Explain its types.

**Answer:**

**Polymorphism:** "Poly" = many, "morph" = forms. Ability of objects to take many forms. Same interface, different implementations.

**Types:**

**1. Compile-Time (Static) Polymorphism:**

- Resolved at compile time
- Achieved through:
  - Function Overloading
  - Operator Overloading
- Also called early binding

**2. Run-Time (Dynamic) Polymorphism:**

- Resolved at runtime
- Achieved through:
  - Virtual Functions
  - Function Overriding
- Also called late binding

---

## Q2. What is function overloading? What are its rules?

**Answer:**

**Function Overloading:** Having multiple functions with the same name but different parameters in the same scope.

```cpp
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
int add(int a, int b, int c) { return a + b + c; }
```

**Rules:**

1. Functions must have same name
2. Must differ in:
   - Number of parameters, OR
   - Type of parameters, OR
   - Order of parameters
3. Return type alone is NOT sufficient
4. Should be in same scope

---

## Q3. Differentiate between function overloading and function overriding.

**Answer:**

| Aspect      | Overloading                     | Overriding                    |
| ----------- | ------------------------------- | ----------------------------- |
| Definition  | Same name, different parameters | Same name AND same parameters |
| Where       | Same class                      | Base and derived classes      |
| Inheritance | Not required                    | Required                      |
| Binding     | Compile-time                    | Run-time (with virtual)       |
| Signature   | Must be different               | Must be same                  |
| Purpose     | Multiple versions of function   | Redefine base class behavior  |

---

## Q4. What is operator overloading? Which operators cannot be overloaded?

**Answer:**

**Operator Overloading:** Giving special meaning to existing operators for user-defined types.

**Syntax:**

```cpp
return_type operator symbol (parameters) {
    // implementation
}
```

**Operators that CANNOT be overloaded:**

1. `::` - Scope resolution
2. `.` - Member access
3. `.*` - Pointer to member access
4. `?:` - Ternary operator
5. `sizeof` - Size operator
6. `typeid` - Type identification

---

## Q5. Write the syntax for overloading unary and binary operators.

**Answer:**

**Unary Operator (e.g., -, ++, --):**

```cpp
class Complex {
public:
    Complex operator-() {  // Unary minus
        return Complex(-real, -imag);
    }

    Complex& operator++() {  // Prefix ++
        real++;
        return *this;
    }

    Complex operator++(int) {  // Postfix ++ (int is dummy)
        Complex temp = *this;
        real++;
        return temp;
    }
};
```

**Binary Operator (e.g., +, -, \*, ==):**

```cpp
class Complex {
public:
    Complex operator+(const Complex &c) {
        return Complex(real + c.real, imag + c.imag);
    }
};
```

---

## Q6. Explain the difference between member function and friend function for operator overloading.

**Answer:**

**As Member Function:**

```cpp
class Complex {
public:
    Complex operator+(Complex &c) {
        return Complex(real + c.real, imag + c.imag);
    }
};
// Usage: c3 = c1 + c2;  (c1.operator+(c2))
```

- Left operand must be object of class
- Takes n-1 parameters (one is implicit `this`)

**As Friend Function:**

```cpp
class Complex {
    friend Complex operator+(Complex &c1, Complex &c2);
};
Complex operator+(Complex &c1, Complex &c2) {
    return Complex(c1.real + c2.real, c1.imag + c2.imag);
}
// Usage: c3 = c1 + c2;  (operator+(c1, c2))
```

- Both operands are parameters
- Takes n parameters
- Useful when left operand is not class object (e.g., `5 + obj`)

---

## Q7. Explain the three types of data conversion in operator overloading.

**Answer:**

**1. Basic to Class Type:**

- Use constructor

```cpp
class Distance {
public:
    Distance(int feet) {  // Converts int to Distance
        this->feet = feet;
    }
};
Distance d = 10;  // int converted to Distance
```

**2. Class to Basic Type:**

- Use conversion operator

```cpp
class Distance {
public:
    operator int() {  // Converts Distance to int
        return feet;
    }
};
Distance d(10);
int x = d;  // Distance converted to int
```

**3. Class to Class Type:**

- Use conversion operator or constructor in target class

```cpp
class Meters {
public:
    operator Feet();  // Meters to Feet
};
```

---

## Q8. What are the restrictions on operator overloading?

**Answer:**

1. **Cannot create new operators** - Only existing operators can be overloaded

2. **Cannot change:**

   - Number of operands
   - Precedence of operator
   - Associativity of operator

3. **Some operators cannot be overloaded:**

   - `::`, `.`, `.*`, `?:`, `sizeof`, `typeid`

4. **Some must be member functions:**

   - `=` (Assignment)
   - `[]` (Subscript)
   - `()` (Function call)
   - `->` (Member access)

5. **At least one operand must be user-defined type**

6. **Cannot overload for built-in types only**

---

# UNIT 4: Inheritance & Aggregation

## Q1. What is inheritance? What are its advantages?

**Answer:**

**Inheritance:** Mechanism by which a new class (derived/child) is created from an existing class (base/parent), inheriting its properties and behaviors.

```cpp
class Derived : public Base {
    // Derived class inherits from Base
};
```

**Advantages:**

1. **Code Reusability** - Use existing code without rewriting
2. **Extensibility** - Add new features to existing class
3. **Hierarchical Organization** - Model real-world relationships
4. **Polymorphism** - Enable runtime behavior switching
5. **Maintenance** - Changes in base class reflect in derived classes

---

## Q2. Explain the types of inheritance with diagrams.

**Answer:**

**1. Single Inheritance:**

```
    A
    |
    B
```

One base class, one derived class.

**2. Multilevel Inheritance:**

```
    A
    |
    B
    |
    C
```

Chain of inheritance (grandparent → parent → child).

**3. Multiple Inheritance:**

```
   A    B
    \  /
     C
```

One class inherits from multiple base classes.

**4. Hierarchical Inheritance:**

```
      A
    / | \
   B  C  D
```

Multiple classes inherit from one base class.

**5. Hybrid Inheritance:**
Combination of two or more types.

---

## Q3. Explain the visibility modes in inheritance.

**Answer:**

| Base Member | public inheritance | protected inheritance | private inheritance |
| ----------- | ------------------ | --------------------- | ------------------- |
| public      | public             | protected             | private             |
| protected   | protected          | protected             | private             |
| private     | Not accessible     | Not accessible        | Not accessible      |

```cpp
class Derived : public Base { };     // Most common
class Derived : protected Base { };
class Derived : private Base { };
```

**Note:** Private members are never directly accessible in derived class (use public methods of base class).

---

## Q4. What is the diamond problem? How is it solved?

**Answer:**

**Diamond Problem:** Ambiguity in multiple inheritance when a class inherits from two classes that have a common base class.

```
       A
      / \
     B   C
      \ /
       D
```

**Problem:**

```cpp
class A { public: int data; };
class B : public A { };
class C : public A { };
class D : public B, public C { };

D obj;
obj.data;  // ERROR: Ambiguous! Two copies of A::data
```

**Solution: Virtual Inheritance**

```cpp
class B : virtual public A { };
class C : virtual public A { };
class D : public B, public C { };

D obj;
obj.data;  // OK: Only one copy of A::data
```

---

## Q5. Explain the order of constructor and destructor calls in inheritance.

**Answer:**

**Constructor Order:** Base → Derived (bottom-up construction)
**Destructor Order:** Derived → Base (top-down destruction)

```cpp
class A {
public:
    A() { cout << "A constructor\n"; }
    ~A() { cout << "A destructor\n"; }
};

class B : public A {
public:
    B() { cout << "B constructor\n"; }
    ~B() { cout << "B destructor\n"; }
};

class C : public B {
public:
    C() { cout << "C constructor\n"; }
    ~C() { cout << "C destructor\n"; }
};

C obj;
// Output:
// A constructor
// B constructor
// C constructor
// C destructor
// B destructor
// A destructor
```

---

## Q6. How do you pass arguments to base class constructor from derived class?

**Answer:**

Use **initialization list** in derived class constructor:

```cpp
class Base {
protected:
    int x;
public:
    Base(int a) : x(a) { }
};

class Derived : public Base {
    int y;
public:
    // Call base constructor in initialization list
    Derived(int a, int b) : Base(a), y(b) { }
};

Derived d(10, 20);  // Base(10) called, then y = 20
```

---

## Q7. What is function overriding? How do you call base class function from derived class?

**Answer:**

**Function Overriding:** Redefining a base class function in derived class with same name and signature.

```cpp
class Base {
public:
    void show() { cout << "Base"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived"; }
};

Derived d;
d.show();  // Output: "Derived"
```

**Calling Base Class Function:**

```cpp
class Derived : public Base {
public:
    void show() {
        Base::show();  // Call base class version
        cout << " and Derived";
    }
};
```

---

## Q8. Differentiate between inheritance and aggregation.

**Answer:**

| Aspect         | Inheritance       | Aggregation         |
| -------------- | ----------------- | ------------------- |
| Relationship   | IS-A              | HAS-A               |
| Example        | Dog IS-A Animal   | Car HAS-A Engine    |
| Implementation | Class derivation  | Object as member    |
| Coupling       | Tight (strong)    | Loose (weak)        |
| Code Reuse     | Through extension | Through composition |

```cpp
// Inheritance (IS-A)
class Dog : public Animal { };

// Aggregation (HAS-A)
class Car {
    Engine engine;  // Car HAS-A Engine
};
```

---

## Q9. Differentiate between composition and aggregation.

**Answer:**

| Aspect       | Composition          | Aggregation                |
| ------------ | -------------------- | -------------------------- |
| Relationship | Strong HAS-A         | Weak HAS-A                 |
| Lifetime     | Part dies with whole | Part exists independently  |
| Ownership    | Whole owns part      | Whole uses part            |
| Memory       | Object as member     | Pointer to external object |

```cpp
// Composition - Engine dies with Car
class Car {
    Engine engine;  // Engine created inside Car
};

// Aggregation - Driver exists independently
class Car {
    Driver *driver;  // Pointer to external Driver
};
```

---

# UNIT 5: STL Templates & Libraries

## Q1. What is a template? Why are templates used?

**Answer:**

**Template:** A feature that allows writing generic code that works with any data type. The compiler generates specific code for each type used.

**Why Used:**

1. **Code Reusability** - Write once, use with any type
2. **Type Safety** - Compile-time type checking
3. **Performance** - No runtime overhead (code generated at compile time)
4. **Generic Programming** - Same algorithm for different types

**Types:**

1. Function Templates
2. Class Templates

---

## Q2. Explain function templates with syntax and example.

**Answer:**

**Function Template:** A blueprint for creating functions that work with any data type.

**Syntax:**

```cpp
template <typename T>
T functionName(T param) {
    // code
}
```

**Example:**

```cpp
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// Usage
cout << maximum(5, 10);       // int version
cout << maximum(3.14, 2.78);  // double version
cout << maximum('A', 'Z');    // char version
```

The compiler generates separate functions for each type used.

---

## Q3. Explain class templates with syntax and example.

**Answer:**

**Class Template:** A blueprint for creating classes that work with any data type.

**Syntax:**

```cpp
template <class T>
class ClassName {
    T member;
public:
    void setMember(T val);
    T getMember();
};
```

**Example:**

```cpp
template <class T>
class Stack {
    T arr[100];
    int top;
public:
    void push(T x) { arr[++top] = x; }
    T pop() { return arr[top--]; }
};

// Usage
Stack<int> intStack;
Stack<string> strStack;
Stack<double> dblStack;
```

---

## Q4. What is STL? Explain its components.

**Answer:**

**STL (Standard Template Library):** A collection of template classes and functions providing general-purpose classes and functions with templates.

**Three Main Components:**

**1. Containers:**

- Store collections of objects
- Examples: vector, list, map, set, stack, queue

**2. Iterators:**

- Objects that point to container elements
- Used to traverse containers
- Types: input, output, forward, bidirectional, random access

**3. Algorithms:**

- Functions that perform operations on containers
- Examples: sort(), find(), count(), reverse()

```cpp
vector<int> v = {5, 2, 8, 1};
sort(v.begin(), v.end());  // Algorithms use iterators
```

---

## Q5. Explain vector and its operations.

**Answer:**

**Vector:** A dynamic array that can grow or shrink in size.

```cpp
#include <vector>

// Declaration
vector<int> v;
vector<int> v(5);      // 5 elements
vector<int> v(5, 10);  // 5 elements, all = 10
vector<int> v = {1, 2, 3};

// Operations
v.push_back(10);   // Add at end
v.pop_back();      // Remove from end
v.size();          // Number of elements
v.empty();         // Check if empty
v[0];              // Access element (no bounds check)
v.at(0);           // Access element (bounds check)
v.front();         // First element
v.back();          // Last element
v.clear();         // Remove all
v.insert(pos, val);// Insert at position
v.erase(pos);      // Erase at position
```

---

## Q6. Explain map and set containers.

**Answer:**

**Map:** Stores key-value pairs, sorted by key, unique keys.

```cpp
#include <map>

map<string, int> m;
m["apple"] = 5;           // Insert
m.insert({"banana", 3});
cout << m["apple"];       // Access

// Iterate
for (auto &p : m) {
    cout << p.first << ": " << p.second;
}

// Find
if (m.find("apple") != m.end()) {
    cout << "Found";
}
```

**Set:** Stores unique elements, automatically sorted.

```cpp
#include <set>

set<int> s;
s.insert(5);
s.insert(3);
s.insert(5);  // Duplicate ignored

// s contains: {3, 5}

// Find
if (s.find(3) != s.end()) {
    cout << "Found";
}
```

---

## Q7. Explain iterators and their types.

**Answer:**

**Iterator:** An object that points to an element in a container, used to traverse containers.

**Types:**

| Type          | Capabilities                | Containers           |
| ------------- | --------------------------- | -------------------- |
| Input         | Read, forward only          | istream              |
| Output        | Write, forward only         | ostream              |
| Forward       | Read/write, forward only    | forward_list         |
| Bidirectional | Read/write, both directions | list, set, map       |
| Random Access | Read/write, any position    | vector, deque, array |

**Usage:**

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Traditional
for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}

// Using auto
for (auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}

// Range-based (C++11)
for (int x : v) {
    cout << x << " ";
}
```

---

## Q8. Explain common STL algorithms.

**Answer:**

```cpp
#include <algorithm>
#include <vector>

vector<int> v = {5, 2, 8, 1, 9};

// sort - Sort elements
sort(v.begin(), v.end());           // Ascending
sort(v.begin(), v.end(), greater<int>());  // Descending

// find - Find element
auto it = find(v.begin(), v.end(), 5);
if (it != v.end()) cout << "Found at " << (it - v.begin());

// count - Count occurrences
int c = count(v.begin(), v.end(), 5);

// reverse - Reverse elements
reverse(v.begin(), v.end());

// min_element / max_element
auto minIt = min_element(v.begin(), v.end());
auto maxIt = max_element(v.begin(), v.end());

// binary_search - Check if exists (sorted container)
bool found = binary_search(v.begin(), v.end(), 5);

// accumulate - Sum
#include <numeric>
int sum = accumulate(v.begin(), v.end(), 0);
```

---

## Q9. Differentiate between vector and list.

**Answer:**

| Aspect                 | Vector             | List               |
| ---------------------- | ------------------ | ------------------ |
| Implementation         | Dynamic array      | Doubly linked list |
| Access                 | Random access O(1) | Sequential O(n)    |
| Insert/Delete (middle) | Slow O(n)          | Fast O(1)          |
| Insert/Delete (end)    | Fast O(1)          | Fast O(1)          |
| Memory                 | Contiguous         | Non-contiguous     |
| Cache performance      | Better             | Worse              |
| Iterator               | Random access      | Bidirectional      |

**Use Vector when:** Random access needed, mostly adding at end
**Use List when:** Frequent insertions/deletions in middle

---

## Q10. Differentiate between stack and queue.

**Answer:**

| Aspect  | Stack                     | Queue                     |
| ------- | ------------------------- | ------------------------- |
| Order   | LIFO (Last In First Out)  | FIFO (First In First Out) |
| Add     | push() - at top           | push() - at back          |
| Remove  | pop() - from top          | pop() - from front        |
| Access  | top()                     | front(), back()           |
| Example | Undo operation, recursion | Print queue, BFS          |

```cpp
// Stack
stack<int> s;
s.push(10);     // Add at top
s.top();        // Access top
s.pop();        // Remove from top

// Queue
queue<int> q;
q.push(10);     // Add at back
q.front();      // Access front
q.pop();        // Remove from front
```

---

# Quick Reference Tables

## Access Specifiers

| Specifier | Class | Derived | Outside |
| --------- | ----- | ------- | ------- |
| public    | ✓     | ✓       | ✓       |
| protected | ✓     | ✓       | ✗       |
| private   | ✓     | ✗       | ✗       |

## Polymorphism Types

| Type         | Binding | Achieved By       |
| ------------ | ------- | ----------------- |
| Compile-time | Early   | Overloading       |
| Run-time     | Late    | Virtual functions |

## Constructor Types

| Type          | Parameters     | When Called                     |
| ------------- | -------------- | ------------------------------- |
| Default       | None           | Object created without args     |
| Parameterized | Has params     | Object created with args        |
| Copy          | Same class ref | Object initialized with another |

## Inheritance Types

| Type         | Structure   | Example                   |
| ------------ | ----------- | ------------------------- |
| Single       | A → B       | Animal → Dog              |
| Multilevel   | A → B → C   | Animal → Mammal → Dog     |
| Multiple     | A,B → C     | Father, Mother → Child    |
| Hierarchical | A → B,C,D   | Shape → Circle, Rectangle |
| Hybrid       | Combination | Multiple + Hierarchical   |

---

> **Good Luck with your exam!**
