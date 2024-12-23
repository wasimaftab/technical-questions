# Python questions

## Question 1
1. What is the type of the data of `items` 
2. What is the issue of this code?
```python
items = (1, 2, 3)
items[0] = 10
print(items)
```

## Question 2
What is the issue of this code?
```python
records = {'A': 1, 'B': 2, 'C': 3}
for key, value in records:
    print(key, value)
```

## Question 3
Predict the output of the following code
```python
numbers = [x**2 for x in range(1, 6)]
print(len(numbers))
print(numbers)
```

## Question 4
You need to get the BRCA1 gene coordinate from Ensembl.
A colleague has given you the following code which queries Ensembl REST API to get the coordinate information.

```python
import requests

class EnsemblClient:
    def __init__(self):
        self.base_url = "https://rest.ensembl.org"

    def __call__(self, gene_name):
        endpoint = f"{self.base_url}/lookup/symbol/homo_sapiens/{gene_name}"
        headers = {"Content-Type": "application/json"}

        response = requests.get(endpoint, headers=headers)
        response.raise_for_status()  # Raise an exception for HTTP errors

        data = response.json()
        return data["start"], data["end"]
```

How can you use this class to get the BRCA1 gene start and end coordinates?


## Question 5
Below is the directory structure from your current working directory (CWD).  

```bash
# Directory structure:
# .
# ├── module.py
# ├── package/
# │   ├── __init__.py
# │   ├── module2.py
```

After initiating a Python3 interpreter from your CWD:
1. How do you import `module.py`?
2. You want to import a `helper` object inside `module2.py`. How do you import it?


## Question 6
With the import statement, it is common to use `*` to import all objects from a module.
```python
from math import *
```
Why might this be a bad idea?

## Question 7
You find this directory
```python
# .
# ├── xyz/
# │   ├── module1.py
# │   └── module2.py
# └── setup.py

# setup.py:
from setuptools import setup

setup(
    name="xyz",
    version="0.1",
    packages=["xyz"]
)
```
1. What is the purpose of `setup.py`?
2. After understanding what the purpose of `setup.py` is, do you notice issue with the directory structure?
3. Is there anything else you would change to follow best practices?


## Question 8
You try to install a python package by running `pip install example_package` and you get the following error:
```bash
ERROR: Could not find a version that satisfies the requirement numpy>=1.21.0 (from example_package==0.1) (from versions: 1.19.5, 1.20.0, 1.20.3)
ERROR: No matching distribution found for numpy>=1.21.0
```
Describe the issue, and explain how you might resolve the issue.

## Question 9
You try to install a python package by running `pip install example_package` and you get the following error:
```bash
ERROR: Failed building wheel for example_package
  Building wheel for example_package (pyproject.toml) ... error
  ERROR: Command errored out with exit status 1:
   command: /usr/bin/python3.8 -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-abc123/example_package/setup.py'"'"'; __file__='"'"'/tmp/pip-install-abc123/example_package/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' bdist_wheel -d /tmp/pip-wheel-def456
       cwd: /tmp/pip-install-abc123/example_package/
  Complete output (15 lines):
  running bdist_wheel
  running build
  running build_ext
  building 'example_package.module' extension
  gcc -pthread -B /usr/bin -Wno-unused-result -Wsign-compare -DNDEBUG -g -fwrapv -O3 -Wall -fPIC -I/usr/include/python3.8 -c example_package/module.c -o build/temp.linux-x86_64-3.8/example_package/module.o
  example_package/module.c: In function 'example_function':
  example_package/module.c:12:5: error: 'EXAMPLE_CONSTANT' undeclared (first use in this function)
      12 |     printf(EXAMPLE_CONSTANT);
         |     ^~~~~~~~~~~~~~
  error: command 'gcc' failed with exit status 1
  ----------------------------------------
ERROR: Could not build wheels for example_package, which is required to install pyproject.toml-based projects
```

Describe the issue, and explain how you might resolve the issue.

## Question 10
You are approached by a colleague who says:

> "I wrote this script, and it runs fine on my computer, but when I tried running it on our institute server, it throws an error and doesn't work. Can you help me figure out what’s wrong? Here’s the code and the error message I’m seeing."  

**Code**
```python
data = [1, 2, 3, 4, 5]

if (n := len(data)) > 3:
    print(f"Data has {n} elements.")
```
**Error message on the institute server**
```bash
  File "script.py", line 3
    if (n := len(data)) > 3:
           ^
SyntaxError: invalid syntax
```
What might be the cause of the issue? Why would this script run fine on the colleague's computer but not on the institute server?


## Question 11
A colleague approaches you and says:
> "I was reviewing a script written by another team member, and I don’t understand some parts of it. It has these strange annotations in the function definitions. I've never seen these before. Can you help me figure out what they mean and if they’re necessary?"  

**Code**  
```python
from typing import List, Optional
                            # What are these List[int] and -> Optional[float]?
def calculate_average(numbers: List[int]) -> Optional[float]:
    if not numbers:
        return None
    return sum(numbers) / len(numbers)

# And what does `result: float` mean? how does this not raise an error? 
result: float = calculate_average([10, 20, 30])
print(f"The average is: {result}")
```
1. How would you explain to your colleague what these annotations are?
2. In this specific context, describe what these annotations mean

