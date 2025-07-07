# Detailed Python Notes

## 1. Installation of Python
Python is a versatile, high-level programming language. Here's how to install it:

- **Download**: Visit [python.org](https://www.python.org/downloads/) and download the latest version (e.g., Python 3.12 as of 2025).
- **Windows**:
  - Run the installer, check "Add Python to PATH" to enable command-line access.
  - Verify: Open Command Prompt and run `python --version` or `python3 --version`.
- **Mac**:
  - Install via the installer or use Homebrew: `brew install python`.
  - Verify: Open Terminal and run `python3 --version`.
- **Linux**:
  - Often pre-installed. Install via package manager, e.g., `sudo apt install python3` (Ubuntu).
  - Verify: Run `python3 --version`.
- **IDEs**: Use IDLE (included with Python), VS Code, PyCharm, or Jupyter Notebook.
- **Virtual Environments**: Use `python -m venv myenv` to create isolated environments, activated with `source myenv/bin/activate` (Linux/Mac) or `myenv\Scripts\activate` (Windows).

## 2. Type Annotations
Type annotations (introduced in PEP 484) enhance code readability and support static type checking with tools like `mypy`.

- **Syntax**:
  ```python
  age: int = 25
  name: str = "Alice"
  def greet(name: str) -> str:
      return f"Hello, {name}!"
  ```
- **Complex Types**: Use `List`, `Dict`, `Tuple`, `Set` from `typing` module.
  ```python
  from typing import List, Dict
  numbers: List[int] = [1, 2, 3]
  user: Dict[str, int] = {"age": 30}
  ```
- **Benefits**: Improves IDE support, catches type errors early, and documents code.
- **Note**: Annotations are optional and not enforced at runtime.

## 3. PEP 8
PEP 8 is Python's style guide for writing readable code.

- **Indentation**: Use 4 spaces per level, avoid tabs.
- **Line Length**: Maximum 79 characters (or 120 in modern practice).
- **Naming Conventions**:
  - Variables/functions: `snake_case` (e.g., `user_name`, `calculate_sum`).
  - Classes: `CamelCase` (e.g., `MyClass`).
  - Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_SIZE`).
- **Imports**:
  - One import per line, grouped as: standard library, third-party, local.
  - Example:
    ```python
    import os
    import numpy
    from my_module import my_function
    ```
- **Whitespace**:
  - Avoid extra spaces in expressions: `func(a, b)` not `func( a , b )`.
  - One blank line between functions, two between classes.
- **Tools**: Use `flake8`, `pylint`, or `black` for automatic formatting.

## 4. Variables
Variables in Python are dynamically typed and created upon assignment.

- **Assignment**: `variable_name = value`.
- **Naming Rules**:
  - Start with a letter or underscore.
  - Use letters, numbers, or underscores.
  - Case-sensitive: `age` ≠ `Age`.
- **Example**:
  ```python
  counter = 10
  user_name = "Bob"
  _private = 42  # Convention for private variables
  ```

## 5. Basic Data Types
Python supports several built-in data types:

- **int**: Whole numbers, unlimited size.
  ```python
  x = 42
  ```
- **float**: Decimal numbers, supports scientific notation.
  ```python
  y = 3.14
  z = 1.2e-3  # 0.0012
  ```
- **bool**: Logical values `True` or `False`.
  ```python
  is_active = True
  ```
- **str**: Text, enclosed in single (`'`) or double (`"`) quotes.
  ```python
  name = "Python"
  multiline = """Line 1
  Line 2"""
  ```

## 6. Conditionals: if, elif, else
Conditionals control program flow based on boolean expressions.

- **Syntax**:
  ```python
  age = 20
  if age >= 18:
      print("Adult")
  elif age >= 13:
      print("Teen")
  else:
      print("Child")
  ```
- **Logical Operators**: `and`, `or`, `not`.
  ```python
  if age >= 18 and age < 65:
      print("Working age")
  ```
- **Ternary Operator**:
  ```python
  status = "Adult" if age >= 18 else "Minor"
  ```

## 7. Loops: for and while
Loops allow repeated execution of code.

- **for loop**: Iterates over iterables (e.g., lists, tuples, `range`).
  ```python
  for i in range(5):  # 0, 1, 2, 3, 4
      print(i)
  for item in ["apple", "banana"]:
      print(item)
  ```
- **while loop**: Runs while a condition is true.
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
    ```python
    for i in range(5):
        if i == 3:
            break
        print(i)
    else:
        print("Loop completed")  # Skipped due to break
    ```

## 8. Data Types: List, Set, Dictionary, Tuple
### List
- Ordered, mutable sequence.
- Creation: `lst = [1, 2, 3]` or `lst = list()`.
- **Functions/Methods**:
  - `append(x)`: Add item to end.
  - `extend(iterable)`: Add multiple items.
  - `insert(i, x)`: Insert at index `i`.
  - `remove(x)`: Remove first occurrence of `x`.
  - `pop([i])`: Remove and return item at index `i` (default: last).
  - `clear()`: Remove all items.
  - `index(x)`: Return index of first `x`.
  - `count(x)`: Count occurrences of `x`.
  - `sort()`: Sort in place.
  - `reverse()`: Reverse in place.
  - `copy()`: Shallow copy.
  ```python
  lst = [1, 2, 2, 3]
  lst.append(4)        # [1, 2, 2, 3, 4]
  lst.remove(2)        # [1, 2, 3, 4]
  print(lst.pop())     # 4, lst = [1, 2, 3]
  print(lst.index(2))  # 1
  lst.sort()           # [1, 2, 3]
  ```

### Set
- Unordered, mutable, unique elements.
- Creation: `st = {1, 2, 3}` or `st = set([1, 2, 3])`.
- **Functions/Methods**:
  - `add(x)`: Add element `x`.
  - `update(iterable)`: Add multiple elements.
  - `remove(x)`: Remove `x` (raises KeyError if not found).
  - `discard(x)`: Remove `x` (no error if not found).
  - `pop()`: Remove and return arbitrary element.
  - `clear()`: Remove all elements.
  - `union(*others)`: Return union of sets.
  - `intersection(*others)`: Return intersection.
  - `difference(*others)`: Return difference.
  - `symmetric_difference(other)`: Return symmetric difference.
  - `issubset(other)`, `issuperset(other)`: Check subset/superset.
  ```python
  st = {1, 2, 3}
  st.add(4)            # {1, 2, 3, 4}
  st.discard(2)        # {1, 3, 4}
  st2 = {3, 4, 5}
  print(st.union(st2)) # {1, 3, 4, 5}
  print(st & st2)      # {3, 4} (intersection)
  ```

### Dictionary
- Key-value pairs, mutable, keys must be unique and hashable.
- Creation: `dct = {"key": "value"}` or `dct = dict(key="value")`.
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
  ```python
  dct = {"name": "Alice", "age": 25}
  print(dct.get("name"))  # Alice
  dct.update({"city": "NY"})  # {"name": "Alice", "age": 25, "city": "NY"}
  print(dct.keys())       # dict_keys(["name", "age", "city"])
  dct.pop("age")          # 25, dct = {"name": "Alice", "city": "NY"}
  ```

### Tuple
- Ordered, immutable sequence.
- Creation: `tpl = (1, 2, 3)` or `tpl = tuple([1, 2, 3])`.
- **Functions/Methods**:
  - `index(x)`: Return index of first `x`.
  - `count(x)`: Count occurrences of `x`.
  ```python
  tpl = (1, 2, 2, 3)
  print(tpl.count(2))  # 2
  print(tpl.index(3))  # 3
  ```
- Note: Immutable, so no add/remove methods. Use for fixed data.

## 9. User Functions and Lambda Functions
- **def**: Define reusable functions with optional parameters.
  ```python
  def add(a: int, b: int = 0) -> int:
      return a + b
  print(add(5, 3))  # 8
  print(add(5))     # 5 (uses default b=0)
  ```
- **Lambda**: Anonymous functions for short, single-use cases.
  ```python
  square = lambda x: x * x
  print(square(4))  # 16
  ```
- **Scope**: Variables defined in functions are local unless declared `global` or `nonlocal`.

## 10. map, filter, and List Comprehensions
- **map(function, iterable)**: Applies function to each item, returns iterator.
  ```python
  nums = [1, 2, 3]
  squares = list(map(lambda x: x * x, nums))  # [1, 4, 9]
  ```
- **filter(function, iterable)**: Keeps items where function returns `True`.
  ```python
  evens = list(filter(lambda x: x % 2 == 0, nums))  # [2]
  ```
- **List Comprehension**: Concise syntax for creating lists.
  ```python
  squares = [x * x for x in nums]               # [1, 4, 9]
  evens = [x for x in nums if x % 2 == 0]       # [2]
  matrix = [[i * j for j in range(3)] for i in range(3)]  # [[0, 0, 0], [0, 1, 2], [0, 2, 4]]
  ```

## 11. PIP Package Manager
PIP manages Python packages.

- **Install**: `pip install package_name` (e.g., `pip install requests`).
- **Upgrade**: `pip install --upgrade package_name`.
- **Uninstall**: `pip uninstall package_name`.
- **List Installed**: `pip list`.
- **Virtual Environments**: Use `pip` within activated virtual environments to isolate dependencies.
- **Requirements File**:
  ```bash
  pip freeze > requirements.txt
  pip install -r requirements.txt
  ```

## 12. External Library and File Systems
- **External Library Example** (using `requests`):
  ```python
  import requests
  response = requests.get("https://api.example.com")
  print(response.status_code)
  ```
  Install: `pip install requests`.
- **File Handling**:
  - Using `open`:
    ```python
    file = open("example.txt", "r")
    content = file.read()
    file.close()
    ```
  - Using `with` (preferred, auto-closes):
    ```python
    with open("example.txt", "w") as file:
        file.write("Hello, Python!")
    with open("example.txt", "r") as file:
        content = file.read()
        lines = file.readlines()  # List of lines
        line = file.readline()    # Single line
    ```
  - Modes: `"r"`, `"w"`, `"a"`, `"rb"`, `"wb"`, etc.
  - Write multiple lines:
    ```python
    with open("example.txt", "w") as file:
        file.writelines(["Line 1\n", "Line 2\n"])
    ```

## 13. Exception Handling
Handle errors gracefully using `try`, `except`, `else`, `finally`.

- **Syntax**:
  ```python
  try:
      result = 10 / 0
  except ZeroDivisionError as e:
      print(f"Error: {e}")
  except ValueError:
      print("Invalid value")
  else:
      print("No errors occurred")
  finally:
      print("Cleanup code")
  ```
- **Raising Exceptions**:
  ```python
  raise ValueError("Invalid input")
  ```
- **Custom Exceptions**:
  ```python
  class CustomError(Exception):
      pass
  try:
      raise CustomError("Something went wrong")
  except CustomError as e:
      print(e)
  ```