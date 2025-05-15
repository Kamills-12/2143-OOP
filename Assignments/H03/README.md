# H03 – Inheritance in OOP  
### Due: 03-25-2025  
### Kade Miller

---

## Part A: Conceptual Questions

### 1. Define inheritance  
Inheritance allows a class to take on the properties and behavior of another class. It’s like building on a base template, the new class (derived) inherits variables and methods from the old one (base) and can add or change features.

### 2. Inheritance vs. Composition/Aggregation  
- Inheritance creates an “is-a” relationship. (A Car is a Vehicle.)  
- Composition/Aggregation create a “has-a” relationship. (A Car has an Engine.)

With inheritance, the derived class gets access to everything in the base class automatically. With composition, you plug in other classes as parts.

### 3. Types of Inheritance + Examples  
- Single Inheritance: One base, one derived class.  
  Example: A `Car` class inherits from `Vehicle`.

- Multiple Inheritance: A class inherits from multiple base classes.  
  Example: A `FlyingCar` inherits from both `Car` and `Aircraft`.

### 4. Method Overriding  
Overriding means replacing a method from the base class with a new version in the derived class. It’s useful when the base class behavior isn’t specific enough.

Example: `Vehicle::drive()` is generic, but `Car::drive()` can include details like “turning on headlights.”

Overriding is better than adding a new method when the interface should stay consistent, but the behavior needs to change.

### 5. Real-world Analogy: 
A Dog is a kind of Animal. It inherits features like breathing, moving, and eating. But it might also override certain behaviors like how it communicates (barking instead of meowing). This models how subclasses refine behavior while still sharing the base features.

---

## Part B: Minimal Code Example

### C++ Inheritance Structure:

```cpp
#include <iostream>
using namespace std;

// Base class
class Vehicle {
public:
    string brand;
    void drive() {
        cout << "Vehicle is driving." << endl;
    }
};

// Derived class
class Car : public Vehicle {
public:
    int doors;
    void drive() {
        cout << "Car is driving with " << doors << " doors." << endl;
    }
};

int main() {
    Vehicle v;
    v.brand = "Generic";
    v.drive();  // Output: Vehicle is driving.

    Car c;
    c.brand = "Toyota";
    c.doors = 4;
    c.drive();  // Output: Car is driving with 4 doors.

    return 0;
}
```

---

## Explanation and Part C:

Explanation:
The Car class inherits from Vehicle. It gets the brand and drive() method from the base class. Then it overrides drive() to give more specific behavior. This demonstrates runtime polymorphism and the structure of single inheritance in C++.

Part C: Reflection & Discussion:
When to Use Inheritance - 
Good: When you have a clear “is-a” relationship, like Dog is an Animal.
 Bad: For unrelated classes — forcing inheritance could make the code fragile or confusing.
Overriding vs. Overloading -
Overriding: Replace base method with custom behavior in derived class (runtime).


Overloading: Same method name with different parameters in the same class (compile time).
Inheritance uses overriding to give flexibility across a class hierarchy.


Inheritance vs Interfaces / Abstract Classes - 
Inheritance gives you actual behavior and data.


Interfaces / Abstract Classes only define structure (no implementations).
 Use abstract classes when you want a base class that can't be instantiated but should provide a contract for subclasses.


Pitfall of Multiple Inheritance:
You can run into a problem where two base classes define the same method or data, and the compiler doesn’t know which one to use.
Solution: Use virtual inheritance in C++, or avoid multiple class inheritance by favoring interface-style patterns.

---

## Part D: (Optional) Research:
Inheritance in Java vs. C++:
Java: Only supports single class inheritance.


C++: Supports full multiple inheritance, but it can lead to complexity. Provides virtual inheritance to help manage it.


Open-Closed Principle + Inheritance: 
The Open-Closed Principle says classes should be open for extension, but closed for modification.
 Inheritance supports this by letting you add new behavior in a subclass without changing the base class.
Example: Add a Truck class that inherits from Vehicle and overrides drive(), no need to touch the Vehicle code.
