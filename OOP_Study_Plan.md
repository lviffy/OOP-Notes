# Complete OOP in C++ Study Plan (8 Hours)

> **Goal**: Master Object-Oriented Programming fundamentals for your college exam

---

## Time Allocation Overview

| Unit      | Topic                               | Time      | Priority |
| --------- | ----------------------------------- | --------- | -------- |
| 1         | C++ Basics & OOP Principles         | 1.5 hrs   | Critical |
| 2         | Classes, Objects & OOP Features     | 1.5 hrs   | Critical |
| 3         | Polymorphism & Operator Overloading | 1.5 hrs   | Critical |
| 4         | Inheritance & Aggregation           | 1.5 hrs   | Critical |
| 5         | STL Templates & Libraries           | 2 hrs     | Critical |
| **Total** |                                     | **8 hrs** |          |

---

# UNIT 1: C++ Basics & OOP Principles (2 Hours)

## 1.1 Understanding Object-Oriented World View

### Topics:

- [ ] **Agents and Communities** - Objects interact like agents in a community
- [ ] **Messages and Methods** - Objects communicate through messages (function calls)
- [ ] **Responsibilities** - Each object has specific duties
- [ ] **Classes and Objects** - Blueprint vs Instance

### The 4 Principles of OOP:

| Principle         | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| **Encapsulation** | Binding data and methods together, hiding internal details |
| **Abstraction**   | Showing only essential features, hiding complexity         |
| **Inheritance**   | Creating new classes from existing ones                    |
| **Polymorphism**  | Same interface, different implementations                  |

---

## 1.2 Overview of C++ and Basic Program Structure

### Topics:

- [ ] **Data Types**

  - Primitive: `int`, `float`, `double`, `char`, `bool`
  - Derived: arrays, pointers, references
  - User-defined: struct, class, enum

- [ ] **Variables and Constants**

  ```cpp
  int x = 10;           // Variable
  const int MAX = 100;  // Constant
  #define PI 3.14       // Macro constant
  ```

- [ ] **Type Conversion**

  ```cpp
  // Implicit conversion
  int a = 5;
  double b = a;  // int to double automatically

  // Explicit conversion (casting)
  double x = 3.14;
  int y = (int)x;        // C-style cast
  int z = static_cast<int>(x);  // C++ style cast
  ```

- [ ] **Operators**
  - Arithmetic: `+`, `-`, `*`, `/`, `%`
  - Relational: `==`, `!=`, `<`, `>`, `<=`, `>=`
  - Logical: `&&`, `||`, `!`
  - Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
  - Assignment: `=`, `+=`, `-=`, etc.

---

## 1.3 Decision-Making and Looping Constructs

### Decision Making:

```cpp
// if-else
if (condition) { } else { }

// switch
switch(x) {
    case 1: break;
    case 2: break;
    default: break;
}

// Ternary operator
result = (condition) ? value1 : value2;
```

### Loops:

```cpp
// for loop
for (int i = 0; i < n; i++) { }

// while loop
while (condition) { }

// do-while loop
do { } while (condition);
```

---

## 1.4 Arrays, Strings, and Pointers

### Arrays:

```cpp
int arr[5] = {1, 2, 3, 4, 5};   // 1D array
int matrix[3][3];               // 2D array
```

### Strings:

```cpp
// C-style string
char str[] = "Hello";

// C++ string
#include <string>
string s = "Hello";
s.length();      // Get length
s + " World";    // Concatenation
s[0];            // Access character
```

### Pointers:

```cpp
int x = 10;
int *ptr = &x;   // Pointer stores address

cout << ptr;     // Address of x
cout << *ptr;    // Value at address (10)

// Pointer arithmetic
ptr++;           // Move to next int address
```

---

## 1.5 Functions, Passing Arguments, Returning Values

### Function Declaration:

```cpp
return_type function_name(parameters) {
    // body
    return value;
}
```

### Passing Arguments:

**1. Pass by Value** (copy is made):

```cpp
void modify(int x) {
    x = 100;  // Original NOT affected
}
```

**2. Pass by Reference** (original affected):

```cpp
void modify(int &x) {
    x = 100;  // Original IS affected
}
```

**3. Pass by Pointer**:

```cpp
void modify(int *x) {
    *x = 100;  // Original IS affected
}
```

### Reference Arguments (Reference Variables):

```cpp
int a = 5;
int &ref = a;   // ref is alias for a
ref = 10;       // a is now 10
```

---

## 1.6 Storage Classes

| Storage Class | Keyword    | Scope  | Lifetime | Default Value |
| ------------- | ---------- | ------ | -------- | ------------- |
| Automatic     | `auto`     | Local  | Function | Garbage       |
| Register      | `register` | Local  | Function | Garbage       |
| Static        | `static`   | Local  | Program  | 0             |
| External      | `extern`   | Global | Program  | 0             |
| Mutable       | `mutable`  | Class  | Object   | -             |

```cpp
void counter() {
    static int count = 0;  // Retains value between calls
    count++;
    cout << count;
}
```

---

## 1.7 Dynamic Memory Management in C++

### new and delete:

```cpp
// Single variable
int *ptr = new int;      // Allocate
*ptr = 10;
delete ptr;              // Deallocate

// Array
int *arr = new int[10];  // Allocate array
delete[] arr;            // Deallocate array
```

### Key Points:

- `new` returns pointer, throws exception if fails
- Always `delete` what you `new` (prevent memory leak)
- Use `delete[]` for arrays

---

# UNIT 2: Classes, Objects & OOP Features (2 Hours)

## 2.1 Concept of Classes and Objects

### Class Definition:

```cpp
class Student {
private:
    int roll;        // Data member
    string name;

public:
    void setData(int r, string n) {  // Member function
        roll = r;
        name = n;
    }

    void display() {
        cout << roll << " " << name;
    }
};
```

### Creating Objects:

```cpp
Student s1;              // Stack allocation
Student *s2 = new Student();  // Heap allocation

s1.setData(1, "John");   // Using dot operator
s2->setData(2, "Jane");  // Using arrow operator
```

### Real-World Example:

- **Class**: Car (blueprint)
- **Object**: Your specific Honda Civic (instance)
- **Attributes**: color, model, speed
- **Methods**: accelerate(), brake(), turn()

---

## 2.2 Encapsulation and Data Hiding

### Access Modifiers:

| Modifier    | Within Class | Derived Class | Outside |
| ----------- | ------------ | ------------- | ------- |
| `private`   | Yes          | No            | No      |
| `protected` | Yes          | Yes           | No      |
| `public`    | Yes          | Yes           | Yes     |

### Data Hiding with Getters/Setters:

```cpp
class BankAccount {
private:
    double balance;  // Hidden from outside

public:
    // Getter
    double getBalance() {
        return balance;
    }

    // Setter with validation
    void deposit(double amount) {
        if (amount > 0)
            balance += amount;
    }
};
```

---

## 2.3 Polymorphism - Types and Use-Cases

### Types:

**1. Compile-Time (Static) Polymorphism**:

- Function Overloading
- Operator Overloading
- Resolved during compilation

**2. Run-Time (Dynamic) Polymorphism**:

- Function Overriding
- Virtual Functions
- Resolved during execution

### Practical Use-Cases:

- **Function Overloading**: `print(int)`, `print(string)`, `print(double)`
- **Operator Overloading**: Adding two complex numbers with `+`
- **Virtual Functions**: Base class pointer calling derived class method

---

## 2.4 Method Overloading vs Method Overriding

| Feature     | Overloading                     | Overriding              |
| ----------- | ------------------------------- | ----------------------- |
| Definition  | Same name, different parameters | Same name AND signature |
| Where       | Same class                      | Base and derived class  |
| Binding     | Compile-time                    | Run-time                |
| Inheritance | Not required                    | Required                |

### Overloading Example:

```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
};
```

### Overriding Example:

```cpp
class Base {
public:
    void show() { cout << "Base"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived"; }  // Overrides Base::show()
};
```

---

## 2.5 Virtual Functions

### Purpose:

- Enable runtime polymorphism
- Base class pointer can call derived class method

### Syntax:

```cpp
class Base {
public:
    virtual void display() {
        cout << "Base class";
    }
};

class Derived : public Base {
public:
    void display() override {
        cout << "Derived class";
    }
};

// Usage
Base *ptr = new Derived();
ptr->display();  // Output: "Derived class"
```

### Virtual Destructor:

```cpp
class Base {
public:
    virtual ~Base() { }  // Important for proper cleanup
};
```

---

## 2.6 Interfaces (Abstract Classes)

### Pure Virtual Function:

```cpp
virtual void show() = 0;  // No implementation
```

### Abstract Class (Interface):

```cpp
class Shape {  // Cannot create objects of this class
public:
    virtual double area() = 0;      // Pure virtual
    virtual double perimeter() = 0; // Pure virtual
};

class Circle : public Shape {
    double radius;
public:
    double area() override {
        return 3.14 * radius * radius;
    }
    double perimeter() override {
        return 2 * 3.14 * radius;
    }
};
```

---

## 2.7 Constructors and Destructors

### Types of Constructors:

**1. Default Constructor**:

```cpp
class Student {
public:
    Student() {
        cout << "Default constructor";
    }
};
```

**2. Parameterized Constructor**:

```cpp
class Student {
    int roll;
public:
    Student(int r) {
        roll = r;
    }
};
```

**3. Copy Constructor**:

```cpp
class Student {
    int roll;
public:
    Student(const Student &s) {
        roll = s.roll;
    }
};
```

### Constructor Initialization List:

```cpp
Student(int r, string n) : roll(r), name(n) { }
```

### Destructor:

```cpp
class Student {
public:
    ~Student() {
        cout << "Destructor called";
        // Release resources here
    }
};
```

### Order of Calls:

- **Constructors**: Base → Derived
- **Destructors**: Derived → Base

---

## 2.8 Methods, Method Calling, Method with Object Parameters

### Defining Methods:

**Inside class (inline)**:

```cpp
class Demo {
public:
    void show() { cout << "Hello"; }
};
```

**Outside class**:

```cpp
class Demo {
public:
    void show();
};

void Demo::show() {
    cout << "Hello";
}
```

### Method Calling:

```cpp
Demo obj;
obj.show();       // Using object

Demo *ptr = &obj;
ptr->show();      // Using pointer
```

### Method with Object Parameters:

```cpp
class Distance {
    int feet;
public:
    void add(Distance d1, Distance d2) {
        feet = d1.feet + d2.feet;
    }

    bool isEqual(Distance d) {
        return feet == d.feet;
    }
};
```

---

# UNIT 3: Polymorphism & Operator Overloading (2 Hours)

## 3.1 Concept of Polymorphism

### Definition:

- "Poly" = Many, "Morph" = Forms
- Same interface, different implementations
- Allows flexibility and extensibility

### Types Recap:

| Type         | When Resolved      | Achieved By                   |
| ------------ | ------------------ | ----------------------------- |
| Compile-time | During compilation | Function/Operator Overloading |
| Run-time     | During execution   | Virtual Functions             |

---

## 3.2 Function Overloading and Its Advantages

### Rules for Overloading:

1. Same function name
2. Different number OR types of parameters
3. Return type alone is NOT sufficient

### Examples:

```cpp
// Different number of parameters
int sum(int a, int b) { return a + b; }
int sum(int a, int b, int c) { return a + b + c; }

// Different types of parameters
void print(int x) { cout << "Integer: " << x; }
void print(double x) { cout << "Double: " << x; }
void print(string x) { cout << "String: " << x; }
```

### Advantages:

1. Code readability
2. Code reusability
3. Logical grouping of similar operations
4. Flexibility in calling

---

## 3.3 Common Problems in Function Overloading

### 1. Ambiguity with Default Arguments:

```cpp
void func(int a, int b = 10) { }
void func(int a) { }  // Ambiguous!

func(5);  // Which one to call?
```

### 2. Type Conversion Ambiguity:

```cpp
void func(int x) { }
void func(double x) { }

func(5.5f);  // float - can convert to both!
```

### 3. Reference vs Value:

```cpp
void func(int x) { }
void func(int &x) { }  // Cannot distinguish at call

int a = 5;
func(a);  // Ambiguous!
```

---

## 3.4 Operator Overloading

### Syntax:

```cpp
return_type operator symbol (parameters) {
    // implementation
}
```

### Can be Overloaded:

`+`, `-`, `*`, `/`, `%`, `++`, `--`, `==`, `!=`, `<`, `>`, `<<`, `>>`, `=`, `[]`, `()`, `->`, etc.

### Cannot be Overloaded:

- `::` (Scope resolution)
- `.` (Member access)
- `.*` (Pointer to member)
- `?:` (Ternary)
- `sizeof`
- `typeid`

---

## 3.5 Overloading Unary Operators

### Unary operators: `++`, `--`, `-`, `!`, `~`

### Example - Overloading `-` (negation):

```cpp
class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) { }

    Complex operator - () {  // Unary minus
        return Complex(-real, -imag);
    }
};

// Usage
Complex c1(3, 4);
Complex c2 = -c1;  // c2 = (-3, -4)
```

### Overloading `++` (prefix and postfix):

```cpp
class Counter {
    int count;
public:
    // Prefix ++
    Counter& operator ++ () {
        count++;
        return *this;
    }

    // Postfix ++ (int is dummy parameter)
    Counter operator ++ (int) {
        Counter temp = *this;
        count++;
        return temp;
    }
};
```

---

## 3.6 Overloading Binary Operators

### Binary operators: `+`, `-`, `*`, `/`, `==`, `<`, etc.

### Example - Overloading `+`:

```cpp
class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) { }

    // As member function
    Complex operator + (const Complex &c) {
        return Complex(real + c.real, imag + c.imag);
    }
};

// Usage
Complex c1(3, 4), c2(1, 2);
Complex c3 = c1 + c2;  // c3 = (4, 6)
```

### As Friend Function:

```cpp
class Complex {
    int real, imag;
public:
    friend Complex operator + (const Complex &c1, const Complex &c2);
};

Complex operator + (const Complex &c1, const Complex &c2) {
    return Complex(c1.real + c2.real, c1.imag + c2.imag);
}
```

---

## 3.7 Data Conversion

### Three Types:

**1. Basic to Class**:

```cpp
class Distance {
    int feet;
public:
    Distance(int f) : feet(f) { }  // Constructor handles conversion
};

Distance d = 10;  // int converted to Distance
```

**2. Class to Basic**:

```cpp
class Distance {
    int feet;
public:
    operator int() {  // Conversion operator
        return feet;
    }
};

Distance d(10);
int x = d;  // Distance converted to int
```

**3. Class to Class**:

```cpp
class Meters {
    double m;
public:
    operator Feet();  // Conversion to Feet class
};
```

---

## 3.8 Problems in Operator Overloading and Type Conversions

### 1. Ambiguity in Conversion:

```cpp
class A {
public:
    operator B();  // A can convert to B
};

class B {
public:
    B(A a);  // B can be constructed from A
};

// Both provide A → B conversion - ambiguous!
```

### 2. Cannot Change Operator Behavior:

- Cannot change precedence
- Cannot change associativity
- Cannot create new operators

### 3. At Least One Operand Must Be User-Defined:

```cpp
// INVALID - cannot overload for built-in types
int operator + (int a, int b);
```

### 4. Some Operators Have Restrictions:

- `=`, `[]`, `()`, `->` must be member functions
- `<<`, `>>` typically friend functions

---

# UNIT 4: Inheritance & Aggregation (2 Hours)

## 4.1 Inheritance - Definition and Applications

### Definition:

- Creating new class (derived) from existing class (base)
- Derived class inherits properties and behaviors
- "IS-A" relationship

### Applications:

- Code reusability
- Extensibility
- Modeling real-world hierarchies
- Framework development

### Basic Syntax:

```cpp
class Derived : access_specifier Base {
    // Additional members
};
```

---

## 4.2 Derived and Base Classes

### Base Class (Parent/Super):

```cpp
class Animal {
protected:
    string name;
public:
    void eat() { cout << "Eating"; }
};
```

### Derived Class (Child/Sub):

```cpp
class Dog : public Animal {
public:
    void bark() { cout << "Barking"; }
    void display() { cout << name; }  // Can access protected
};
```

### What is Inherited:

| Member      | Can be Inherited?                      |
| ----------- | -------------------------------------- |
| public      | Yes                                    |
| protected   | Yes                                    |
| private     | No (but accessible via public methods) |
| Constructor | No (but called automatically)          |
| Destructor  | No (but called automatically)          |

---

## 4.3 Derived Class Constructor, Overriding Member Functions

### Derived Class Constructor:

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
    // Call base constructor explicitly
    Derived(int a, int b) : Base(a), y(b) { }
};
```

### Overriding Member Functions:

```cpp
class Base {
public:
    void show() { cout << "Base"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived"; }  // Overrides Base::show()

    void callBaseShow() {
        Base::show();  // Explicit call to base version
    }
};
```

---

## 4.4 Inheritance Example - English Distance Class

```cpp
class Distance {
protected:
    int feet;
    float inches;
public:
    Distance() : feet(0), inches(0.0) { }
    Distance(int f, float i) : feet(f), inches(i) { }

    void showDist() {
        cout << feet << "'" << inches << "\"";
    }
};

class DistSign : public Distance {
    char sign;  // '+' or '-'
public:
    DistSign() : Distance(), sign('+') { }
    DistSign(int f, float i, char s) : Distance(f, i), sign(s) { }

    void showDist() {
        cout << sign;
        Distance::showDist();  // Call base method
    }
};
```

---

## 4.5 Class Hierarchies

### Single Inheritance:

```
     Animal
        |
       Dog
```

### Multilevel Inheritance:

```
     Animal
        |
     Mammal
        |
       Dog
```

### Hierarchical Inheritance:

```
        Animal
       /   |   \
     Dog  Cat  Bird
```

### Example:

```cpp
// Multilevel
class Animal {
public:
    void eat() { cout << "Eating"; }
};

class Mammal : public Animal {
public:
    void breathe() { cout << "Breathing"; }
};

class Dog : public Mammal {
public:
    void bark() { cout << "Barking"; }
};

// Dog can use eat(), breathe(), bark()
```

---

## 4.6 Inheritance and Graphics Shapes

```cpp
class Shape {
protected:
    int x, y;  // Position
public:
    virtual void draw() = 0;      // Pure virtual
    virtual double area() = 0;
};

class Circle : public Shape {
    double radius;
public:
    void draw() override {
        cout << "Drawing circle at " << x << "," << y;
    }
    double area() override {
        return 3.14 * radius * radius;
    }
};

class Rectangle : public Shape {
    double width, height;
public:
    void draw() override {
        cout << "Drawing rectangle at " << x << "," << y;
    }
    double area() override {
        return width * height;
    }
};
```

---

## 4.7 Public and Private Inheritance, Levels of Inheritance

### Visibility Modes:

| Base Member | public inheritance | protected inheritance | private inheritance |
| ----------- | ------------------ | --------------------- | ------------------- |
| public      | public             | protected             | private             |
| protected   | protected          | protected             | private             |
| private     | Not accessible     | Not accessible        | Not accessible      |

### Examples:

```cpp
class Base {
public:
    int pub;
protected:
    int prot;
private:
    int priv;
};

// Public inheritance - most common
class D1 : public Base {
    // pub → public, prot → protected
};

// Protected inheritance
class D2 : protected Base {
    // pub → protected, prot → protected
};

// Private inheritance
class D3 : private Base {
    // pub → private, prot → private
};
```

### Levels of Inheritance:

- **Single Level**: A → B
- **Two Level**: A → B → C
- **Three Level**: A → B → C → D
- And so on...

---

## 4.8 Multiple Inheritance, Ambiguity in Multiple Inheritance

### Multiple Inheritance:

```cpp
class A {
public:
    void showA() { cout << "Class A"; }
};

class B {
public:
    void showB() { cout << "Class B"; }
};

class C : public A, public B {
public:
    void showC() { cout << "Class C"; }
};

// C has showA(), showB(), and showC()
```

### Ambiguity Problem:

```cpp
class A {
public:
    void show() { cout << "A"; }
};

class B {
public:
    void show() { cout << "B"; }
};

class C : public A, public B { };

C obj;
obj.show();  // ERROR: Ambiguous!

// Solution: Use scope resolution
obj.A::show();  // Calls A's show
obj.B::show();  // Calls B's show
```

### Diamond Problem:

```
       A
      / \
     B   C
      \ /
       D
```

```cpp
class A {
public:
    int data;
};

class B : public A { };
class C : public A { };
class D : public B, public C { };

D obj;
obj.data;  // ERROR: Ambiguous! (Two copies of A::data)

// Solution: Virtual Inheritance
class B : virtual public A { };
class C : virtual public A { };
class D : public B, public C { };  // Only one copy of A
```

---

## 4.9 Aggregation: Classes Within Classes

### Definition:

- "HAS-A" relationship (not "IS-A")
- One class contains objects of another class
- Two types: Composition and Aggregation

### Composition (Strong "HAS-A"):

- Part cannot exist without whole
- Lifetime dependent

```cpp
class Engine {
public:
    void start() { cout << "Engine started"; }
};

class Car {
    Engine engine;  // Engine is part of Car
public:
    void startCar() {
        engine.start();  // Using contained object
    }
};
// When Car is destroyed, Engine is also destroyed
```

### Aggregation (Weak "HAS-A"):

- Part can exist independently
- Lifetime independent

```cpp
class Driver {
public:
    string name;
};

class Car {
    Driver *driver;  // Pointer to external Driver
public:
    void setDriver(Driver *d) {
        driver = d;
    }
};
// Driver exists even if Car is destroyed
```

### Comparison:

| Feature      | Inheritance        | Aggregation         |
| ------------ | ------------------ | ------------------- |
| Relationship | IS-A               | HAS-A               |
| Example      | Dog IS-A Animal    | Car HAS-A Engine    |
| Code Reuse   | Through derivation | Through containment |
| Coupling     | Tight              | Loose               |

---

# UNIT 5: STL Templates & Libraries (2 Hours)

## 5.1 Introduction to Templates

### What are Templates?

- Generic programming feature
- Write code once, use with any data type
- Compiler generates specific versions

### Types:

1. Function Templates
2. Class Templates

---

## 5.2 Function Templates

### Syntax:

```cpp
template <typename T>
T functionName(T param) {
    // code
}
```

### Example:

```cpp
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// Usage - compiler deduces type
cout << maximum(5, 10);       // int version
cout << maximum(3.5, 2.1);    // double version
cout << maximum('a', 'z');    // char version

// Explicit type specification
cout << maximum<int>(5, 10);
```

### Multiple Template Parameters:

```cpp
template <typename T, typename U>
void display(T a, U b) {
    cout << a << " " << b;
}

display(5, "hello");  // T=int, U=string
```

---

## 5.3 Class Templates

### Syntax:

```cpp
template <class T>
class ClassName {
    T member;
public:
    void setMember(T val);
    T getMember();
};

// Member function definition outside class
template <class T>
void ClassName<T>::setMember(T val) {
    member = val;
}
```

### Example - Generic Stack:

```cpp
template <class T>
class Stack {
    T arr[100];
    int top;
public:
    Stack() : top(-1) { }

    void push(T x) {
        arr[++top] = x;
    }

    T pop() {
        return arr[top--];
    }

    bool isEmpty() {
        return top == -1;
    }
};

// Usage
Stack<int> intStack;
Stack<string> strStack;
Stack<double> dblStack;
```

---

## 5.4 STL Overview (Standard Template Library)

### Three Components:

| Component      | Description     | Examples                |
| -------------- | --------------- | ----------------------- |
| **Containers** | Store data      | vector, list, map, set  |
| **Iterators**  | Access elements | begin(), end()          |
| **Algorithms** | Process data    | sort(), find(), count() |

---

## 5.5 STL Containers

### 1. Vector (Dynamic Array):

```cpp
#include <vector>

vector<int> v;            // Empty vector
vector<int> v(5);         // 5 elements, default value
vector<int> v(5, 10);     // 5 elements, all = 10
vector<int> v = {1,2,3};  // Initialize with values

// Operations
v.push_back(10);    // Add at end
v.pop_back();       // Remove from end
v.size();           // Number of elements
v.empty();          // Check if empty
v[0];               // Access element
v.at(0);            // Access with bounds check
v.front();          // First element
v.back();           // Last element
v.clear();          // Remove all elements
```

### 2. List (Doubly Linked List):

```cpp
#include <list>

list<int> lst;
lst.push_back(10);   // Add at end
lst.push_front(5);   // Add at beginning
lst.pop_back();      // Remove from end
lst.pop_front();     // Remove from beginning
```

### 3. Stack (LIFO):

```cpp
#include <stack>

stack<int> s;
s.push(10);      // Add element
s.pop();         // Remove top
s.top();         // Access top element
s.empty();       // Check if empty
s.size();        // Number of elements
```

### 4. Queue (FIFO):

```cpp
#include <queue>

queue<int> q;
q.push(10);      // Add at back
q.pop();         // Remove from front
q.front();       // Access front element
q.back();        // Access back element
```

### 5. Map (Key-Value Pairs):

```cpp
#include <map>

map<string, int> m;
m["apple"] = 5;     // Insert
m["banana"] = 3;

cout << m["apple"];  // Access: 5

// Check if key exists
if (m.find("apple") != m.end()) {
    cout << "Found";
}

// Iterate
for (auto &p : m) {
    cout << p.first << ": " << p.second;
}
```

### 6. Set (Unique Elements, Sorted):

```cpp
#include <set>

set<int> s;
s.insert(5);
s.insert(3);
s.insert(5);  // Duplicate ignored

// s contains: {3, 5}
```

---

## 5.6 STL Iterators

### What are Iterators?

- Pointer-like objects
- Used to traverse containers

### Types:

| Type          | Movement                 | Example Containers |
| ------------- | ------------------------ | ------------------ |
| Input         | Forward only, read       | istream            |
| Output        | Forward only, write      | ostream            |
| Forward       | Forward only, read/write | forward_list       |
| Bidirectional | Both directions          | list, set, map     |
| Random Access | Any position             | vector, deque      |

### Usage:

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Using iterator
for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}

// Using auto (C++11)
for (auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}

// Range-based for loop (C++11)
for (int x : v) {
    cout << x << " ";
}
```

---

## 5.7 STL Algorithms

```cpp
#include <algorithm>

vector<int> v = {5, 2, 8, 1, 9};

// Sort
sort(v.begin(), v.end());        // Ascending: 1,2,5,8,9
sort(v.begin(), v.end(), greater<int>());  // Descending

// Find
auto it = find(v.begin(), v.end(), 5);
if (it != v.end()) {
    cout << "Found at index: " << (it - v.begin());
}

// Count
int c = count(v.begin(), v.end(), 5);

// Reverse
reverse(v.begin(), v.end());

// Min/Max element
auto minIt = min_element(v.begin(), v.end());
auto maxIt = max_element(v.begin(), v.end());

// Binary search (requires sorted container)
bool found = binary_search(v.begin(), v.end(), 5);

// Accumulate (sum)
#include <numeric>
int sum = accumulate(v.begin(), v.end(), 0);
```

---

## 5.8 Pair and Tuple

### Pair:

```cpp
#include <utility>

pair<int, string> p;
p.first = 1;
p.second = "hello";

// Or
pair<int, string> p = make_pair(1, "hello");
auto p2 = make_pair(2, "world");
```

### Tuple (C++11):

```cpp
#include <tuple>

tuple<int, string, double> t = make_tuple(1, "hello", 3.14);

cout << get<0>(t);  // 1
cout << get<1>(t);  // "hello"
cout << get<2>(t);  // 3.14
```

---

## 5.9 String Class (STL)

```cpp
#include <string>

string s = "Hello";

// Operations
s.length();           // 5
s.size();             // 5 (same as length)
s.empty();            // false
s[0];                 // 'H'
s.at(0);              // 'H' with bounds check

s + " World";         // Concatenation
s.append(" World");   // Append

s.substr(0, 3);       // "Hel" (position, length)
s.find("llo");        // 2 (position of substring)
s.compare("Hello");   // 0 if equal

s.insert(5, "!");     // Insert at position
s.erase(5, 1);        // Erase from position, count
s.replace(0, 5, "Hi"); // Replace

// Convert to C-string
const char* cstr = s.c_str();
```

---

# Quick Revision Checklist

## Unit 1 Key Points:

- [ ] 4 Principles of OOP
- [ ] Data types, variables, constants
- [ ] Pass by value vs reference vs pointer
- [ ] Storage classes (auto, static, extern, register)
- [ ] Dynamic memory (new, delete)

## Unit 2 Key Points:

- [ ] Class vs Object
- [ ] Access modifiers (public, private, protected)
- [ ] 3 types of constructors
- [ ] Virtual functions and abstract classes
- [ ] Method overloading vs overriding

## Unit 3 Key Points:

- [ ] Compile-time vs Run-time polymorphism
- [ ] Function overloading rules
- [ ] Operator overloading syntax
- [ ] Unary vs Binary operator overloading
- [ ] Data conversion (3 types)

## Unit 4 Key Points:

- [ ] 5 types of inheritance
- [ ] Visibility modes in inheritance
- [ ] Diamond problem and virtual inheritance
- [ ] Composition vs Aggregation

## Unit 5 Key Points:

- [ ] Function templates syntax
- [ ] Class templates syntax
- [ ] STL containers (vector, list, map, set, stack, queue)
- [ ] Iterators and their types
- [ ] Common algorithms (sort, find, count)

---

## Common Exam Questions:

1. Difference between structure and class
2. Types of constructors with examples
3. Types of inheritance with diagrams
4. Virtual functions and polymorphism
5. Operator overloading example (binary and unary)
6. Friend function vs Member function
7. Abstract class vs Concrete class
8. Diamond problem and its solution
9. Shallow copy vs Deep copy
10. Aggregation vs Composition
11. Function template vs Class template
12. STL containers and their operations

---

## Study Tips

1. **Practice Code**: Write each example yourself
2. **Draw Diagrams**: Especially for inheritance hierarchies
3. **Understand Syntax**: Memorize key syntax patterns
4. **Take Breaks**: 10 minutes every 50 minutes
5. **Revise**: Use checklist in last hour

---

> **Good Luck!** You've got this!
