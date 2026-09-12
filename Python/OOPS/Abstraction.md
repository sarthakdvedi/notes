- By importing abc class, and using @abstractmethod decorator.
- it's like cpp, --> can contain both abstract and non abstract methods.

```python
from abc import ABC, abstractmethod

# Abstract Class
class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

# Concrete Subclass
class Car(Vehicle):
    def start_engine(self):
        return "Car engine started. Vroom!"

# my_vehicle = Vehicle()  # This will raise a TypeError
my_car = Car()
print(my_car.start_engine())  # Output: Car engine started. Vroom!
```




---

### Pro Tip: Calling Abstract Methods inside Concrete Methods

You can even call an abstract method from _inside_ a concrete method within the same abstract class. Because the subclass is guaranteed to implement the abstract method, Python will safely execute it at runtime.


```python
class Appliance(ABC):
    @abstractmethod
    def turn_on(self):
        pass

    # Concrete method calling an abstract method
    def operate(self):
        # Python knows the subclass will provide turn_on()
        status = self.turn_on() 
        return f"Operation log: {status}"
```