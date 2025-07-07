# Comprehensive Python Notes

## 1. Installation of Python
Python is a high-level, interpreted programming language. Installing it correctly is crucial for development.

- **Download**: Visit [python.org/downloads](https://www.python.org/downloads/) to get the latest version (e.g., Python 3.12 as of 2025).
- **Windows**:
  - Download the installer, run it, and check "Add Python to PATH" to enable command-line access.
  - Verify installation: Open Command Prompt and run:
    ```bash
    python --version
    ```
    Expected output: `Python 3.x.x`.
- **Mac**:
  - Use the installer from python.org or Homebrew:
    ```bash
    brew install python
    ```
  - Verify: In Terminal, run:
    ```bash
    python3 --version
    ```
- **Linux**:
  - Often pre-installed. Install via package manager, e.g., for Ubuntu:
    ```bash
    sudo apt update
    sudo apt install python3 python3-pip
    ```
  - Verify:
    ```bash
    python3 --version
    ```
- **Virtual Environments**: Isolate dependencies using:
  ```bash
  python -m venv myenv
  source myenv/bin/activate  # Linux/Mac
  myenv\Scripts\activate     # Windows
  ```
  Deactivate: `deactivate`.
- **IDEs**: Options include:
  - **IDLE**: Built-in, lightweight.
  - **VS Code**: Install Python extension.
  - **PyCharm**: Feature-rich, great for large projects.
  - **Jupyter Notebook**: Ideal for data science (`pip install jupyter`).

**Example**: Verify Python and create a virtual environment:
```bash
python3 --version
python3 -m venv myenv
source myenv/bin/activate
```

## 2. Type Annotations
Type annotations (PEP 484) specify variable and function types to improve code clarity and enable static type checking with tools like `mypy`.

- **Syntax**:
  - Variable: `variable_name: type = value`
  - Function: `def function_name(param: type) -> return_type:`
- **Basic Types**: `int`, `float`, `str`, `bool`.
- **Complex Types**: Use `typing` module for `List`, `Dict`, `Tuple`, `Set`, etc.
- **Optional Types**: Use `Optional[type]` for values that can be `None`.

**Examples**:
```python
# Basic annotations
age: int = 25
name: str = "Alice"

# Function annotation
def greet(name: str) -> str:
    return f"Hello, {name}!"

# Complex types
from typing import List, Dict, Optional
numbers: List[int] = [1, 2, 3]
user: Dict[str, str] = {"name": "Bob", "city": "NY"}
optional_value: Optional[int] = None

# Function with default and optional
def divide(a: float, b: float = 1.0) -> float:
    return a / b

print(greet("Alice"))  # Output: Hello, Alice!
print(divide(10.0, 2.0))  # Output: 5.0
```

**Notes**:
- Annotations are hints, not enforced at runtime.
- Use `mypy script.py` to check types statically.
- Install mypy: `pip install mypy`.

## 3. PEP 8
PEP 8 is Python’s style guide for consistent, readable code ([PEP 8](https://www.python.org/dev/peps/pep-0008/)).

- **Indentation**:
  - Syntax: Use 4 spaces per indentation level.
  - Avoid tabs.
  ```python
  def example():
      print("Indented with 4 spaces")
  ```
- **Line Length**:
  - Maximum 79 characters (or 120 in modern practice).
  - Break long lines using `\` or parentheses.
  ```python
  long_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, \
               11, 12]
  ```
- **Naming Conventions**:
  - Variables/functions: `snake_case`.
  - Classes: `CamelCase`.
  - Constants: `UPPER_SNAKE_CASE`.
  ```python
  user_name = "Alice"  # Variable
  def calculate_sum():  # Function
      pass
  class UserProfile:   # Class
      pass
  MAX_RETRIES = 5      # Constant
  ```
- **Imports**:
  - One import per line, grouped: standard library, third-party, local.
  - Syntax:
    ```python
    import os
    import sys
    import numpy as np
    from my_module import my_function
    ```
- **Whitespace**:
  - Avoid extra spaces in expressions.
  - Correct: `func(a, b)`, Incorrect: `func( a , b )`.
  - One blank line between functions, two between classes.
- **Tools**:
  - `flake8`: Linting for PEP 8 compliance (`pip install flake8`).
  - `black`: Auto-formatting (`pip install black`).
  ```bash
  black script.py
  flake8 script.py
  ```

**Example**:
```python
import math

def calculate_area(radius: float) -> float:
    return math.pi * radius ** 2

class Circle:
    def __init__(self, radius: float):
        self.radius = radius
```

## 4. Variables
Variables store data and are dynamically typed.

- **Syntax**: `variable_name = value`
- **Naming Rules**:
  - Start with letter or underscore (`_`).
  - Contain letters, numbers, underscores.
  - Case-sensitive: `age` ≠ `Age`.
  - Avoid reserved keywords (e.g., `if`, `for`, `class`).
- **Conventions**:
  - Use `snake_case` (PEP 8).
  - `_variable` for private variables (convention, not enforced).

**Examples**:
```python
# Basic assignment
count = 10
user_name = "Bob"
_price = 99.99  # Private by convention

# Multiple assignment
x, y, z = 1, 2, 3

# Swap variables
a, b = 5, 10
a, b = b, a  # a=10, b=5

print(count, user_name, _price, x, y, z, a, b)
```

## 5. Basic Data Types
Python’s core data types include:

- **int**: Whole numbers, no size limit.
  - Syntax: `x = 42`
- **float**: Decimal or scientific notation numbers.
  - Syntax: `y = 3.14` or `z = 1.2e-3`
- **bool**: Logical values `True` or `False`.
  - Syntax: `is_valid = True`
- **str**: Text, using single (`'`) or double (`"`) quotes.
  - Syntax: `name = "Python"` or `text = 'Hello'`

**Examples**:
```python
# Integer
count = 100
large_num = 12345678901234567890

# Float
pi = 3.14159
sci_not = 1.5e3  # 1500.0

# Boolean
is_active = True
is_empty = False

# String
greeting = "Hello, World!"
multiline = """Line 1
Line 2"""

# Operations
print(count + 50)      # 150
print(pi * 2)          # 6.28318
print(is_active and is_empty)  # False
print(greeting.upper())  # HELLO, WORLD!
```

## 6. Conditionals: if, elif, else
Conditionals execute code based on boolean conditions.

- **Syntax**:
  ```python
  if condition:
      # Code block
  elif another_condition:
      # Code block
  else:
      # Code block
  ```
- **Operators**:
  - Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`.
  - Logical: `and`, `or`, `not`.
  - Membership: `in`, `not in`.
  - Identity: `is`, `is not`.
- **Ternary Operator**:
  ```python
  result = value_if_true if condition else value_if_false
  ```

**Examples**:
```python
# Basic conditional
age = 20
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teen")
else:
    print("Child")

# Logical operators
if age >= 18 and age < 65:
    print("Working age")

# Membership and ternary
fruits = ["apple", "banana"]
if "apple" in fruits:
    print("Apple found")
status = "Adult" if age >= 18 else "Minor"
print(status)  # Adult
```

## 7. Loops: for and while
Loops repeat code execution.

- **for loop**:
  - Syntax: `for variable in iterable:`
  - Common iterables: `list`, `tuple`, `range`, `str`.
  ```python
  for i in range(5):  # 0, 1, 2, 3, 4
      print(i)
  for char in "Python":
      print(char)
  ```
- **while loop**:
  - Syntax: `while condition:`
  ```python
  count = 0
  while count < 5:
      print(count)
      count += 1
  ```
- **Control Statements**:
  - `break`: Exit loop.
  - `continue`: Skip to next iteration.
  - `else`: Runs if loop completes without breaking.
- **Nested Loops**:
  ```python
  for i in range(3):
      for j in range(2):
          print(f"i={i}, j={j}")
  ```

**Examples**:
```python
# for with range
for i in range(1, 6, 2):  # Start=1, stop=6, step=2 -> 1, 3, 5
    print(i)

# while with break
count = 0
while True:
    if count == 3:
        break
    print(count)
    count += 1

# for with else
for i in range(5):
    print(i)
else:
    print("Loop completed")  # Runs after loop
```

## 8. Data Types: List, Set, Dictionary, Tuple
### List
- Ordered, mutable sequence. Allows duplicates.
- Syntax: `lst = [item1, item2]` or `lst = list(iterable)`
- **Functions/Methods**:
  - `append(x)`: Add item to end.
  - `extend(iterable)`: Add multiple items.
  - `insert(i, x)`: Insert `x` at index `i`.
  - `remove(x)`: Remove first `x` (raises ValueError if not found).
  - `pop([i])`: Remove and return item at index `i` (default: last).
  - `clear()`: Remove all items.
  - `index(x)`: Return index of first `x`.
  - `count(x)`: Count occurrences of `x`.
  - `sort(key=None, reverse=False)`: Sort in place.
  - `reverse()`: Reverse in place.
  - `copy()`: Return shallow copy.
- **Slicing**: `lst[start:stop:step]`

**Examples**:
```python
lst = [1, 2, 2, 3]
lst.append(4)         # [1, 2, FU2, 3, 4]
lst.extend([5, 6])    # [1, 2, 2, 3, 4, 5, 6]
lst.insert(1, 7)      # [1, 7, 2, 2, 3, 4, 5, 6]
lst.remove(2)         # [1, 7, 2, 3, 4, 5, 6]
print(lst.pop())      # 6, lst = [1, 7, 2, 3, 4, 5]
print(lst.pop(1))     # 7, lst = [1, 2, 3, 4, 5]
print(lst.index(3))   # 2
print(lst.count(2))   # 1
lst.sort()            # [1, 2, 3, 4, 5]
lst.reverse()         # [5, 4, 3, 2, 1]
copy_lst = lst.copy() # [5, 4, 3, 2, 1]
print(lst[1:4])       # [4, 3, 2]
```

### Set
- Unordered, mutable, unique elements. No duplicates.
- Syntax: `st = {item1, item2}` or `st = set(iterable)`
- **Functions/Methods**:
  - `add(x)`: Add element `x`.
  - `update(iterable)`: Add multiple elements.
  - `remove(x)`: Remove `x` (raises KeyError if not found).
  - `discard(x)`: Remove `x` (no error if not found).
  - `pop()`: Remove and return arbitrary element.
  - `clear()`: Remove all elements.
  - `union(*others)` or `|`: Return union.
  - `intersection(*others)` or `&`: Return intersection.
  - `difference(*others)` or `-`: Return difference.
  - `symmetric_difference(other)` or `^`: Return symmetric difference.
  - `issubset(other)` or `<=`: Check if subset.
  - `issuperset(other)` or `>=`: Check if superset.
- **Frozenset**: Immutable set, created with `frozenset(iterable)`.

**Examples**:
```python
st = {1, 2, 3}
st.add(4)             # {1, 2, 3, 4}
st.update([5, 6])     # {1, 2, 3, 4, 5, 6}
st.discard(2)         # {1, 3, 4, 5, 6}
st.remove(3)          # {1, 4, 5, 6}
print(st.pop())       # Arbitrary element, e.g., 1
st2 = {5, 6, 7}
print(st.union(st2))  # {1, 4, 5, 6, 7}
print(st & st2)       # {5, 6}
print(st - st2)       # {1, 4}
print(st ^ st2)       # {1, 4, 7}
print(st.issubset({1, 4, 5, 6, 7}))  # True
fs = frozenset([1, 2])  # Immutable
```

### Dictionary
- Key-value pairs, mutable, keys must be unique and hashable.
- Syntax: `dct = {key1: value1, key2: value2}` or `dct = dict(key1=value1)`
- **Functions/Methods**:
  - `get(key[, default])`: Return value for key, or default if not found.
  - `setdefault(key[, default])`: Return value for key, set default if not found.
  - `update(other)`: Update with key-value pairs from another dict/iterable.
  - `pop(key[, default])`: Remove and return value for key.
  - `popitem()`: Remove and return last key-value pair.
  - `clear()`: Remove all items.
  - `keys()`: Return view of keys.
  - `values()`: Return view of values.
  - `items()`: Return view of key-value pairs.

**Examples**:
```python
dct = {"name": "Alice", "age": 25}
print(dct.get("name"))     # Alice
print(dct.get("city", "NY"))  # NY (default)
dct.setdefault("city", "LA")  # {"name": "Alice", "age": 25, "city": "LA"}
dct.update({"age": 26, "job": "Engineer"})  # Update age, add job
print(dct.pop("age"))      # 26, dct = {"name": "Alice", "city": "LA", "job": "Engineer"}
print(dct.popitem())       # ("job", "Engineer")
print(dct.keys())          # dict_keys(["name", "city"])
print(dct.values())        # dict_values(["Alice", "LA"])
print(dct.items())         # dict_items([("name", "Alice"), ("city", "LA")])
dct.clear()                # {}
```

### Tuple
- Ordered, immutable sequence. Allows duplicates.
- Syntax: `tpl = (item1, item2)` or `tpl = tuple(iterable)`
- **Functions/Methods**:
  - `index(x)`: Return index of first `x`.
  - `count(x)`: Count occurrences of `x`.
- Note: Immutable, so no add/remove methods.

**Examples**:
```python
tpl = (1, 2, 2, 3)
print(tpl.count(2))  # 2
print(tpl.index(3))  # 3
print(tpl[1:3])      # (2, 2)
single = (42,)       # Single-element tuple needs comma
```

## 9. User Functions and Lambda Functions
Functions encapsulate reusable code.

- **def**:
  - Syntax:
    ```python
    def function_name(parameters: type) -> return_type:
        # Code block
        return value
    ```
  - Supports default, positional, keyword, and variable-length arguments (`*args`, `**kwargs`).
- **lambda**:
  - Syntax: `lambda arguments: expression`
  - For short, single-expression functions.

**Examples**:
```python
# Defined function
def factorial(n: int) -> int:
    if n == 0:
        return 1
    return n * factorial(n - 1)

# Default and keyword arguments
def greet(name: str, greeting: str = "Hello") -> str:
    return f"{greeting}, {name}!"

# Variable-length arguments
def sum_all(*args: int) -> int:
    return sum(args)

# Lambda
square = lambda x: x * x

print(factorial(5))      # 120
print(greet("Alice"))    # Hello, Alice!
print(greet(name="Bob", greeting="Hi"))  # Hi, Bob!
print(sum_all(1, 2, 3))  # 6
print(square(4))         # 16
```

## 10. map, filter, and List Comprehensions
These tools process iterables efficiently.

- **map(function, iterable)**:
  - Syntax: `map(function, iterable)`
  - Applies function to each item, returns iterator.
- **filter(function, iterable)**:
  - Syntax: `filter(function, iterable)`
  - Keeps items where function returns `True`.
- **List Comprehension**:
  - Syntax: `[expression for item in iterable if condition]`
  - Concise alternative to loops.

**Examples**:
```python
nums = [1, 2, 3, 4]
# map
squares = list(map(lambda x: x * x, nums))  # [1, 4, 9, 16]
# filter
evens = list(filter(lambda x: x % 2 == 0, nums))  # [2, 4]
# List comprehension
squares_comp = [x * x for x in nums]  # [1, 4, 9, 16]
evens_comp = [x for x in nums if x % 2 == 0]  # [2, 4]
# Nested comprehension
matrix = [[i * j for j in range(3)] for i in range(3)]  # [[0, 0, 0], [0, 1, 2], [0, 2, 4]]

print(squares, evens, squares_comp, evens_comp, matrix)
```

## 11. PIP Package Manager
PIP installs and manages Python packages.

- **Syntax**:
  ```bash
  pip install package_name  # Install
  pip install package_name==version  # Specific version
  pip install --upgrade package_name  # Upgrade
  pip uninstall package_name  # Uninstall
  pip list  # List installed packages
  ```
- **Requirements File**:
  - Export: `pip freeze > requirements.txt`
  - Install: `pip install -r requirements.txt`
- **Virtual Environments**: Use PIP within activated virtual environments.

**Example**:
```bash
pip install requests
pip list
pip freeze > requirements.txt
```

## 12. External Library and File Systems
- **External Library Example** (using `requests`):
  - Install: `pip install requests`
  - Syntax:
    ```python
    import requests
    response = requests.get("https://api.example.com")
    print(response.status_code, response.json())
    ```
- **File Handling**:
  - **open**: `open(file, mode)`
  - **with**: Preferred, auto-closes file.
  - Modes: `"r"` (read), `"w"` (write), `"a"` (append), `"rb"` (read binary), `"wb"` (write binary).
  - Methods: `read()`, `readline()`, `readlines()`, `write()`, `writelines()`.

**Examples**:
```python
# Using open
file = open("example.txt", "w")
file.write("Hello, Python!\n")
file.close()

# Using with
with open("example.txt", "a") as file:
    file.write("Second line\n")

with open("example.txt", "r") as file:
    content = file.read()        # Entire content
    file.seek(0)                 # Reset cursor
    lines = file.readlines()     # List of lines
    file.seek(0)
    first_line = file.readline() # First line

print(content)
print(lines)
print(first_line)
```

## 13. Exception Handling
Handle errors to prevent crashes.

- **Syntax**:
  ```python
  try:
      # Code that might raise an exception
  except ExceptionType as e:
      # Handle specific exception
  except AnotherExceptionType:
      # Handle another exception
  else:
      # Run if no exception
  finally:
      # Always run
  ```
- **Raising Exceptions**: `raise ExceptionType("message")`
- **Custom Exceptions**:
  ```python
  class CustomError(Exception):
      pass
  ```

**Examples**:
```python
# Basic exception handling
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
else:
    print("Division successful")
finally:
    print("Cleanup")

# Multiple exceptions
try:
    num = int("abc")
except ValueError:
    print("Invalid number")
except TypeError:
    print("Type error")

# Raising exception
try:
    age = -5
    if age < 0:
        raise ValueError("Age cannot be negative")
except ValueError as e:
    print(e)

# Custom exception
try:
    raise CustomError("Custom error occurred")
except CustomError as e:
    print(e)
```