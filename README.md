<p align="center">
<a href="https://github.com/sashsinha/typed_input"><img alt="Typed Input Logo" src="https://raw.githubusercontent.com/sashsinha/typed_input/main/logo.png"></a>
</p>

<h1 align="center">Typed Input</h1>

<h3 align="center">Effortless type-safe user input for integers, floats, dates, and more...</h3>

<br/>

<p align="center">
<a href="https://raw.githubusercontent.com/sashsinha/typed_input/main/LICENCE"><img alt="License: MIT" src="https://raw.githubusercontent.com/sashsinha/typed_input/main/license.svg"></a>
<a href="https://pypi.org/project/typed-input/"><img src="https://img.shields.io/badge/platform-windows%20%7C%20linux%20%7C%20macos-lightgrey" alt="Supported Platforms"></a>
<a href="https://pypi.org/project/typed-input/"><img 
alt="PyPI Supported Versions" src="https://img.shields.io/pypi/pyversions/typed-input.svg"></a>
<a href="https://pypi.org/project/typed-input/"><img alt="PyPI" src="https://img.shields.io/pypi/v/typed-input"></a>
<a href="https://pypi.org/project/typed-input/"><img alt="PyPI Status" src="https://img.shields.io/pypi/status/typed-input"></a>
<a href="https://pepy.tech/project/typed-input"><img alt="Downloads" src="https://pepy.tech/badge/typed-input"></a>
</p>

### Installation

#### PyPI
```
pip install typed-input
```

#### [`uv`](https://github.com/astral-sh/uv)
```
uv add typed-input
```


### Supported Functions:
- [`int_input`](#int_input-for-validated-integer-input)
- [`float_input`](#float_input-for-validated-floating-point-input)
- [`decimal_input`](#decimal_input-for-validated-decimal-input)
- [`datetime_input`](#datetime_input-for-validated-datetime-input)

Each function has this structure:

```python
<type>_input(
  prompt: str | None = None,
  min_value: <type> | None = None,
  max_value: <type> | None = None,
  default_value: <type> | None = None,
  type_error_message: str | None = None,
) -> <type>
```

#### Parameters:
- **`prompt`**: *(Optional)* Message displayed to the user when prompting for input.
- **`min_value` / `max_value`**: *(Optional)* Bounds for input validation.
- **`default_value`**: *(Optional)* Value returned if no input is provided. Must fall within bounds.
- **`type_error_message`**: *(Optional)* Error message shown when input cannot be converted to expected type. Defaults are provided for each function.

#### Default Type Error Messages:

| Function         | Default `type_error_message`                                                                                                                                                                                          |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `int_input`      | **Error**: You must enter a valid integer.                                                                                                                                                                            |
| `float_input`    | **Error**: You must enter a valid float.                                                                                                                                                                              |
| `decimal_input`  | **Error**: You must enter a valid Decimal.                                                                                                                                                                            |
| `datetime_input` | **Error**: You must enter a valid datetime in valid ISO 8601 format e.g. YYYY-MM-DD.<br>See [documentation](https://docs.python.org/3/library/datetime.html#datetime.datetime.fromisoformat) for all allowed options. |

---

Here's an updated README section to showcase how `typed_input` supports the same API as `input()`:

---

### Seamless Input API Compatibility

The `typed_input` library is designed to feel natural for Python developers by
supporting the same API as the standard [`input()`](https://docs.python.org/3/library/functions.html#input) function.

#### Example Usage (like [`input()`](https://docs.python.org/3/library/functions.html#input))
```python
>>> from typed_input import int_input
>>> x = int_input()
a
Error: You must enter a valid integer.
42
>>> type(x)
<class 'int'>
>>> x
42

>>> from typed_input import float_input
>>> x = float_input()
3.14
>>> type(x)
<class 'float'>

>>> from typed_input import decimal_input
>>> x = decimal_input()
1.45
>>> type(x)
<class 'decimal.Decimal'>

>>> from typed_input import datetime_input
>>> dt = datetime_input()
2024-01-01
>>> type(dt)
<class 'datetime.datetime'>
```

#### Example with a `prompt`
Just like [`input()`](https://docs.python.org/3/library/functions.html#input), you can also pass a `prompt` to guide the user:
```python
>>> from typed_input import int_input
>>> int_input('Enter a number: ')
Enter a number: 7
7
```

This compatibility makes `typed_input` a drop-in replacement for `input()` in 
many scenarios, with the added benefit of type safety and validation!

### More Examples Showing Range Validation

#### `int_input` for validated integer input
```python
>>> from typed_input import int_input
>>> int_input(prompt="Enter a number (1-10): ", min_value=1, max_value=10)
Enter a number (1-10): abc
Error: You must enter a valid integer.
Enter a number (1-10): 20
Error: Value must be between 1 and 10.
Enter a number (1-10): 5
5
```

#### `float_input` for validated floating-point input
```python
>>> from typed_input import float_input
>>> float_input(prompt="Enter a temperature (-50 to 50): ", min_value=-50.0, max_value=50.0)
Enter a temperature (-50 to 50): 
Error: You must enter a valid float.
Enter a temperature (-50 to 50): 100
Error: Value must be between -50.0 and 50.0.
Enter a temperature (-50 to 50): 22.5
22.5
```

#### `decimal_input` for validated decimal input
```python
>>> from typed_input import decimal_input
>>> from decimal import Decimal
>>> decimal_input(prompt="Enter a price (min 0.01): ", min_value=Decimal("0.01"))
Enter a price (min 0.01): -10
Error: Value must be at least 0.01.
Enter a price (min 0.01): 19.99
Decimal('19.99')
```

#### `datetime_input` for validated datetime input
```python
>>> from typed_input import datetime_input
>>> from datetime import datetime
>>> datetime_input(prompt="Enter a date (YYYY-MM-DD): ", min_value=datetime(2023, 1, 1))
Enter a date (YYYY-MM-DD): invalid
Error: You must enter a valid datetime in ISO 8601 format (e.g., YYYY-MM-DD).
Enter a date (YYYY-MM-DD): 2022-12-31
Error: Date must be on or after 2023-01-01.
Enter a date (YYYY-MM-DD): 2023-01-15
datetime.datetime(2023, 1, 15, 0, 0)
```
---

### ❌ Error Handling

All functions raise a `ValueError` for:
- **Invalid Range**: `min_value > max_value`.
- **Default Out of Bounds**: `default_value` outside `min_value`/`max_value`.

Example:
```python
>>> int_input(min_value=10, max_value=5)
Traceback (most recent call last):
  ...
ValueError: min_value (10) cannot be greater than max_value (5).
```

---

### 🛠️ Development

- Run formater: 
  - `uv run ruff check --select I --fix && uv run ruff format`
- Run type checking: 
  - `uv run mypy . `
- Run all unit tests:
  - `uv run typed_input_test.py`
- Run specific unit test:
  - `uv run python -m unittest int_input_test.py`

