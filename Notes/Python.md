
![1752812344068](https://github.com/user-attachments/assets/b4fef07b-0fd4-4c50-904a-c57deb8115dc)



## PYTHON ESSENTIALS (NEVER FORGET!)

### Variables & Data Types
```python
x = 10            # int
pi = 3.14         # float
name = "Luis"     # str
flag = True       # bool
data = [1, 2, 3]  # list
```

### Bitwise & Comparison Operators
| Operator | Description | Example |
|----------|-------------|---------|
|   &      | bitwise AND | A & b   |  
|   |      | bitwise OR  | a | b   |
|   ^      | XOR         | a^b     |
|   ~      | bitwise NOT | ~a      |
|   <<     | bitwise left shift | a  << b|
|   >>     | bitwise right shift | a >> b|
|   ==     | equality    | a == b  |
|   !=     | inequality  | a != b  |
|   <      | less than   | a < b   |
|   <=     | less than or equal to| a <= b |
|   >      | greater than| a > b   |
|   >=     | greater than or equal to| a >= b |


# convert int to binary
``` python
bin(3) #output -> '0b11'
```

# convert binary to int
``` python
int('11', 2) # the 2 stands for the base of the integer (binary = base 2)
# output -> '3'
```

### Functions
``` python
def area_circle(r):
  return 3.1416 * r ** 2
```

### IF / ELSE
``` python
if x > 5:
  print("Big")
elif x == 5:
  print("Medium")
else:
  print("small")
```

### Loops
``` python
for i in range(5):
  print(i)

while True:
  break
```

### List Comprehension
``` python
squares = [i**2 for i in range(10) if i % 2 == 0]
```

### Enumerate
``` python
for i, val in enumerate(['a', 'b', 'c']):
  print(i,val)
```

### Zip
``` python
for name, score in zip(['Luis', 'Anne'], [90. 95]):
  print(name, score)
```

### Lambda & Map
``` python
double = lambda x: x * 2
result = list(map(double, [1, 2, 3]))
```

### Filter
``` python
evens = list(filter(lambda x: x % 2 == 0, range(10)))
```

### Classes
``` python
class RocketStove:
  def __init__(self, air_inlet, chamber_diameter):
      self.air_inlet = air_inlet
      self.chamber_diameter = chamber_diameter

  def efficiency(self):
      return (self.air_inlet ** 2) / self.chamber_diameter

#or this

class Simulation:
  def __init__(self, state, dt=0.01):
      self.state = state
      self.dt = dt

  def step(self):
      # physics update
      self.state['T'] += -0.05 * self.state['T'] * self.dt

  def run(self, steps):
      for _ in range(steps:
          self.step()
      # i use this class for thermal models, digital twins or even Unity WebSocket backends :)))
```


### Decorators & Contexts
This allows you to modify or extend the behavior of functions or methods without changing their actual code. They essentially allow you to wrap another function or method and execute code before and/or after the wrapped function runs. Decorators are typically denoted by the @ symbol followed by the decorator function name, placed just above the function definition.

``` python
def logger(func):
  def wrapper(*args, **kwargs):
    print("running", func.__name__)
    return func(*args, **kwargs)
  return wrapper

@logger
def simulate()
  print("simulating . . . ")

with open("log.txt", "w") as file:
  file.write("run completed")
```
``` python
def my_decorator(func):
  def wrapper():
  print("Something is hapenning before the function is called.")
  func()
  print("something is hapenning after the function is called.")
return wrapper

@my_decorator
def say_hello():
  print("Hello!")

say_hello()
```
> decorator function that takes another function, func, as its argument. Inside of my_decorator, a nested function wrapper is defined. . . which wraps around the original function func. Inside wrapper, you can include code to be executed before and/or after calling func. Finally, the wrapper function is returned.

> when you decorate the say_hello function with @my_decorator, python essentially does this: say_hello = my_decorator(say_hello). So, when you call say_hello(), it actually calls the wrapper function created by my_decorator, which turn calls the original say_hello function within it.

# Some common decorators used 
  1. @property : used to define properties on calsses, allowing you to define getter, setter, and deleter methods for attributes.
  2. @classmethod : Declares a method within a class that takes the class itself as its first argument instead of the instance.
  3. @staticmethod : used to declare a method that belongs to the class but doesnt require access to the class or instance.
  4. @abstractmethod : used in abstract base classes to declare abstract methods, which must be implemented by subclasses.
  5. @wraps : a decorator from the functools module used to preserve the metadata of the original function when creating wrapper functions. This is particularly useful for maintaining docstrings, function name, and other attributes.
  6. @Iru_cache : a decorator from the functools module that caches the results of a function, saving time when the same inputs occur again.

### Dunder methods
Dunder methods, short for "double underscore" methods, are special methods in Python that have names surrounded by double underscores, like __init__, __repr__. __add__, etc. They are also called magic methods or special methods.

These methods allow classes to define specific behavior that gets invoked in response to cecrtain operations or interactions. For example, when you use the + operator with instance of a class, python looks for the add method to determine how to perform addition for those objects.

  - __init__(self, ...) : this constructor method that initializes a new instance of a class.
  - __repr__(self) : Method that returns a string representation of the object, used for debugging and logging.
  - __str__(self) : Method that returns a string representation of the object, used for informal representation to end-users.
  - __len__(self) : Method that returns the length of the object.
  - __getitem__(self, key) : Method that enables accessing elements of an object using square brackets, like obj[key].


# Iterators
an object that is used to iterate over iterable objects like listss, tuples, dicts, and sets. The python iterators object is initialized using the iter() method. it uses the next() method for iteration.
  * __iter__() : the iter() method is called for the initialization of an iterator



### Files, JSON, CSV
``` python
import json
import csv

data = {'temp': 100, 'pressure': 5}
with open("log.json", "w") as f:
  json.dump(data, f)

with open('data.csv', newline='') as f:
  reader = csv.reader(f)
  for row in reader:
    print(row)
```

### Numpy
``` python
import numpy as np

a = np.array([1, 2, 3])
b = np.linspace(0, 1, 5)
```

### Dot Product
``` python
np.dot(a, a) #scalar
np.matmul(A, B) #Matrix multiply
np.linalg.solve(A, b) #linear system
```

### Integral & ODE
``` python
from scipy.integrate import solve_ivp

def dydt(t, y):
  return [-0.5 * y[0]]

sol = solve_ivp(dydt, [0, 10], [100])
```

### Pandas 
``` python
import pandas as pd

df = pd.read_csv("file.csv")
df.head()
df['col'].mean()
df[df['col'] > 5]

# usually use this in Google Takeout analysis, trends and logs :D
```

### BONUS!~
``` python
import streamlit as st

st.title(Thermal simulation)
temp = st.slider("temperature", 100, 500)
st.write("selected:", temp)
```


### ASYNCIO
``` python
import asyncio

async def run():
  while True:
    print("Running . . . ")
    await asyncio.sleep(1)

asyncio.run(run())
# this is for websocket clients, voice command engines, or local llm system
```

