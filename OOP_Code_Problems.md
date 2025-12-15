# OOP Code Problems with Solutions

> Practice these coding problems for your exam

---

# UNIT 1: C++ Basics & OOP Principles

## Problem 1.1: Swap Two Numbers Using Pointers

**Question:** Write a program to swap two numbers using pointers.

```cpp
#include <iostream>
using namespace std;

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 10, y = 20;

    cout << "Before swap: x = " << x << ", y = " << y << endl;
    swap(&x, &y);
    cout << "After swap: x = " << x << ", y = " << y << endl;

    return 0;
}
```

**Output:**

```
Before swap: x = 10, y = 20
After swap: x = 20, y = 10
```

---

## Problem 1.2: Call by Value vs Call by Reference

**Question:** Demonstrate the difference between call by value and call by reference.

```cpp
#include <iostream>
using namespace std;

// Call by Value
void incrementByValue(int x) {
    x++;
    cout << "Inside function (by value): " << x << endl;
}

// Call by Reference
void incrementByReference(int &x) {
    x++;
    cout << "Inside function (by reference): " << x << endl;
}

int main() {
    int a = 10, b = 10;

    cout << "Original a: " << a << endl;
    incrementByValue(a);
    cout << "After call by value, a: " << a << endl;

    cout << "\nOriginal b: " << b << endl;
    incrementByReference(b);
    cout << "After call by reference, b: " << b << endl;

    return 0;
}
```

**Output:**

```
Original a: 10
Inside function (by value): 11
After call by value, a: 10

Original b: 10
Inside function (by reference): 11
After call by reference, b: 11
```

---

## Problem 1.3: Dynamic Memory Allocation

**Question:** Create a dynamic array, input values, find sum and average, then deallocate memory.

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Enter number of elements: ";
    cin >> n;

    // Dynamic allocation
    int *arr = new int[n];

    // Input
    cout << "Enter " << n << " elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Calculate sum
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    cout << "Sum: " << sum << endl;
    cout << "Average: " << (float)sum / n << endl;

    // Deallocate memory
    delete[] arr;

    return 0;
}
```

---

## Problem 1.4: Static Variable Demo

**Question:** Demonstrate how static variables retain their value between function calls.

```cpp
#include <iostream>
using namespace std;

void counter() {
    static int count = 0;  // Initialized only once
    count++;
    cout << "Function called " << count << " times" << endl;
}

int main() {
    counter();  // count = 1
    counter();  // count = 2
    counter();  // count = 3
    counter();  // count = 4

    return 0;
}
```

**Output:**

```
Function called 1 times
Function called 2 times
Function called 3 times
Function called 4 times
```

---

# UNIT 2: Classes, Objects & OOP Features

## Problem 2.1: Basic Class with Constructor and Destructor

**Question:** Create a Student class with roll number and name. Implement constructor, destructor, and display function.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
private:
    int roll;
    string name;

public:
    // Default Constructor
    Student() {
        roll = 0;
        name = "Unknown";
        cout << "Default Constructor called" << endl;
    }

    // Parameterized Constructor
    Student(int r, string n) {
        roll = r;
        name = n;
        cout << "Parameterized Constructor called for " << name << endl;
    }

    // Destructor
    ~Student() {
        cout << "Destructor called for " << name << endl;
    }

    void display() {
        cout << "Roll: " << roll << ", Name: " << name << endl;
    }
};

int main() {
    Student s1;                      // Default constructor
    Student s2(101, "John");         // Parameterized constructor

    s1.display();
    s2.display();

    return 0;
}
```

---

## Problem 2.2: Copy Constructor and Deep Copy

**Question:** Implement a class with dynamic memory and demonstrate deep copy constructor.

```cpp
#include <iostream>
#include <cstring>
using namespace std;

class String {
private:
    char *str;
    int length;

public:
    // Constructor
    String(const char *s = "") {
        length = strlen(s);
        str = new char[length + 1];
        strcpy(str, s);
        cout << "Constructor: " << str << endl;
    }

    // Deep Copy Constructor
    String(const String &source) {
        length = source.length;
        str = new char[length + 1];  // Allocate new memory
        strcpy(str, source.str);     // Copy content
        cout << "Copy Constructor: " << str << endl;
    }

    // Destructor
    ~String() {
        cout << "Destructor: " << str << endl;
        delete[] str;
    }

    void display() {
        cout << "String: " << str << ", Length: " << length << endl;
    }

    void change(const char *s) {
        delete[] str;
        length = strlen(s);
        str = new char[length + 1];
        strcpy(str, s);
    }
};

int main() {
    String s1("Hello");
    String s2 = s1;  // Copy constructor called

    s1.display();
    s2.display();

    s1.change("World");  // Change s1

    cout << "\nAfter changing s1:" << endl;
    s1.display();  // s1 changed
    s2.display();  // s2 unchanged (deep copy)

    return 0;
}
```

---

## Problem 2.3: Encapsulation with Getter and Setter

**Question:** Create a BankAccount class demonstrating encapsulation with getter and setter methods.

```cpp
#include <iostream>
using namespace std;

class BankAccount {
private:
    string accountNumber;
    double balance;

public:
    // Constructor
    BankAccount(string accNo, double initialBalance) {
        accountNumber = accNo;
        if (initialBalance >= 0)
            balance = initialBalance;
        else
            balance = 0;
    }

    // Getter
    double getBalance() {
        return balance;
    }

    string getAccountNumber() {
        return accountNumber;
    }

    // Setter with validation
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "Deposited: " << amount << endl;
        } else {
            cout << "Invalid amount!" << endl;
        }
    }

    bool withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "Withdrawn: " << amount << endl;
            return true;
        } else {
            cout << "Insufficient balance or invalid amount!" << endl;
            return false;
        }
    }

    void display() {
        cout << "Account: " << accountNumber << ", Balance: $" << balance << endl;
    }
};

int main() {
    BankAccount acc("ACC001", 1000);

    acc.display();
    acc.deposit(500);
    acc.withdraw(200);
    acc.display();

    acc.withdraw(2000);  // Should fail

    return 0;
}
```

---

## Problem 2.4: Virtual Function and Runtime Polymorphism

**Question:** Demonstrate runtime polymorphism using virtual functions with a Shape class hierarchy.

```cpp
#include <iostream>
using namespace std;

class Shape {
public:
    virtual void draw() {
        cout << "Drawing a shape" << endl;
    }

    virtual double area() {
        return 0;
    }

    virtual ~Shape() { }  // Virtual destructor
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) { }

    void draw() override {
        cout << "Drawing a circle with radius " << radius << endl;
    }

    double area() override {
        return 3.14159 * radius * radius;
    }
};

class Rectangle : public Shape {
private:
    double width, height;

public:
    Rectangle(double w, double h) : width(w), height(h) { }

    void draw() override {
        cout << "Drawing a rectangle " << width << "x" << height << endl;
    }

    double area() override {
        return width * height;
    }
};

int main() {
    Shape *shapes[3];

    shapes[0] = new Circle(5);
    shapes[1] = new Rectangle(4, 6);
    shapes[2] = new Circle(3);

    // Polymorphic behavior
    for (int i = 0; i < 3; i++) {
        shapes[i]->draw();
        cout << "Area: " << shapes[i]->area() << endl << endl;
    }

    // Cleanup
    for (int i = 0; i < 3; i++) {
        delete shapes[i];
    }

    return 0;
}
```

---

## Problem 2.5: Abstract Class and Pure Virtual Function

**Question:** Create an abstract class Animal with pure virtual functions and implement in derived classes.

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Animal {
protected:
    string name;

public:
    Animal(string n) : name(n) { }

    // Pure virtual functions
    virtual void makeSound() = 0;
    virtual void move() = 0;

    void display() {
        cout << "Animal: " << name << endl;
    }

    virtual ~Animal() { }
};

class Dog : public Animal {
public:
    Dog(string n) : Animal(n) { }

    void makeSound() override {
        cout << name << " says: Woof! Woof!" << endl;
    }

    void move() override {
        cout << name << " runs on four legs" << endl;
    }
};

class Bird : public Animal {
public:
    Bird(string n) : Animal(n) { }

    void makeSound() override {
        cout << name << " says: Tweet! Tweet!" << endl;
    }

    void move() override {
        cout << name << " flies in the sky" << endl;
    }
};

int main() {
    // Animal a("Test");  // ERROR: Cannot instantiate abstract class

    Animal *animals[2];
    animals[0] = new Dog("Buddy");
    animals[1] = new Bird("Tweety");

    for (int i = 0; i < 2; i++) {
        animals[i]->display();
        animals[i]->makeSound();
        animals[i]->move();
        cout << endl;
    }

    delete animals[0];
    delete animals[1];

    return 0;
}
```

---

# UNIT 3: Polymorphism & Operator Overloading

## Problem 3.1: Function Overloading

**Question:** Demonstrate function overloading with an add() function that works with different types.

```cpp
#include <iostream>
using namespace std;

// Function overloading
int add(int a, int b) {
    cout << "Adding two integers: ";
    return a + b;
}

int add(int a, int b, int c) {
    cout << "Adding three integers: ";
    return a + b + c;
}

double add(double a, double b) {
    cout << "Adding two doubles: ";
    return a + b;
}

string add(string a, string b) {
    cout << "Concatenating strings: ";
    return a + b;
}

int main() {
    cout << add(5, 10) << endl;
    cout << add(5, 10, 15) << endl;
    cout << add(3.5, 2.5) << endl;
    cout << add("Hello ", "World") << endl;

    return 0;
}
```

**Output:**

```
Adding two integers: 15
Adding three integers: 30
Adding two doubles: 6
Concatenating strings: Hello World
```

---

## Problem 3.2: Unary Operator Overloading (Prefix and Postfix ++)

**Question:** Overload both prefix and postfix increment operators for a Counter class.

```cpp
#include <iostream>
using namespace std;

class Counter {
private:
    int count;

public:
    Counter(int c = 0) : count(c) { }

    // Prefix increment (++obj)
    Counter& operator++() {
        count++;
        return *this;
    }

    // Postfix increment (obj++)
    Counter operator++(int) {  // int is dummy parameter
        Counter temp = *this;
        count++;
        return temp;
    }

    void display() {
        cout << "Count: " << count << endl;
    }
};

int main() {
    Counter c1(5);

    cout << "Initial: ";
    c1.display();

    ++c1;  // Prefix
    cout << "After ++c1: ";
    c1.display();

    c1++;  // Postfix
    cout << "After c1++: ";
    c1.display();

    // Demonstrating difference
    Counter c2(10);
    Counter c3 = ++c2;  // c2 incremented, then assigned
    cout << "\nc2 after ++c2: ";
    c2.display();
    cout << "c3 received: ";
    c3.display();

    Counter c4(10);
    Counter c5 = c4++;  // assigned, then c4 incremented
    cout << "\nc4 after c4++: ";
    c4.display();
    cout << "c5 received: ";
    c5.display();

    return 0;
}
```

---

## Problem 3.3: Binary Operator Overloading (+ operator)

**Question:** Overload the + operator for a Complex class to add two complex numbers.

```cpp
#include <iostream>
using namespace std;

class Complex {
private:
    double real;
    double imag;

public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) { }

    // Overload + as member function
    Complex operator+(const Complex &c) {
        return Complex(real + c.real, imag + c.imag);
    }

    // Overload - as member function
    Complex operator-(const Complex &c) {
        return Complex(real - c.real, imag - c.imag);
    }

    // Overload * as member function
    Complex operator*(const Complex &c) {
        return Complex(
            real * c.real - imag * c.imag,
            real * c.imag + imag * c.real
        );
    }

    // Overload == for comparison
    bool operator==(const Complex &c) {
        return (real == c.real && imag == c.imag);
    }

    void display() {
        cout << real;
        if (imag >= 0)
            cout << " + " << imag << "i";
        else
            cout << " - " << -imag << "i";
        cout << endl;
    }
};

int main() {
    Complex c1(3, 4);
    Complex c2(1, 2);

    cout << "c1 = ";
    c1.display();

    cout << "c2 = ";
    c2.display();

    Complex c3 = c1 + c2;
    cout << "c1 + c2 = ";
    c3.display();

    Complex c4 = c1 - c2;
    cout << "c1 - c2 = ";
    c4.display();

    Complex c5 = c1 * c2;
    cout << "c1 * c2 = ";
    c5.display();

    cout << "c1 == c2? " << (c1 == c2 ? "Yes" : "No") << endl;

    return 0;
}
```

---

## Problem 3.4: Overloading << and >> Using Friend Function

**Question:** Overload stream insertion and extraction operators for a Distance class.

```cpp
#include <iostream>
using namespace std;

class Distance {
private:
    int feet;
    float inches;

public:
    Distance() : feet(0), inches(0) { }
    Distance(int f, float i) : feet(f), inches(i) { }

    // Friend function for << operator
    friend ostream& operator<<(ostream &out, const Distance &d);

    // Friend function for >> operator
    friend istream& operator>>(istream &in, Distance &d);

    // Overload + operator
    Distance operator+(const Distance &d) {
        int f = feet + d.feet;
        float i = inches + d.inches;

        if (i >= 12.0) {
            i -= 12.0;
            f++;
        }

        return Distance(f, i);
    }
};

ostream& operator<<(ostream &out, const Distance &d) {
    out << d.feet << "' " << d.inches << "\"";
    return out;
}

istream& operator>>(istream &in, Distance &d) {
    cout << "Enter feet: ";
    in >> d.feet;
    cout << "Enter inches: ";
    in >> d.inches;
    return in;
}

int main() {
    Distance d1, d2;

    cout << "Enter first distance:" << endl;
    cin >> d1;

    cout << "Enter second distance:" << endl;
    cin >> d2;

    cout << "\nDistance 1: " << d1 << endl;
    cout << "Distance 2: " << d2 << endl;

    Distance d3 = d1 + d2;
    cout << "Sum: " << d3 << endl;

    return 0;
}
```

---

## Problem 3.5: Data Conversion (Basic to Class, Class to Basic)

**Question:** Demonstrate type conversion between basic types and class types.

```cpp
#include <iostream>
using namespace std;

class Temperature {
private:
    double celsius;

public:
    // Constructor for basic to class conversion
    Temperature(double c = 0) : celsius(c) {
        cout << "Converted " << c << " to Temperature object" << endl;
    }

    // Conversion operator for class to basic (Fahrenheit)
    operator double() {
        double fahrenheit = (celsius * 9 / 5) + 32;
        cout << "Converting Temperature to double (Fahrenheit): ";
        return fahrenheit;
    }

    // Conversion operator to int
    operator int() {
        cout << "Converting Temperature to int: ";
        return (int)celsius;
    }

    void display() {
        cout << celsius << "°C" << endl;
    }
};

int main() {
    // Basic to Class conversion (using constructor)
    Temperature t1 = 100.0;  // double to Temperature
    cout << "t1 = ";
    t1.display();

    // Class to Basic conversion (using conversion operator)
    double f = (double)t1;  // Temperature to double (Fahrenheit)
    cout << f << "°F" << endl;

    int c = (int)t1;  // Temperature to int
    cout << c << endl;

    return 0;
}
```

---

# UNIT 4: Inheritance & Aggregation

## Problem 4.1: Single Inheritance

**Question:** Implement single inheritance with Person as base class and Student as derived class.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {
        cout << "Person constructor called" << endl;
    }

    void displayPerson() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }

    ~Person() {
        cout << "Person destructor called" << endl;
    }
};

class Student : public Person {
private:
    int rollNo;
    string course;

public:
    Student(string n, int a, int r, string c)
        : Person(n, a), rollNo(r), course(c) {
        cout << "Student constructor called" << endl;
    }

    void displayStudent() {
        displayPerson();
        cout << "Roll No: " << rollNo << ", Course: " << course << endl;
    }

    ~Student() {
        cout << "Student destructor called" << endl;
    }
};

int main() {
    Student s("John", 20, 101, "Computer Science");
    cout << "\nStudent Details:" << endl;
    s.displayStudent();
    cout << endl;

    return 0;
}
```

**Output:**

```
Person constructor called
Student constructor called

Student Details:
Name: John, Age: 20
Roll No: 101, Course: Computer Science

Student destructor called
Person destructor called
```

---

## Problem 4.2: Multilevel Inheritance

**Question:** Implement multilevel inheritance with Animal -> Mammal -> Dog.

```cpp
#include <iostream>
using namespace std;

class Animal {
protected:
    string name;

public:
    Animal(string n) : name(n) {
        cout << "Animal constructor" << endl;
    }

    void eat() {
        cout << name << " is eating" << endl;
    }

    ~Animal() {
        cout << "Animal destructor" << endl;
    }
};

class Mammal : public Animal {
protected:
    bool hasFur;

public:
    Mammal(string n, bool fur) : Animal(n), hasFur(fur) {
        cout << "Mammal constructor" << endl;
    }

    void breastfeed() {
        cout << name << " can breastfeed" << endl;
    }

    ~Mammal() {
        cout << "Mammal destructor" << endl;
    }
};

class Dog : public Mammal {
private:
    string breed;

public:
    Dog(string n, bool fur, string b) : Mammal(n, fur), breed(b) {
        cout << "Dog constructor" << endl;
    }

    void bark() {
        cout << name << " (Breed: " << breed << ") says Woof!" << endl;
    }

    void display() {
        cout << "Name: " << name << endl;
        cout << "Has Fur: " << (hasFur ? "Yes" : "No") << endl;
        cout << "Breed: " << breed << endl;
    }

    ~Dog() {
        cout << "Dog destructor" << endl;
    }
};

int main() {
    cout << "Creating Dog object:" << endl;
    Dog d("Buddy", true, "Golden Retriever");

    cout << "\nDog actions:" << endl;
    d.eat();        // From Animal
    d.breastfeed(); // From Mammal
    d.bark();       // From Dog

    cout << "\nDog details:" << endl;
    d.display();

    cout << "\nDestroying Dog object:" << endl;
    return 0;
}
```

---

## Problem 4.3: Multiple Inheritance

**Question:** Implement multiple inheritance where Student inherits from both Person and Marks.

```cpp
#include <iostream>
using namespace std;

class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) { }

    void displayPerson() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

class Marks {
protected:
    int marks[3];

public:
    Marks(int m1, int m2, int m3) {
        marks[0] = m1;
        marks[1] = m2;
        marks[2] = m3;
    }

    void displayMarks() {
        cout << "Marks: " << marks[0] << ", " << marks[1] << ", " << marks[2] << endl;
    }

    int getTotal() {
        return marks[0] + marks[1] + marks[2];
    }
};

class Student : public Person, public Marks {
private:
    int rollNo;

public:
    Student(string n, int a, int r, int m1, int m2, int m3)
        : Person(n, a), Marks(m1, m2, m3), rollNo(r) { }

    void display() {
        displayPerson();
        cout << "Roll No: " << rollNo << endl;
        displayMarks();
        cout << "Total: " << getTotal() << endl;
        cout << "Percentage: " << (float)getTotal() / 3 << "%" << endl;
    }
};

int main() {
    Student s("Alice", 20, 101, 85, 90, 88);
    s.display();

    return 0;
}
```

---

## Problem 4.4: Diamond Problem and Virtual Inheritance

**Question:** Demonstrate the diamond problem and solve it using virtual inheritance.

```cpp
#include <iostream>
using namespace std;

class Person {
protected:
    string name;

public:
    Person(string n = "Unknown") : name(n) {
        cout << "Person constructor: " << name << endl;
    }

    void display() {
        cout << "Name: " << name << endl;
    }
};

// Virtual inheritance
class Student : virtual public Person {
protected:
    int rollNo;

public:
    Student(string n, int r) : Person(n), rollNo(r) {
        cout << "Student constructor" << endl;
    }

    void displayStudent() {
        cout << "Roll No: " << rollNo << endl;
    }
};

class Employee : virtual public Person {
protected:
    int empId;

public:
    Employee(string n, int e) : Person(n), empId(e) {
        cout << "Employee constructor" << endl;
    }

    void displayEmployee() {
        cout << "Emp ID: " << empId << endl;
    }
};

class TA : public Student, public Employee {
private:
    string subject;

public:
    // With virtual inheritance, most derived class calls Person constructor
    TA(string n, int r, int e, string s)
        : Person(n), Student(n, r), Employee(n, e), subject(s) {
        cout << "TA constructor" << endl;
    }

    void displayTA() {
        display();           // Only one copy of name
        displayStudent();
        displayEmployee();
        cout << "Subject: " << subject << endl;
    }
};

int main() {
    cout << "Creating TA object:" << endl;
    TA ta("John", 101, 5001, "Computer Science");

    cout << "\nTA Details:" << endl;
    ta.displayTA();

    return 0;
}
```

---

## Problem 4.5: Aggregation and Composition

**Question:** Demonstrate aggregation (Car has Driver) and composition (Car has Engine).

```cpp
#include <iostream>
using namespace std;

// Independent class (for aggregation)
class Driver {
private:
    string name;
    string licenseNo;

public:
    Driver(string n, string lic) : name(n), licenseNo(lic) { }

    void display() {
        cout << "Driver: " << name << ", License: " << licenseNo << endl;
    }

    string getName() { return name; }
};

// Dependent class (for composition)
class Engine {
private:
    int horsepower;
    string type;

public:
    Engine(int hp, string t) : horsepower(hp), type(t) {
        cout << "Engine created" << endl;
    }

    void start() {
        cout << type << " engine (" << horsepower << " HP) started" << endl;
    }

    ~Engine() {
        cout << "Engine destroyed" << endl;
    }
};

class Car {
private:
    string model;
    Engine engine;    // Composition - Engine is part of Car
    Driver *driver;   // Aggregation - Driver is associated with Car

public:
    Car(string m, int hp, string engType)
        : model(m), engine(hp, engType), driver(nullptr) {
        cout << "Car " << model << " created" << endl;
    }

    void setDriver(Driver *d) {
        driver = d;
        cout << "Driver " << d->getName() << " assigned to " << model << endl;
    }

    void start() {
        if (driver) {
            cout << model << " is being started by " << driver->getName() << endl;
            engine.start();
        } else {
            cout << "No driver assigned!" << endl;
        }
    }

    ~Car() {
        cout << "Car " << model << " destroyed" << endl;
        // Note: Engine is automatically destroyed (composition)
        // Driver is NOT destroyed (aggregation)
    }
};

int main() {
    // Driver exists independently
    Driver d1("John", "DL-123456");

    {
        // Car with Engine (composition)
        Car car("Tesla Model S", 670, "Electric");

        // Associate Driver with Car (aggregation)
        car.setDriver(&d1);
        car.start();

        cout << "\nCar going out of scope..." << endl;
    }

    // Driver still exists after Car is destroyed
    cout << "\nDriver still exists:" << endl;
    d1.display();

    return 0;
}
```

---

# UNIT 5: STL Templates & Libraries

## Problem 5.1: Function Template

**Question:** Create a function template to find the maximum of two values.

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// Template specialization for strings (by length)
template <>
string maximum<string>(string a, string b) {
    return (a.length() > b.length()) ? a : b;
}

int main() {
    cout << "Max of 10 and 20: " << maximum(10, 20) << endl;
    cout << "Max of 3.14 and 2.78: " << maximum(3.14, 2.78) << endl;
    cout << "Max of 'A' and 'Z': " << maximum('A', 'Z') << endl;

    string s1 = "Hello";
    string s2 = "World!";
    cout << "Longer string: " << maximum(s1, s2) << endl;

    return 0;
}
```

---

## Problem 5.2: Class Template - Generic Stack

**Question:** Implement a generic Stack class template that works with any data type.

```cpp
#include <iostream>
using namespace std;

template <class T>
class Stack {
private:
    T *arr;
    int top;
    int capacity;

public:
    Stack(int size = 10) {
        capacity = size;
        arr = new T[capacity];
        top = -1;
    }

    ~Stack() {
        delete[] arr;
    }

    void push(T item) {
        if (isFull()) {
            cout << "Stack Overflow!" << endl;
            return;
        }
        arr[++top] = item;
    }

    T pop() {
        if (isEmpty()) {
            cout << "Stack Underflow!" << endl;
            return T();  // Return default value
        }
        return arr[top--];
    }

    T peek() {
        if (isEmpty()) {
            cout << "Stack is empty!" << endl;
            return T();
        }
        return arr[top];
    }

    bool isEmpty() {
        return top == -1;
    }

    bool isFull() {
        return top == capacity - 1;
    }

    int size() {
        return top + 1;
    }
};

int main() {
    // Stack of integers
    Stack<int> intStack(5);
    intStack.push(10);
    intStack.push(20);
    intStack.push(30);

    cout << "Integer Stack:" << endl;
    cout << "Top: " << intStack.peek() << endl;
    cout << "Pop: " << intStack.pop() << endl;
    cout << "Pop: " << intStack.pop() << endl;

    // Stack of strings
    Stack<string> strStack(5);
    strStack.push("Hello");
    strStack.push("World");

    cout << "\nString Stack:" << endl;
    cout << "Top: " << strStack.peek() << endl;
    cout << "Pop: " << strStack.pop() << endl;

    return 0;
}
```

---

## Problem 5.3: STL Vector Operations

**Question:** Demonstrate various vector operations in STL.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // Creating vectors
    vector<int> v1;                    // Empty vector
    vector<int> v2(5, 10);             // 5 elements, all = 10
    vector<int> v3 = {5, 2, 8, 1, 9};  // Initializer list

    // Adding elements
    v1.push_back(30);
    v1.push_back(10);
    v1.push_back(50);
    v1.push_back(20);
    v1.push_back(40);

    cout << "v1: ";
    for (int x : v1) cout << x << " ";
    cout << endl;

    // Size and capacity
    cout << "Size: " << v1.size() << endl;
    cout << "Capacity: " << v1.capacity() << endl;

    // Accessing elements
    cout << "First: " << v1.front() << endl;
    cout << "Last: " << v1.back() << endl;
    cout << "Element at index 2: " << v1[2] << endl;

    // Sorting
    sort(v1.begin(), v1.end());
    cout << "After sorting: ";
    for (int x : v1) cout << x << " ";
    cout << endl;

    // Sorting in descending order
    sort(v1.begin(), v1.end(), greater<int>());
    cout << "Descending: ";
    for (int x : v1) cout << x << " ";
    cout << endl;

    // Finding an element
    sort(v1.begin(), v1.end());  // Sort for binary_search
    if (binary_search(v1.begin(), v1.end(), 30)) {
        cout << "30 found in vector" << endl;
    }

    // Reversing
    reverse(v1.begin(), v1.end());
    cout << "Reversed: ";
    for (int x : v1) cout << x << " ";
    cout << endl;

    // Removing last element
    v1.pop_back();
    cout << "After pop_back: ";
    for (int x : v1) cout << x << " ";
    cout << endl;

    // Clearing
    v1.clear();
    cout << "After clear, size: " << v1.size() << endl;

    return 0;
}
```

---

## Problem 5.4: STL Map Operations

**Question:** Demonstrate map operations - inserting, accessing, iterating, and finding.

```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main() {
    // Creating a map
    map<string, int> studentMarks;

    // Inserting elements
    studentMarks["Alice"] = 85;
    studentMarks["Bob"] = 92;
    studentMarks["Charlie"] = 78;
    studentMarks.insert({"David", 88});
    studentMarks.insert(make_pair("Eve", 95));

    // Accessing elements
    cout << "Alice's marks: " << studentMarks["Alice"] << endl;

    // Iterating using iterator
    cout << "\nAll students (using iterator):" << endl;
    for (map<string, int>::iterator it = studentMarks.begin();
         it != studentMarks.end(); it++) {
        cout << it->first << ": " << it->second << endl;
    }

    // Iterating using range-based for
    cout << "\nAll students (range-based):" << endl;
    for (auto &pair : studentMarks) {
        cout << pair.first << ": " << pair.second << endl;
    }

    // Finding an element
    string searchName = "Bob";
    auto it = studentMarks.find(searchName);
    if (it != studentMarks.end()) {
        cout << "\nFound " << searchName << " with marks: " << it->second << endl;
    } else {
        cout << "\n" << searchName << " not found" << endl;
    }

    // Size
    cout << "\nTotal students: " << studentMarks.size() << endl;

    // Erasing
    studentMarks.erase("Charlie");
    cout << "After erasing Charlie, size: " << studentMarks.size() << endl;

    // Check if key exists
    if (studentMarks.count("Alice") > 0) {
        cout << "Alice exists in the map" << endl;
    }

    return 0;
}
```

---

## Problem 5.5: STL Set Operations

**Question:** Demonstrate set operations including insert, find, and set algorithms.

```cpp
#include <iostream>
#include <set>
#include <algorithm>
using namespace std;

int main() {
    // Creating sets
    set<int> s1 = {5, 2, 8, 1, 9, 5, 2};  // Duplicates ignored
    set<int> s2 = {4, 2, 7, 1, 6};

    cout << "Set s1 (unique, sorted): ";
    for (int x : s1) cout << x << " ";
    cout << endl;

    cout << "Set s2: ";
    for (int x : s2) cout << x << " ";
    cout << endl;

    // Inserting
    s1.insert(3);
    s1.insert(5);  // Already exists, ignored
    cout << "After insert(3): ";
    for (int x : s1) cout << x << " ";
    cout << endl;

    // Finding
    if (s1.find(8) != s1.end()) {
        cout << "8 found in s1" << endl;
    }

    // Set operations
    set<int> result;

    // Union
    set_union(s1.begin(), s1.end(), s2.begin(), s2.end(),
              inserter(result, result.begin()));
    cout << "Union: ";
    for (int x : result) cout << x << " ";
    cout << endl;

    result.clear();

    // Intersection
    set_intersection(s1.begin(), s1.end(), s2.begin(), s2.end(),
                     inserter(result, result.begin()));
    cout << "Intersection: ";
    for (int x : result) cout << x << " ";
    cout << endl;

    result.clear();

    // Difference (s1 - s2)
    set_difference(s1.begin(), s1.end(), s2.begin(), s2.end(),
                   inserter(result, result.begin()));
    cout << "Difference (s1-s2): ";
    for (int x : result) cout << x << " ";
    cout << endl;

    // Size
    cout << "Size of s1: " << s1.size() << endl;

    // Erase
    s1.erase(5);
    cout << "After erasing 5: ";
    for (int x : s1) cout << x << " ";
    cout << endl;

    return 0;
}
```

---

## Problem 5.6: STL Stack and Queue

**Question:** Demonstrate stack (LIFO) and queue (FIFO) operations.

```cpp
#include <iostream>
#include <stack>
#include <queue>
using namespace std;

int main() {
    // STACK - LIFO
    cout << "=== STACK (LIFO) ===" << endl;
    stack<int> stk;

    // Push
    stk.push(10);
    stk.push(20);
    stk.push(30);

    cout << "Top: " << stk.top() << endl;
    cout << "Size: " << stk.size() << endl;

    cout << "Popping: ";
    while (!stk.empty()) {
        cout << stk.top() << " ";
        stk.pop();
    }
    cout << endl;

    // QUEUE - FIFO
    cout << "\n=== QUEUE (FIFO) ===" << endl;
    queue<string> q;

    // Enqueue
    q.push("First");
    q.push("Second");
    q.push("Third");

    cout << "Front: " << q.front() << endl;
    cout << "Back: " << q.back() << endl;
    cout << "Size: " << q.size() << endl;

    cout << "Dequeuing: ";
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;

    // Priority Queue (Max Heap)
    cout << "\n=== PRIORITY QUEUE ===" << endl;
    priority_queue<int> pq;

    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);

    cout << "Highest priority first: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;

    return 0;
}
```

**Output:**

```
=== STACK (LIFO) ===
Top: 30
Size: 3
Popping: 30 20 10

=== QUEUE (FIFO) ===
Front: First
Back: Third
Size: 3
Dequeuing: First Second Third

=== PRIORITY QUEUE ===
Highest priority first: 50 30 20 10
```

---

# Quick Reference: Common Code Patterns

## Constructor Syntax

```cpp
ClassName() { }                          // Default
ClassName(params) { }                    // Parameterized
ClassName(const ClassName &obj) { }      // Copy
~ClassName() { }                         // Destructor
```

## Operator Overloading Syntax

```cpp
// Unary
ClassName operator-() { }
ClassName& operator++() { }               // Prefix
ClassName operator++(int) { }             // Postfix

// Binary
ClassName operator+(const ClassName &obj) { }

// Stream
friend ostream& operator<<(ostream &out, const ClassName &obj);
friend istream& operator>>(istream &in, ClassName &obj);
```

## Inheritance Syntax

```cpp
class Derived : public Base { };
class Derived : protected Base { };
class Derived : private Base { };
class Derived : public Base1, public Base2 { };   // Multiple
class Derived : virtual public Base { };          // Virtual
```

## Template Syntax

```cpp
template <typename T>
T func(T param) { }

template <class T>
class ClassName { T member; };
```

---

> **Practice these programs thoroughly for your exam!**
