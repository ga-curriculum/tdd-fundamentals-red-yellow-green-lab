<h1>
  <span class="headline">TDD Fundamentals: Red, Yellow, Green Lab</span>
  <span class="subhead">Exercise</span>
</h1>

## Practicing TDD with Red, Yellow, Green

### 🔴 Section 1: Red — Write a Failing Test First

**Goal:** Start with the test. This defines what your function should do.

### Key Principles:

- Write a single, focused test that clearly describes the expected behavior.
- Do **not** write implementation code yet.
- Run the test suite and confirm that it **fails**.

### Why Red?

A failing test proves your test is valid and that the feature doesn't yet exist. It sets a clear starting point.

### Example:

```python
def test_area_of_square():
    assert area(5, 3) == 15
```

> ❌ You haven’t defined `area()` yet. This test should fail—it’s your starting line.

### 🟡 Section 2: Yellow — Make It Pass, Quickly

**Goal:** Write the minimum code necessary to make the failing test pass.

### Key Principles:

- Don’t overthink the implementation.
- Avoid refactoring or optimizations.
- Write code that is **just enough** to get to green.

### Why Yellow?

You're prioritizing proof-of-behavior, not elegance. It's okay to hardcode values temporarily.

### Example:

```python
def area(width, height):
    return 15
```

> ✅ This passes the test by returning the expected value—hardcoded for now.

### 🟢 Section 3: Green — Refactor and Improve

**Goal:** Improve the implementation without changing the behavior.

### Key Principles:

- Clean up code while keeping all tests green.
- Generalize logic, improve naming, remove duplication.
- Keep rerunning tests to ensure behavior remains correct.

### Why Green?

Your test now acts as a safety net. You can confidently improve your code structure knowing its behavior is verified.

### Example:

```python
def area(width, height):
    return width * height
```

> ✨ Now it works for any dimensions, like `(4, 2) → 8` or `(10, 10) → 100`.

## Now lets look at a more challenging context

### 🔴 Red — Write a Failing Test First

This time we will create a `FastAPI` route that performs a simple operation like reversing a string sent as a URL parameter.

```python
from fastapi.testclient import TestClient
from main import app

client = TestClient(app)

def test_reverse_string_route():
    response = client.get("/reverse?text=hello")
    assert response.status_code == 200
    assert response.json() == {"reversed": "olleh"}
```

> ❌ The /reverse route doesn't exist yet, so this test fails. That's expected—it's your red phase.

### 🟡 Yellow — Make It Pass, Quickly

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/reverse")
def reverse_string(text: str):
    return {"reversed": "olleh"}
```

> ✅ The test now passes, but the logic is hardcoded—it only works for `"hello"`.

### 🟢 Green — Refactor and Improve

```python
@app.get("/reverse")
def reverse_string(text: str):
    return {"reversed": text[::-1]}
```

> ✨ Now it dynamically reverses any string, not just `"hello"`—you can reuse it for `"world"`, or `"Python"`.

--

## Part 1 - Build Your Own TDD Cycle

### Scenario:

You are building a currency conversion utility that supports converting between several international currencies based on fixed exchange rates.

### Instructions:

1. **Red:** Write a test for this function:

   ```python
   def convert_currency(amount: float, from_currency: str, to_currency: str) -> float:
       pass
   ```

   Write a test that expects:

   ```python
   convert_currency(100, "USD", "BHD") == 37.8
   ```

2. **Yellow:** Hardcode a value to pass that test.

3. **Green:** Refactor to use a dictionary of exchange rates, like:

   ```python
   EXCHANGE_RATES = {
       ("USD", "BHD"): 0.378,
       ("BHD", "USD"): 2.6455,
       # Add more pairs
   }
   ```

4. Add tests for more scenarios:

   - Converting between multiple currencies
   - Handling unsupported currencies with `ValueError`
   - Rounding output to two decimals

5. Use `pytest` to run and rerun your tests through each stage.

### Deliverables:

- A `converter.py` file with your function.
- A `test_converter.py` file with at least 3 tests.

## Part 2 - Build a TDD-Driven Calculator API

### Scenario

You’re creating a simple calculator API with FastAPI. Users can perform basic math operations by visiting specific routes. You’ll build the API step-by-step using Test-Driven Development (TDD): write tests first, make them pass, then improve the implementation.

### Instructions

1. **Red:** Start by writing a test for a new route:

```python
def test_addition_route():
    response = client.get("/add?a=5&b=3")
    assert response.status_code == 200
    assert response.json() == {"result": 8}
```

2. **Yellow:** Create the bare minimum implementation in your FastAPI app:

```python
@app.get("/add")
def add(a: int, b: int):
    return {"result": 8}
```

3. **Green:** Refactor to make it dynamic:

```python
@app.get("/add")
def add(a: int, b: int):
    return {"result": a + b}
```

4. Repeat the process to build **three more** routes:

- `/subtract?a=10&b=4` → `{"result": 6}`
- `/multiply?a=7&b=6` → `{"result": 42}`
- `/divide?a=10&b=2` → `{"result": 5}`

Use the same Red → Yellow → Green approach for each.

1. Add edge case tests:

- Subtracting a larger number from a smaller one
- Multiplying by zero
- Passing non-integer input (expect FastAPI validation error)
- Remainders after division

6. Run all your tests with `pytest` during each phase to track your progress.

### Deliverables

- `main.py` with at least three calculator routes.
- `test_calculator.py` with at least **one test per route** and **one edge case test**.
