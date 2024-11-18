<p align="center">
<a href="https://github.com/sashsinha/typed_input"><img alt="Typed Input Logo" src="https://raw.githubusercontent.com/sashsinha/typed_input/main/logo.png"></a>
</p>

<h1 align="center">Typed Input</h1>

<h3 align="center">Effortless type-safe user input for integers, floats, dates, and more...</h3>

<p align="center">
<a href="https://raw.githubusercontent.com/sashsinha/typed_input/main/LICENCE"><img alt="License: MIT" src="https://raw.githubusercontent.com/sashsinha/typed_input/main/license.svg"></a>
</p>


# 🛠️ Development

- Run formater: 
    - `uv run ruff check --select I --fix && uv run ruff format`
- Run type checking: 
    - `uv run mypy . `
- Run all unit tests:
    - `uv run typed_input_test.py`
- Run specific unit test:
    - `uv run python -m unittest int_input_test.py`
