# H07: Basic Design Principles in Software Development  
## Due: 03-25-2025 (Tuesday)
## Kade Miller

---

## Part A: Conceptual Questions:

### DRY (Don’t Repeat Yourself) - 

- Definition: DRY means avoiding code duplication by abstracting repeated logic into reusable components (like functions or classes).  
  Violation Example:
  ```cpp
  void printUserA() {
      std::cout << "Name: John\nAge: 30\nEmail: john@example.com\n";
  }

  void printUserB() {
      std::cout << "Name: Jane\nAge: 28\nEmail: jane@example.com\n";
  }
  ```
  Refactor to DRY:
  ```cpp
  void printUser(std::string name, int age, std::string email) {
      std::cout << "Name: " << name << "\nAge: " << age << "\nEmail: " << email << "\n";
  }
  ```

---

### KISS (Keep It Simple, Stupid) - 

- Definition: KISS encourages developers to write simple, straightforward code that’s easy to read, test, and maintain.
- Drawback of Oversimplifying: Over-simplified code might lack necessary flexibility or error handling, making it harder to scale or adapt later.

---

### Introduction to SOLID (High-Level) - 

- SRP (Single Responsibility Principle): A class should have only one reason to change, one job or responsibility.
- OCP (Open-Closed Principle): Code should be open for extension, but closed for modification.

---


- Why SOLID matters: In large codebases, SOLID principles help organize responsibilities clearly, reduce bugs during updates, and make the system easier to scale and maintain.

---

## Part B: Minimal Examples or Scenarios: 

### DRY Violation & Fix - 

Before (Repeated Code):
```cpp
void showAdmin() {
    std::cout << "Role: Admin\nPermissions: All\n";
}
void showUser() {
    std::cout << "Role: User\nPermissions: Limited\n";
}
```

After (Refactored):
```cpp
void showRole(std::string role, std::string permissions) {
    std::cout << "Role: " << role << "\nPermissions: " << permissions << "\n";
}
```

---

### KISS Principle Example: 

Overly Complex:
```cpp
float getDiscount(float price, std::string type) {
    if ((type == "holiday" && price > 100) || (type == "clearance" && price > 50)) {
        return price * 0.20;
    } else if (type == "member" && price > 80) {
        return price * 0.15;
    }
    return 0;
}
```

Simplified (KISS):
```cpp
float getDiscount(float price, float rate) {
    return price * rate;
}
```

---

### SOLID Application - 

Problem: `Shape` interface has both `draw()` and `computeArea()`. But not all shapes need both.

Interface Segregation Principle (ISP):
```cpp
class Drawable {
public:
    virtual void draw() = 0;
};

class Measurable {
public:
    virtual float computeArea() = 0;
};

class Circle : public Drawable, public Measurable {
    void draw() override { /*...*/ }
    float computeArea() override { return 3.14f * r * r; }
};
```

Now shapes only implement the functionality they need.

---

## Part C: Reflection & Short Discussion:

### Trade-Offs: 

Readable Repetition: Sometimes repeating a few lines is clearer than abstracting into a complex function that handles multiple cases awkwardly.

---

### Combining Principles - 

DRY + KISS Together: Using a helper function to avoid repetition (DRY), but keeping it small and clear (KISS).
Example:
```cpp
void showMessage(std::string type) {
    std::cout << (type == "error" ? "An error occurred." : "Success!") << "\n";
}
```

---

### SOLID in Practice - 

Strict Adherence Not Always Needed: In small projects, applying every SOLID principle might be overkill. Simpler designs work better early on, where flexibility and rapid changes matter more than abstraction layers.
