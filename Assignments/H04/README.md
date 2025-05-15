# H04 – Understanding Polymorphism in OOP  
### Due: 03-25-2025  
### Kade Miller

---

## Part A: Conceptual Questions

### 1. What is polymorphism?  
Polymorphism allows objects of different classes to be treated as if they are of the same base type, while still using their own behavior. It means “many forms,” and lets the same interface call different implementations.

### 2. Why is polymorphism a pillar of OOP?  
Polymorphism allows flexibility, code reuse, and cleaner design by letting us write code that works with general types but still behaves specifically based on the object passed in.

---

### 3. Compile-Time Polymorphism (Overloading)  
This occurs when multiple methods in the same class have the same name but different parameter lists. The correct method is chosen at compile time.

### 4. Runtime Polymorphism (Overriding)  
This happens when a derived class provides its own version of a base class method. The correct version is chosen at runtime through a base pointer or reference.

> Runtime polymorphism requires inheritance because it depends on using a base type to refer to a derived object.

---

### 5. Why use method overloading?  
It simplifies the interface by allowing the same method name to handle different inputs, making the class easier to use.

Example: A `print()` method in a Logger class could take a string, an int, or a float — all with the same name but different parameters.

---

### 6. Why use method overriding?  
It lets derived classes customize behavior inherited from a base class. The `virtual` keyword in C++ is needed to tell the compiler to support dynamic dispatch — choosing the correct method at runtime instead of compile time.

---

## Part B: Minimal Code Example:

### Runtime Polymorphism (C++)

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Shape {
public:
    virtual void draw() = 0;  // abstract method
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Circle." << endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Rectangle." << endl;
    }
};

int main() {
    vector<Shape*> shapes;
    shapes.push_back(new Circle());
    shapes.push_back(new Rectangle());

    for (Shape* s : shapes)
        s->draw();  // correct draw() is chosen at runtime

    // cleanup
    for (Shape* s : shapes)
        delete s;

    return 0;
}
```

---

## Explanation and Part C:

Explanation - 
This example shows how Shape* can point to both Circle and Rectangle. Even though the method call is made on a base class pointer, the correct derived version of draw() runs. That’s runtime polymorphism.

---

Part C: Overloading vs. Overriding Distinctions - 
Compile-time resolution (Overloading)
If a Calculator class has calculate(int, int) and calculate(double, double), the compiler picks the correct one at compile time based on the argument types.

Runtime resolution (Overriding)
In the Shape example, the decision to call Circle::draw() or Rectangle::draw() is made at runtime depending on the actual object the pointer refers to.

This matters because it allows us to write code that works generically but behaves specifically.

---

## Part D: Reflection & Real-World Applications:

Practical Example - 
In a game engine, you might have a base class called GameEntity. polymorphism allows you to store all different entities (player, enemy, NPC, etc.) in a single array and still call the correct update() method for each.

This cuts down on duplicate logic and makes the codebase way easier to expand or manage.

Pitfalls - 
Overloading Pitfall: Easy to confuse which method will run, especially with implicit type conversions (e.g., int vs float).

Overriding Pitfall: Can lead to confusing bugs if the base method isn’t marked virtual, or if developers forget to override.

---

Triangle Class Example: 
If we add a new Triangle class that inherits from Shape and overrides draw(), we don’t need to change any other code that uses Shape* pointers. The draw method just works.
