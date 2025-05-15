# Final Project: JSON Database with Python OOP  
## Due: 05-15-2025
## Kade Miller

---

## Overview & Key Concepts:

This project demonstrates the use of object-oriented programming and JSON files to simulate a basic, modular database system.

We will build:
- A generic base class `JsonDB` that performs universal database operations (CRUD).
- Specialized subclasses (`PeopleDB`, `MeteoriteDB`, `EarthquakeDB`) that inherit from `JsonDB` and implement custom logic, such as filtering, validation, or querying based on domain-specific attributes.

### Goals:
- Use Python (though we reference C++ conceptually).
- Show a clear separation between generic database logic and domain-specific behavior.
- Understand how inheritance supports code reuse and specialization.

---

## Design Summary:

- `JsonDB`:  
  - Loads and saves data to a `.json` file.  
  - Stores records in-memory using a list.  
  - Provides methods: `create`, `read`, `update`, `delete`.  

- `PeopleDB`:  
  - Adds methods like `create_person()` and `find_by_name()`.  
  - Example validation: check for valid email.

- `MeteoriteDB`:  
  - Adds methods like `find_heaviest()` or `find_by_year_range()`.

- `EarthquakeDB`:  
  - Adds filters for magnitude or place-based queries.

### Why Not Just One Class?

While a single flexible DB class might work, using inheritance and OOP design gives each data domain its own logic and constraints, making the code easier to expand, test, and maintain.

---

## Python Code Implementation:

```python
import json
import os

# ----------- Base Class: JsonDB -----------

class JsonDB:
    def __init__(self, filepath):
        self.filepath = filepath
        self.data = self._load_data()

    def _load_data(self):
        if not os.path.exists(self.filepath):
            return []
        with open(self.filepath, 'r') as file:
            return json.load(file)

    def _save_data(self):
        with open(self.filepath, 'w') as file:
            json.dump(self.data, file, indent=2)

    def create(self, record):
        """Append a new record to the list."""
        self.data.append(record)
        self._save_data()
        return len(self.data) - 1  # ID = index

    def read(self, **filters):
        """Read all records or filter by key-value."""
        if not filters:
            return self.data
        return [rec for rec in self.data if all(rec.get(k) == v for k, v in filters.items())]

    def update(self, record_id, updates):
        if 0 <= record_id < len(self.data):
            self.data[record_id].update(updates)
            self._save_data()
            return True
        return False

    def delete(self, record_id):
        if 0 <= record_id < len(self.data):
            del self.data[record_id]
            self._save_data()
            return True
        return False
```

---

### PeopleDB: Subclass Example:

```python
class PeopleDB(JsonDB):
    def find_by_name(self, first_name=None, last_name=None):
        results = []
        for person in self.data:
            if (first_name is None or person.get("first_name") == first_name) and \
               (last_name is None or person.get("last_name") == last_name):
                results.append(person)
        return results

    def create_person(self, first_name, last_name, email):
        if "@" not in email:
            raise ValueError("Invalid email")
        new_person = {
            "first_name": first_name,
            "last_name": last_name,
            "email": email
        }
        return self.create(new_person)
```

---

### MeteoriteDB: Subclass Example:

```python
class MeteoriteDB(JsonDB):
    def find_heaviest(self, top_n=5):
        sorted_data = sorted(self.data, key=lambda x: float(x.get("mass", 0)), reverse=True)
        return sorted_data[:top_n]

    def find_by_year_range(self, start_year, end_year):
        return [m for m in self.data if start_year <= int(m.get("year", 0)) <= end_year]
```

---

### EarthquakeDB: Subclass Example

```python
class EarthquakeDB(JsonDB):
    def filter_by_magnitude(self, min_mag):
        return [e for e in self.data if float(e.get("magnitude", 0)) >= min_mag]

    def filter_by_place(self, keyword):
        return [e for e in self.data if keyword.lower() in e.get("place", "").lower()]
```

---

## Sample Usage Flow: 

```python
def main():
    # Generic usage
    db = JsonDB("generic.json")
    db.create({"hello": "world"})
    print("All data:", db.read())

    # People
    people_db = PeopleDB("people.json")
    people_db.create_person("Teresa", "Smith", "teresa@example.com")
    print("Search Teresa:", people_db.find_by_name(first_name="Teresa"))

    # Meteorites
    meteor_db = MeteoriteDB("meteorites.json")
    heavy = meteor_db.find_heaviest()
    print("Top Meteorites:", heavy)

    # Earthquakes
    quake_db = EarthquakeDB("quakes.json")
    big_quakes = quake_db.filter_by_magnitude(6.0)
    print("Strong earthquakes:", big_quakes)

if __name__ == "__main__":
    main()
```

---

## Optional Advanced Additions

### Context Manager Support:
```python
def __enter__(self):
    return self
def __exit__(self, exc_type, exc_val, exc_tb):
    self._save_data()
```

Then use:
```python
with PeopleDB("people.json") as db:
    db.create_person("Kade", "Miller", "kade@example.com")
```

---

## Appendix: Sample JSON Files

### people.json
```json
[ { "first_name": "Teresa", "last_name": "Smith", "email": "teresa@example.com" }, ... ]
```

### meteorites.json
```json
[ { "name": "Abee", "id": "1", "mass": "107000", "year": "1952" }, ... ]
```

### quakes.json
```json
[ { "place": "California", "magnitude": "6.5", "depth": "10" }, ... ]
```

---

## Takeaways

- The base class encapsulates core logic (CRUD + persistence).
- Subclasses define domain-specific operations.
- OOP inheritance allows easy expansion for other datasets like `InventoryDB`, `StudentDB`, etc.
- Python’s dynamic typing and JSON-friendly data structures make it ideal for rapid development.

---
