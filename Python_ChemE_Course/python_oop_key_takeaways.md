# 🐍 Python OOP Key Takeaways & Examples

## 1. Classes and Objects
- A **class** is a blueprint for creating objects.
- An **object** (instance) is created from a class.

### Example:
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

rafael = Person("Rafael", 32)
print(rafael.name)  # Rafael
print(rafael.age)   # 32
```

---

## 2. Methods vs Functions
- Functions inside a class are called **methods**.
- `self` always refers to the current instance.

### Example with a method:
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def say_hello(self):
        print(f"Hi, my name is {self.name} and I am {self.age} years old.")

rafael = Person("Rafael", 32)
rafael.say_hello()
```

---

## 3. Dunder (Magic) Methods
- Special methods with `__double_underscores__`.
- Allow custom behaviors for built-in operations.

### Useful dunder methods:
- `__init__` → constructor (runs when object is created).  
- `__str__` → string representation for `print(obj)`.  
- `__repr__` → developer representation (`repr(obj)`).  
- `__len__` → defines `len(obj)`.  
- `__getitem__` → indexing with `obj[i]`.  
- `__add__` → addition with `+`.  
- `__eq__` → comparison with `==`.  

### Example with multiple dunder methods:
```python
class Team:
    def __init__(self, name, members):
        self.name = name
        self.members = members

    def __str__(self):
        return f"Team {self.name} with {len(self)} members"

    def __repr__(self):
        return f"Team(name='{self.name}', members={self.members})"

    def __len__(self):
        return len(self.members)

    def __getitem__(self, index):
        return self.members[index]

    def __add__(self, other):
        return Team(self.name + "&" + other.name,
                    self.members + other.members)

    def __eq__(self, other):
        return self.members == other.members

team1 = Team("Alpha", ["Alice", "Bob"])
team2 = Team("Beta", ["Charlie", "Diana"])
print(team1)         # Team Alpha with 2 members
print(len(team1))    # 2
print(team1[0])      # Alice
print(team1 + team2) # Team Alpha&Beta with 4 members
print(team1 == team2)# False
```

---

## 4. Encapsulation
- Bundles data (attributes) and methods inside a class.
- Restricts direct access to data → promotes safe interaction.

### Levels of access:
- **Public**: normal attributes (accessible everywhere).  
- **Protected** (`_var`): internal use (convention, not enforced).  
- **Private** (`__var`): name-mangled, harder to access directly.

### Example: Bank Account with Encapsulation
```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
        else:
            print("Deposit must be positive!")

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient funds or invalid amount!")

account = BankAccount("Alice", 1000)
print(account.get_balance())  # 1000
account.deposit(500)
print(account.get_balance())  # 1500
account.withdraw(2000)        # Insufficient funds
print(account.get_balance())  # 1500
```

---

# 🎯 Summary
- **Classes** = blueprints, **Objects** = instances.  
- **Methods** are functions inside classes, always use `self`.  
- **Dunder methods** let your objects behave like built-ins.  
- **Encapsulation** protects data by controlling access through methods.  
