    pass
```

Keyword arguments do not use spaces around `=`:

```python
connect(port=8080)
```

### Complete style example

```python
PASS_MARK = 50


def has_passed(score):
    return score >= PASS_MARK


student_score = 75
print(has_passed(student_score))
```

This example uses a meaningful constant, descriptive names, four-space
indentation, blank lines, and consistent spacing. It prints `True` because the
score meets the pass mark.

## 4. Useful Python Idioms

Python provides concise ways to express common conditions.

### Check for `None` with identity

```python
if result is None:
    print("No result is available.")
```

Use `is None` or `is not None` instead of equality comparisons.

### Check collections directly

```python
if not scores:
    print("No scores are available.")
```

Empty strings, lists, tuples, and dictionaries are false in a condition.
Non-empty collections are true.

### Use Boolean values directly

```python
if has_passed:
    print("Pass")

if not has_passed:
    print("Try again")
```

There is usually no need to compare a Boolean value with `True` or `False`.

## 5. Debugging and Error Handling

Debugging means finding the cause of unexpected behavior and correcting it.
Python problems generally fall into three groups:

- **Syntax errors:** the code does not follow Python's grammar.
- **Runtime errors:** the program raises an exception while running.
- **Logic errors:** the program runs but produces the wrong result.

Common exceptions include:

| Exception | Typical cause |
| --- | --- |
| `TypeError` | An operation receives an incompatible type. |
| `KeyError` | A requested dictionary key does not exist. |
| `IndexError` | A sequence index is outside the valid range. |
| `ValueError` | A value has the correct general type but an invalid form. |

### A practical debugging workflow

1. **Reproduce the problem.** Run the program with the input that caused the
   unexpected result.
2. **Read the error carefully.** The final line normally shows the exception
   type and message, while the traceback identifies relevant calls and files.
3. **Reduce the search area.** Inspect the reported line, variable values,
   types, and conditions. Test a small function independently when possible.
4. **Correct the cause.** Make a focused change based on the evidence.
5. **Test again.** Retry the original case, then test normal, empty, and
   boundary inputs to check for regressions.

### Helpful debugging tools

- **Temporary output:** use `print()` to inspect values during a small
  investigation, then remove temporary messages when finished.
- **Logging:** use the `logging` module to record events at `DEBUG`, `INFO`,
  `WARNING`, `ERROR`, or `CRITICAL` level.
- **Breakpoints:** call `breakpoint()` to open the standard debugger, inspect
  variables, and step through the program.
- **Specific exception handling:** catch only the exceptions the program can
  handle meaningfully. A bare `except:` can hide important events such as
  `KeyboardInterrupt` and `SystemExit`.

### Error-handling example

```python
raw_score = "eighty"

try:
    score = int(raw_score)
except ValueError:
    print("Enter a whole-number score.")
else:
    print(f"Score: {score}")
```

Try the example with both `"eighty"` and `"80"` to test the error and success
paths. Error handling describes how the program responds to an expected
problem; debugging is the process of finding and fixing an unexpected one.

## 6. Habits That Improve Code Quality

- Configure the editor to insert four spaces and display a line-length guide.
- Format and lint code regularly instead of postponing all cleanup.
- Review names, comments, and docstrings manually; automated tools cannot
  judge whether an explanation is genuinely clear.
- Use complete sentences in prose comments while preserving the exact spelling
  of identifiers.
- Test small functions as they are written.
- Include normal, empty, and boundary cases, such as a score equal to the pass
  mark.
- Rerun relevant examples or tests after every behavioral change.

## 7. Formatting and Linting with Ruff

[Ruff](https://docs.astral.sh/ruff/) includes a formatter for code layout and a
linter for identifying issues covered by enabled rules.

Install Ruff in an activated Python virtual environment:

```bash
python -m pip install ruff
```

Useful commands:

| Command | Purpose |
| --- | --- |
| `ruff check .` | Report lint problems in the current project. |
| `ruff check --fix .` | Apply safe automatic fixes for enabled rules. |
| `ruff format .` | Format the project's Python files. |
| `ruff format --check .` | Check formatting without changing files. |

Ruff's formatter defaults to a line length of 88 characters. A project that
uses the 79-character convention can add the following configuration to
`pyproject.toml`:

```toml
[tool.ruff]
line-length = 79

[tool.ruff.lint]
extend-select = ["I", "N", "E501"]
```

In this example:

- `I` enables import-sorting checks.
- `N` enables naming checks.
- `E501` reports lines that exceed the configured length.

The formatter handles layout, while lint rules detect issues such as import
order and naming. Some long lines still need manual editing, and human review
is always needed for meaningful names, comments, and docstrings.

### Editor integration

An editor integration, such as the Ruff extension for Visual Studio Code, can
show lint feedback while you type and format files when you save. Use the same
project configuration in the editor and command line so both produce
consistent results.

## 8. Final Checklist

Before considering a Python task complete, ask:

- Are names descriptive and consistent?
- Does each function have one clear responsibility?
- Has repeated logic been moved into reusable functions?
- Are important fixed values represented by named constants?
- Do comments explain decisions rather than repeat the code?