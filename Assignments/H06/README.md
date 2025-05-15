# H06: Understanding Composition and Aggregation in OOP  
## Due: 03-25-2025 (Tuesday)
## Kade Miller
---

## Part A: Conceptual Questions:

### Composition vs. Aggregation - 

- Composition is a strong "has-a" relationship where one class owns another. The contained object cannot exist independently of the container.  
  Example:  
  ```cpp
  class Engine {
  public:
      Engine() {}
  };

  class Car {
  private:
      Engine engine; // Composition: Car owns Engine
  };
  ```

- Aggregation is a weaker "has-a" relationship where one class uses another, but the contained object can exist independently.  
  Example:  
  ```cpp
  class Player {
  public:
      Player(std::string n) : name(n) {}
  private:
      std::string name;
  };

  class Team {
  private:
      Player* player; // Aggregation: Team uses Player
  public:
      Team(Player* p) : player(p) {}
  };
  ```

- Composition implies stronger ownership, when the parent is destroyed, so is the child.

---

### When to Use:

- Composition Scenario (Gaming): A `GameCharacter` has a `HealthBar` that updates as the character takes damage. If the character is deleted, so is the HealthBar, composition is ideal.
- Aggregation Scenario: A `Window` class has a reference to a `Theme` object. The theme exists independently and can be shared, aggregation fits better due to looser coupling.

---

### Differences from Inheritance:

- Composition/Aggregation represent "has-a" relationships, while inheritance represents "is-a".
- OOP design may favor composition to avoid deep inheritance trees, improve modularity, and support change without breaking parent-child contracts.

---

### Real-World Analogy:

- A Car has an Engine (composition, engine is part of the car).
- A Car has a Driver (aggregation, driver exists independently).
- These distinctions matter to manage object lifecycles, avoid memory leaks, and design loosely coupled systems.

---

## Part B: Minimal Class Design (Option 1):

```cpp
class Address {
private:
    std::string street;
    std::string city;
public:
    Address(std::string s, std::string c) : street(s), city(c) {}
};

class Person {
private:
    Address* address; // Aggregation: Person uses Address, but doesn't own it
public:
    Person(Address* addr) : address(addr) {}
};
```

- In this example, `Person` holds a pointer to an `Address` that may exist independently. This is aggregation because `Address` is not destroyed with `Person`.

---

## Part C: Reflection & Short Discussion:

### Ownership & Lifecycle - 

- In composition, when the parent object is destroyed, the child object is destroyed too.
- In aggregation, the child can exist independently and may still be used by other objects after the parent is gone.

---

### Advantages & Pitfalls: 

- Advantage of Composition: Full control over lifecycles; child objects are tightly integrated and don’t need to be managed separately.
- Pitfall of Wrong Use: Using composition when objects should live independently can lead to inflexible and overly tight coupling.

---

### Contrast with Inheritance:

- "Has-a" (composition/aggregation) means building systems by combining objects with specific roles.
- "Is-a" (inheritance) can overcomplicate the hierarchy and break when behavior changes.
- Favoring composition/aggregation helps reduce dependencies and increases flexibility in design.
