<h1>
  <span class="headline">TDD Fundamentals: Red, Yellow, Green Lab</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

Before starting the lab, let’s set up your project folder, install dependencies, and create the required files for both parts of the exercise.

## 1. Create Your Project Folder

In your terminal:

```bash
mkdir tdd-fundamentals-lab
cd tdd-fundamentals-lab
```

## 2. Set Up a Virtual Environment

Create and activate a virtual environment:

**macOS/Linux:**

```bash
python -m venv venv
source venv/bin/activate
```

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

## 3. Install Dependencies

```bash
pip install fastapi uvicorn pytest
```

Check installation:

```bash
pip show fastapi
pip show pytest
```

## 4. Create These Files

For **Part 1: Currency Converter Function**:

- `converter.py` – for your currency conversion logic
- `test_converter.py` – for your unit tests using `pytest`

For **Part 2: Calculator API**:

- `main.py` – your FastAPI app and calculator routes
- `test_calculator.py` – test file for calculator routes

Your final folder structure should look like:

```
tdd-fundamentals-lab/
│
├── converter.py
├── test_converter.py
│
├── main.py
├── test_calculator.py
```

## 5. Run Tests with Pytest

From the root of your `tdd-fundamentals-lab` folder, you can run tests by running:

```bash
pytest <filename>
```

Make sure each test follows the **Red → Yellow → Green** cycle as you build.
