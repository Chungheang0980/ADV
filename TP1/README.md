# Python Fundamentals, Clean Code, and PEP 8

## 1. Introduction

This section explains several common terms used in Python programming.

### Function

A **function** is a reusable section of code created to complete a particular
task. It may receive information through parameters and send a result back to
the caller.

For instance, `calculate_total(price, quantity)` could calculate the cost of
multiple items. Using a function means that the same calculation does not need
to be rewritten in different parts of the program. When a function finishes
without an explicit return value, Python returns `None`.

### Variable

A **variable** is a name that points to a value or object. Variables make it
possible to access and work with data. The value connected to a variable name
can also be replaced later.

```python
student_score = 75
```

Here, the name `student_score` refers to the value `75`.

### Method

A **method** is a function that belongs to a class or an object. An instance
method represents an action that an object can perform. Its first parameter
receives the object itself and is traditionally named `self`.

### Class

A **class** acts as a blueprint for producing objects with shared structure and
behavior. It can contain attributes that store data and methods that describe
actions. An object made from a class is known as an **instance** of that class.

### Module

A **module** is a Python source file that stores code such as variables,
functions, and classes. Other files can import and reuse that code. For
example, a file named `math_helpers.py` could contain several calculation
functions.

### Package

A **package** organizes related modules into a group. A package called
`utilities`, for example, might contain a module called `math_helpers`. Its
dotted import name would be `utilities.math_helpers`.

Regular packages include an `__init__.py` file, while namespace packages are
allowed to omit it.

### Constant

A **constant** is a named value that is intended to remain unchanged while a
program is running. Python does not prevent an ordinary constant from being
reassigned, so programmers communicate this intention through a naming
convention.

```python
PASS_MARK = 50
```

The uppercase name shows that `PASS_MARK` should be treated as a fixed value.

### How classes, objects, and methods relate

The following example demonstrates the relationship between these concepts:

```python
class Student:
    """Represent a student in a simple example."""

    def greet(self):
        """Return a greeting for the student."""
        return "Hello, welcome to class!"


student = Student()
print(student.greet())
```

In this code, `Student` is the class, `student` refers to an instance of that
class, and `greet()` is an instance method. Calling the method through
`student` passes that object to the method as `self`.

## 2. Clean Code, PEP 8, and Debugging

### 2.1 Clean Code Principles

Clean code clearly communicates what it is meant to do. It should also be easy
for another programmer to read, update, and maintain.

#### Select descriptive names

Names such as `student_score` and `calculate_average` help explain the data or
operation they represent. Short names can still be suitable when their meaning
is obvious within a small context.

#### Give a function a clear purpose

When a long function combines unrelated tasks, separate it into smaller helper
functions. Each part then becomes easier to understand and test on its own.

#### Reuse common logic

Move repeated calculations or operations into functions. If the logic needs to
be corrected later, the change can then be made in one place.

#### Give changeable values meaningful names

A constant such as `PASS_MARK` makes a grading limit easier to identify and
change than a number repeated throughout the code.

#### Use comments to describe decisions

Comments should explain the reason for a difficult or unexpected step. They
should also be kept accurate when the code is updated.

#### Add documentation to reusable code

A **docstring** is a string literal placed as the first statement in a module,
class, or function. It should summarize the code's purpose and describe useful
details about inputs, outputs, and expected errors.

PEP 257 recommends using triple double quotes, beginning with a clear sentence,
and ending that sentence with a period.

#### Keep the control flow straightforward

An early return, which is also called a **guard clause**, can deal with a
special case before the main calculation begins. This approach can reduce
unnecessary nesting.

The next function documents its result and handles an empty list before trying
to calculate an average:

```python
def calculate_average(scores):
    """Return the mean score, or None if no scores are available."""
    if not scores:
        return None
    return sum(scores) / len(scores)


print(calculate_average([60, 80, 100]))
print(calculate_average([]))
```

The two outputs are `80.0` and `None`. The early return avoids division by zero
when the list is empty, while leaving the main calculation easy to read.

### 2.2 PEP 8 Guidelines

PEP 8 is the style guide for Python. It contains conventions that support
consistent, readable code and make programs easier to review and maintain. A
project's chosen conventions should be followed consistently.

| Rule | Guidance |
| --- | --- |
| **Indentation** | Use four spaces for each level in new code. Align wrapped elements or apply a clear hanging indent to continuation lines. |
| **Line length** | Code lines are normally limited to 79 characters, while comments and docstrings are normally limited to 72. |
| **Imports** | Put imports after module comments or docstrings and before constants. Separate standard-library, third-party, and local imports with blank lines. Do not use wildcard imports. |
| **Naming** | Write variables, functions, and methods in `snake_case`; constants in `UPPER_CASE`; and classes in `PascalCase`. |
| **Whitespace** | Add spaces around assignment and comparison operators, and use spacing that keeps arithmetic readable. Do not put unnecessary spaces inside delimiters or before the `(` in a function call. |
| **Commas and colons** | Write `[60, 80]` and `{"score": 80}`. Slice notation follows a different pattern: `scores[1:3]`. |
| **Blank lines** | Leave two blank lines between top-level functions or classes and one blank line between methods. |
| **Wrapped expressions** | Use parentheses when wrapping expressions. For new code, prefer placing a break before a binary operator. |
| **Quotes** | Keep string quotation marks consistent. Triple double quotes are conventionally used for docstrings. |

Separate modules should usually be imported on separate lines:

```python
import math
import logging
```

Several names may be imported from one module on the same line:

```python
from math import ceil, floor
```

For default parameters, write `port=8080` when no annotation is present and
`port: int = 8080` when the parameter has a type annotation. A keyword argument
is written as `connect(port=8080)`.

The following example brings several conventions together:

```python
PASS_MARK = 50


def has_passed(score):
    return score >= PASS_MARK


student_score = 75
print(has_passed(student_score))
```

This code uses meaningful names, a constant, four-space indentation, and
consistent spacing. It displays `True` because the student's result reaches
the required pass mark.

### 2.3 Useful Python Idioms

#### Test for a missing value by identity

Use `result is None` or `result is not None` when checking for `None`.

#### Test collections directly

Use `if not scores:` when a list is empty and `if scores:` when it contains
items. Empty strings, tuples, and dictionaries are also treated as false in a
condition.

#### Use Boolean values without a comparison

If `has_passed` already contains a Boolean value, write `if has_passed:` or
`if not has_passed:`. Comparing it with `True` or `False` is unnecessary.

### 2.4 Debugging and Error Handling

**Debugging** is the process of locating the cause of an error and fixing it.
A program may contain invalid syntax, raise an exception while running, or
produce the wrong result even though it runs successfully.

For example:

- `TypeError` can signal that incompatible types were used.
- `KeyError` can indicate that a dictionary key is missing.
- `IndexError` can mean that a sequence index is invalid.

A useful debugging routine contains the following steps:

1. **Reproduce the problem.** Run the program with the input that originally
   caused the unexpected behavior.
2. **Study the error message.** For an exception, the final line gives the
   error type and message. The traceback identifies the relevant calls and
   locations.
3. **Narrow the search.** Inspect the reported line together with its variable
   values, types, and conditions. Test a small function separately with known
   inputs before returning to the full program.
4. **Correct the cause.** Make a focused change that addresses the reason for
   the failure.
5. **Test once more.** Repeat the original case and try additional inputs to
   confirm that the correction works without creating another problem.

Several tools can support this process:

- **Temporary output:** `print()` can reveal a value quickly during a small
  investigation. Temporary messages should be removed once they are no longer
  useful.
- **Logging:** Python's `logging` module can record events using the `DEBUG`,
  `INFO`, `WARNING`, `ERROR`, and `CRITICAL` levels. Changing the configured
  level controls which messages are displayed without requiring the logging
  calls to be deleted.
- **Breakpoints:** `breakpoint()` normally starts Python's `pdb` debugger at
  that location. It can be used to inspect variables and move through the
  program one step at a time.
- **Specific exception handling:** Expected exceptions should be caught by
  name. A bare `except:` also catches events such as `KeyboardInterrupt` and
  `SystemExit`, which may hide a problem or prevent an intended exit.

Converting text into an integer, for example, may raise `ValueError`. The code
below responds to that expected input problem:

```python
raw_score = "eighty"

try:
    score = int(raw_score)
except ValueError:
    print("Enter a whole-number score.")
else:
    print(f"Score: {score}")
```

Run the example once with `"eighty"` and once with `"80"` to test both the
error path and the success path. **Error handling** determines how a program
responds to an expected problem, whereas **debugging** is used to identify and
correct the cause of unexpected behavior.

## 3. Tips and Tricks to Help Code Follow PEP 8

### 3.1 Daily Coding Habits

- Set the editor to insert four spaces and display a guide for line length.
- Use formatting and linting feedback regularly instead of postponing every
  style correction until the activity is complete.
- Check names, comments, and docstrings manually. Prose comments should use
  complete sentences, but an identifier's original spelling should be kept
  when it appears at the beginning of a sentence.
- Test small functions while developing them. Include normal input, empty
  collections, and boundary values such as a score exactly equal to the pass
  mark.
- After making a change, rerun the relevant examples or tests to confirm the
  behavior.

### 3.2 Formatting and Linting with Ruff

Ruff includes a formatter that manages code layout and a linter that reports
problems covered by the enabled rules.

Install Ruff in an active Python virtual environment:

```bash
python -m pip install ruff
```

| Command | Purpose |
| --- | --- |
| `ruff check .` | Find lint issues in the current project. |
| `ruff check --fix .` | Apply the safe corrections available under the enabled rules. |
| `ruff format .` | Format the code. |
| `ruff format --check .` | Check the formatting without modifying any files. |

Ruff uses a default line length of 88 characters. A Python project that follows
the 79-character convention can include this example configuration in
`pyproject.toml`:

```toml
[tool.ruff]
line-length = 79

[tool.ruff.lint]
extend-select = ["I", "N", "E501"]
```

In this configuration, `I` turns on import-sorting checks, `N` enables naming
checks, and `E501` checks for lines that are too long. Import ordering is
handled through lint rules, while the formatter manages the code layout.

The formatter attempts to wrap long lines, but some cases still need to be
edited manually. The meaning and clarity of names, comments, and docstrings
also require human review.

### 3.3 Editor Integration

An editor integration, such as the Ruff extension for Visual Studio Code, can
display lint diagnostics during editing and format code when a file is saved.
The editor and command line should use the same project configuration so their
results remain consistent.

## 4. References

- Personal class notes and a classmate's lecture summary for TP1
- PEP 8: Style Guide for Python Code
- PEP 257: Docstring Conventions
- Python Tutorial: Classes
- Python Tutorial: Modules and Packages
- Python Tutorial: Errors and Exceptions
- Python Logging HOWTO
- Python Built-in Functions: `breakpoint`
- Ruff documentation: Formatter, Linter, and Configuration
