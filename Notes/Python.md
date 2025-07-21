



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
|   &      | bitwise AND |bitwise OR|  

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

