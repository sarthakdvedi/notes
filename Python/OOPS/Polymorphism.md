
## 1. Duck Typing (without inheritance) -
- In many statically typed languages (like Java or C++), a function can only accept an object if it belongs to a specific class or implements a specific interface. Python ignores this constraint completely.
- Taking the object it can call same method and output will be according to the object nature.

```python
class Car:
    def move(self):
        return "Driving on the road"

class Boat:
    def move(self):
        return "Sailing on the water"

# A standalone function that doesn't care about the object's class heritage
def travel(vehicle):
    print(vehicle.move())

travel(Car())   # Output: Driving on the road
travel(Boat())  # Output: Sailing on the water
```



## 2. Method Overriding (with inheritance) -
```python
class Animal:
    def make_sound(self):
        return "Generic sound"

class Dog(Animal):
    def make_sound(self):
        return "Woof!"
```


## 3. Operator Overloading
- Python allows built-in operators to exhibit polymorphic behavior depending on the objects they act upon. This is achieved using special "magic" or "dunder" (double underscore) methods
- For example, the `+` operator executes addition for numbers but concatenation for strings because their underlying classes implement `__add__` differently

```python
print(5 + 5)          # Output: 10 (Addition)
print("a" + "b")      # Output: "ab" (Concatenation)


class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    # Overriding the '+' operator
    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented

    # Overriding the '==' operator
    def __eq__(self, other):
        if isinstance(other, Vector):
            return self.x == other.x and self.y == other.y
        return False

    # Overriding the string print layout
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

# Creating instances
v1 = Vector(2, 4)
v2 = Vector(3, 1)
v3 = Vector(2, 4)

# Using the overloaded '+' operator
result = v1 + v2 
print(result)  # Output: Vector(5, 5)

# Using the overloaded '==' operator
print(v1 == v3)  # Output: True
print(v1 == v2)  # Output: False
```


## 4. Method Overloading -
- ==Python **does not support** traditional method overloading; if you define a method twice, the last one overrides the previous ones==
- However, Python achieves the exact same polymorphic behavior using **default arguments** or variable arguments (`*args` and `**kwargs`) within a single method definition

```python
class Calculator:
    def add(self, a, b, c=0):
        return a + b + c

calc = Calculator()
print(calc.add(2, 3))     # Output: 5
print(calc.add(2, 3, 4))  # Output: 9
```

