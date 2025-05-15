# H01 – Homework: Classes & Objects  
### Kade Miller  
Due: 03-25-2025

---

## Part A: Conceptual Questions

### 1. What is a class in object-oriented programming?  
A class is a blueprint for creating objects. It defines the structure and behavior of what the object should have and do, using variables (attributes) and methods (functions).

### 2. What is an object, and how does it relate to a class?  
An object is an actual instance of a class. It has its own copies of the class’s variables and can call the class’s methods.

### 3. Define a constructor. What is its role in a class?  
A constructor is a method that automatically runs when an object is created. Its job is to initialize the object’s variables.

### 4. Define a destructor. Why is it important in managing an object’s lifecycle?  
A destructor is a method that runs when the object is destroyed. It’s used to clean up resources like memory, files, or connections the object used during its life.

### 5. Briefly describe the lifecycle of an object from instantiation to destruction.  
The lifecycle begins when the object is created using a class constructor. It then performs its tasks during its lifetime. When it is deleted, its destructor is called and the object is destroyed.

### 6. Why is it important for a class to manage its resources during its lifecycle?  
If a class doesn’t release resources properly, it can cause memory leaks or leave files open. This leads to poor performance, crashes, or security issues.

---

## Part B: Minimal Coding Example

### `Goblin` Class (C++)

```cpp
#include <iostream>
using namespace std;

class Goblin {
private:
    int health;

public:
    // Constructor
    Goblin(int h) {
        health = h;
        cout << "Goblin created with " << health << " HP." << endl;
    }

    // Destructor
    ~Goblin() {
        cout << "Goblin destroyed." << endl;
    }

    // Public method
    void showStats() {
        cout << "Goblin Health: " << health << endl;
    }
};

int main() {
    Goblin g(30);
    g.showStats();
    return 0;
}
```

### Explanation: 

This Goblin class uses a constructor to initialize its health when the object is created. When the Goblin object goes out of scope at the end of main(), the destructor is automatically called and prints a message. This shows the full object lifecycle: creation → use → destruction. It also demonstrates encapsulation by keeping health private and exposing behavior through a public method.

### Part C: 

Part C: Reflection & Short Answer
How do constructors help ensure that an object starts its lifecycle in a valid state?
Constructors make sure that required variables are set when the object is created. They help avoid bugs caused by uninitialized data.
Explain why destructors are necessary, especially in languages without automatic garbage collection.
Destructors are critical in languages like C++ because they give you a safe place to manually release memory, close files, or disconnect resources. Without them, your program could leak memory or crash.
What could happen if a class does not properly manage its resources during its lifecycle?
It could cause memory leaks, file locks, or dangling pointers. Over time, this degrades performance and can make your software unstable or unsafe.
