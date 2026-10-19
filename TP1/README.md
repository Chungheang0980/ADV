# Writing Clean and Readable Python

This guide introduces essential Python concepts, clean-code practices,
PEP 8 conventions, and practical debugging techniques. It is designed as a
quick reference for writing code that is easy to understand, test, and
maintain.

## 1. Core Python Concepts

Before focusing on style, it helps to understand the building blocks used in
most Python programs.

| Concept | Meaning | Example |
| --- | --- | --- |
| **Function** | A reusable block of code that performs a task. It can accept parameters and return a result. If it has no explicit `return`, it returns `None`. | `calculate_total(price, quantity)` |
| **Variable** | A name that refers to a value or object. The value associated with the name can change. | `student_score = 75` |
| **Method** | A function associated with a class or object. An instance method conventionally receives the object through `self`. | `student.greet()` |
| **Class** | A blueprint that defines the data and behavior shared by a group of objects. | `class Student:` |
| **Module** | A Python source file containing reusable functions, classes, or variables. | `math_helpers.py` |
| **Package** | A collection of related modules organized under a common name. Regular packages contain `__init__.py`; namespace packages can omit it. | `utilities.math_helpers` |
| **Constant** | A named value that is intended to remain unchanged. Python communicates this intention through uppercase naming rather than enforcing it. | `PASS_MARK = 50` |

### Class, object, and method example

```python
class Student:
    """Represent a student in a simple example."""

    def greet(self):
        """Return a greeting for the student."""
        return "Hello, welcome to class!"


student = Student()
print(student.greet())
```

In this example:

- `Student` is a class.
- `student` refers to an object, or instance, of that class.
- `greet()` is an instance method.
- Calling `student.greet()` automatically passes `student` as `self`.

## 2. What Makes Code Clean?

Clean code makes its purpose easy to recognize. A reader should be able to
understand what the program does without having to decode unclear names,
duplicated logic, or deeply nested conditions.

### Choose meaningful names

Names should describe the value or operation they represent.

```python
# Unclear
s = 75

# Clear
student_score = 75
```

Short names can still be useful when their meaning is obvious from a small
context, but descriptive names are usually better for important data and
reusable code.

### Give each function one clear responsibility

A function is easier to understand and test when it performs one focused task.
If a function handles several unrelated jobs, divide it into smaller helper
functions.

### Avoid repeated logic

Place repeated calculations or operations in a function. This reduces
duplication and allows future corrections to be made in one location.

### Replace unexplained values with named constants

```python
PASS_MARK = 50


def has_passed(score):
    return score >= PASS_MARK
```

`PASS_MARK` explains the role of `50` and makes the threshold easier to update.

### Explain decisions, not obvious syntax

Comments are most useful when they explain *why* a decision was made. Avoid
comments that merely repeat what a clear line of code already says, and update
comments whenever the related code changes.

### Document reusable code