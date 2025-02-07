# Python questions

## Question 1
1. What is the type of the data of `items` 
2. What is the issue of this code?
```python
items = (1, 2, 3)
items[0] = 10
print(items)
```
> 1. tuple
> 2. In python, tuples are immutable.
> - Convert the tuple to a list.
> - Modify the list.
> - Convert it back to a tuple.

## Question 2
What is the issue of this code?
```python
records = {'A': 1, 'B': 2, 'C': 3}
for key, value in records:
    print(key, value)
```
> To iterate through dictionary key-value pairs, use the items() method.
> 
> for key, value in records.items(): print(key, value)

## Question 3
Predict the output of the following code
```python
numbers = [x**2 for x in range(1, 6)]
print(len(numbers))
print(numbers)
```
> 5
> 
>[1, 4, 9, 16, 25]

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
```
# Create an instance of the class
client = EnsemblClient()

# Call the instance with "BRCA1"
brca1_start, brca1_end = client("BRCA1")  

print(f"BRCA1 start: {brca1_start}, end: {brca1_end}")    
```


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

```
1. import module as mdl
2. from package.module2 import helper_obj
```


## Question 6
With the import statement, it is common to use `*` to import all objects from a module.
```python
from math import *
```
Why might this be a bad idea?
> This will import all the functions, objects, etc. defined in math library which might overwrite the functions with the same name from other modules or a user-defined function and it will be hard to keep track of that. So it is important to import specific functions to avoid variable space pollution.

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
```
1. Defines the package for installation (pip install .).
2. Missing xyz/__init__.py, so xyz/ isn’t a valid package.
3. Add install_requires, README.md, MANIFEST.in.
```


## Question 8
You try to install a python package by running `pip install example_package` and you get the following error:
```bash
ERROR: Could not find a version that satisfies the requirement numpy>=1.21.0 (from example_package==0.1) (from versions: 1.19.5, 1.20.0, 1.20.3)
ERROR: No matching distribution found for numpy>=1.21.0
```
Describe the issue, and explain how you might resolve the issue.
```
Issue:
The error occurs because example_package requires numpy>=1.21.0,
but pip cannot find this version in the available package index. This is likely due to:

1. An outdated pip, preventing it from fetching the latest versions.
    Solution: `pip install --upgrade` and then `pip setuptools wheel`
2. An incompatible Python version (e.g., Python 3.6 instead of 3.7+).
    Solution: manually install older numpy, e.g., `pip install numpy==1.20.3` and then `pip install example_package`
3. A virtual environment or system dependency conflict.
    Solution: Use a clean virtual environment, it helps to isolate dependencies and ensure that pip can fetch the latest versions.
```

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
```
The error arises due to a missing constant (EXAMPLE_CONSTANT) while compiling example_package/module.c which might point to missing header files, and dependencies.
So, I would try installing the dependencies such as build-essential, python3-dev etc. and then attempt the installation
```

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
```
:= is an operator introduced in Python 3.8, which allows the assignment of variables within expressions. So, the like scenario is that colleague's pc has Python version >=3.8,
and the institute server's Python version is <3.8 installed.
```


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


## Question 12
A colleague is working on a Python class to manage genomic variants for different projects in a research institute. They write a class that keeps track of a list of variants for each project. However, when they create separate instances of the class for different projects, the variants from one project appear in another project’s list, which is not the expected behavior. The colleague comes to you for help.
```python
class VariantManager:
    def __init__(self, variants=[]):
        self.variants = variants

    def add_variant(self, variant):
        self.variants.append(variant)

# Manager for Project A
manager_a = VariantManager()
manager_a.add_variant({"id": "rs123", "position": 100, "gene": "Gene1"})

# Manager for Project B
manager_b = VariantManager()
manager_b.add_variant({"id": "rs456", "position": 200, "gene": "Gene2"})

# Print variants for each project
print("Project A variants:", manager_a.variants)
print("Project B variants:", manager_b.variants)
```
Output:
>```python
>Project A variants: [{'id': 'rs123', 'position': 100, 'gene': 'Gene1'}, {'id': 'rs456', 'position': 200, 'gene': 'Gene2'}]
>Project B variants: [{'id': 'rs123', 'position': 100, 'gene': 'Gene1'}, {'id': 'rs456', 'position': 200, 'gene': 'Gene2'}]
>```

- Why are the variants for `manager_a` and `manager_b` shared across both projects?
- How would you advise your colleague to fix the issue?


## Question 13
You received a JSON file from a colleague that contains all the variants you need to analyse in a 2Kbp window (1Kbp up and downstream of the variant).  
The JSON file only contains the position of the variant, and so you need to compute the 2Kbp window yourself for all variants. So you write the following code and run it:
```python
import json

with open('variants.json', 'r') as f:
    json_data = json.load(f)

windows = dict()
for variant, val in json_data.items():
    windows[variant] = '{}:{}-{}'.format(val['chromosome'], val['position']-1000, val['position']+1000)
```
But when you run the code, you get the following error:
```python
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[1], line 3
      1 windows = dict()
      2 for variant, val in json_data.items():
----> 3     windows[variant] = '{}:{}-{}'.format(val['chromosome'], val['position']-1000, val['position']+1000)

TypeError: unsupported operand type(s) for -: 'str' and 'int'
```
- What might be the issue? What is the simplest way to fix it?
- The `variant.json` file is in the same directory as this README file.


## Question 14

A colleague is writing a script to keep track of the total number of processed variants in a genomic dataset. They use a global variable to track the count, but the script doesn't produce the expected results. They ask for your help to debug the issue.

```python
# Global variable to track the total number of processed variants
total_variants = 0

def process_variant(variant_id):
    # Increment the global variable for each processed variant
    total_variants += 1
    print(f"Processed variant: {variant_id}, Total so far: {total_variants}")

# Process a few variants
process_variant("rs123")
process_variant("rs456")
process_variant("rs789")

print(f"Total variants processed: {total_variants}")
```

Error message
```
UnboundLocalError: local variable 'total_variants' referenced before assignment
```

- Why does the script raise an `UnboundLocalError`?
- How would you advise the colleague to re-write their script?

