# H05 – Understanding Abstraction in OOP  
### Due: 03-25-2025  
### Kade Miller

---

## Part A: Conceptual Questions:

### 1. What is abstraction in OOP?  
Abstraction is about modeling only what matters to the user or system and hiding the rest. It lets us focus on the essential features of an object while ignoring internal details.

### 2. Real-world analogy:
Think of a TV remote, you see buttons like “volume” and “channel,” but you don’t need to know the internal circuits that control the TV. That’s abstraction in action.

---

### 3. Abstraction vs. Encapsulation:

| Concept       | Focuses On                        |
|---------------|------------------------------------|
| Abstraction   | What an object does            |
| Encapsulation | How it hides internal details  |

They’re often confused because both hide complexity, but abstraction defines behavior while encapsulation protects data.

---

### 4. Smart Thermostat Example - 

Essential attributes:
- currentTemperature
- targetTemperature
- powerState

Essential methods:
- setTemperature()
- togglePower()

Omitted details:
Stuff like circuit board design, sensor calibration, or firmware update logic isn’t relevant to the user and would clutter the public interface. That’s why it stays hidden.

---

### 5. Benefits of Abstraction

- Makes code easier to use and understand across large teams.
- Reduces how often you need to change things when the internals evolve.

One-liner: Abstraction removes distractions so you can build and maintain software faster.

---

## Part B: Minimal Class Example (C++):

### Abstract Class Structure - 

```cpp
#include <iostream>
using namespace std;

// Abstract class
class BankAccount {
public:
    virtual void deposit(double amount) = 0;
    virtual void withdraw(double amount) = 0;
    virtual ~BankAccount() {}
};

// Derived class
class SavingsAccount : public BankAccount {
private:
    double balance;

public:
    SavingsAccount() : balance(0.0) {}

    void deposit(double amount) override {
        balance += amount;
    }

    void withdraw(double amount) override {
        if (amount <= balance)
            balance -= amount;
    }

    void displayBalance() {
        cout << "Balance: $" << balance << endl;
    }
};
```

---

## How It Demonstrates Abstraction:

The BankAccount class defines what every account should do (deposit, withdraw) without revealing how it’s done. The internal workings (balance management, validations) are handled privately by SavingsAccount.

---

## Part C: Reflection & Comparison:
What Would I Hide?
In SavingsAccount, I’d hide:
The balance variable (make it private)


Internal checks like overdraft protection


Logging or encryption if included


This keeps the public interface clean and focused on deposit() and withdraw() only.

---

## Polymorphism vs. Abstraction
Polymorphism happens when a BankAccount* points to a SavingsAccount and calls withdraw(). The code uses abstraction (base class interface) and polymorphism (runtime method resolution) together for flexibility.

---

## Real-world Example
In healthcare apps, you might define a MedicalRecord abstraction. The app interacts with it through methods like getSummary() without ever touching the internal structure of sensitive patient data.

---

## (Optional) Additional Exploration:
Interfaces vs. Abstract Classes:
An interface defines only method signatures.
An abstract class can include both abstract methods and shared implementation.
Use an interface when multiple unrelated classes need to implement the same capability.

---

Testing Abstractions - 
You can write tests against derived classes (like SavingsAccount) that implement the abstract interface.
Mock implementations can also help test how code interacts with the abstraction, not the internals.
