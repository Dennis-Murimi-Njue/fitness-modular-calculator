# 🏃 Fitness & Modular Calculator

A lightweight, modular Python toolkit for tracking a client's weekly fitness. Each calculator is a small, self-contained function, and the final script combines them all into one printed weekly report. It uses the Python standard library only, so there is nothing to install.

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)

---

## 📑 Table of Contents

- [Features](#-features)
- [Getting Started](#-getting-started)
- [Calculator Reference](#-calculator-reference)
- [Full Weekly Report](#-full-weekly-report)
- [Sample Output](#-sample-output)
- [Customising the Data](#-customising-the-data)
- [Concepts Demonstrated](#-concepts-demonstrated)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

| # | Calculator | Functions | Python concept |
|---|------------|-----------|----------------|
| 1 | BMI Calculator | `calculate_bmi()`, `bmi_category()` | Arithmetic, `round()`, conditionals |
| 2 | Step Goal Checker | `weekly_step_summary()` | Default parameters, list comprehensions |
| 3 | Calorie Estimate | `estimate_calories()` | `math` module (`math.floor`) |
| 4 | Days on Protocol | `protocol_summary()` | Counting, dictionaries (dict comprehension in the full report) |
| 5 | Full Weekly Report | all of the above | `datetime` (`date.today()`), f-strings |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or newer

### Installation

```bash
git clone https://github.com/<your-username>/fitness-calculator.git
cd fitness-calculator
```

No `pip install` is needed, since only the built-in `math` and `datetime` modules are used.

### Run

```bash
python fitness_calculator.py
```

Replace `fitness_calculator.py` with whatever you named your script. Running it prints each calculator's test output, followed by the full weekly report.

---

## 📖 Calculator Reference

### 1. BMI Calculator

**`calculate_bmi(weight_kg, height_m)`**

Takes weight in kilograms and height in metres. Returns BMI rounded to one decimal place, using `weight / height²`.

| Parameter | Type | Description |
|-----------|------|-------------|
| `weight_kg` | `float` | Body weight in kilograms |
| `height_m` | `float` | Height in metres |

**Returns:** `float` (e.g. `26.5`)

**`bmi_category(bmi)`**

Takes a BMI value and returns its category as a string.

| BMI | Category |
|-----|----------|
| < 18.5 | Underweight |
| 18.5 to 24.9 | Normal weight |
| 25.0 to 29.9 | Overweight |
| 30.0 and above | Obese |

```python
bmi = calculate_bmi(84, 1.78)   # 26.5
bmi_category(bmi)               # "Overweight"
```

---

### 2. Step Goal Checker

**`weekly_step_summary(steps_list, goal=8000)`**

Takes a list of daily step counts and an optional goal, and returns a summary of the week. The `goal` parameter has a **default of 8,000**, so you only need to pass it if you want a different target. A list comprehension counts the days the goal was reached.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `steps_list` | `list[int]` | required | Step count for each day |
| `goal` | `int` | `8000` | Daily step target |

**Returns:** `dict`

| Key | Meaning |
|-----|---------|
| `days_on_goal` | Number of days that met or beat the goal |
| `total_days` | Number of days in the list |
| `average` | Average steps per day (rounded) |
| `best_day` | Highest daily step count |
| `worst_day` | Lowest daily step count |

```python
weekly = [9200, 7500, 10500, 8800, 6900, 11000, 9600]
weekly_step_summary(weekly)            # uses the default goal of 8,000
weekly_step_summary(weekly, goal=10000)  # custom goal
```

---

### 3. Calorie Estimate

**`estimate_calories(steps, calories_per_step=0.04)`**

Estimates calories burned from walking, using approximately **0.04 kcal per step**. The result is rounded down with `math.floor()`.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `steps` | `int` | required | Steps taken |
| `calories_per_step` | `float` | `0.04` | Estimated kcal burned per step |

**Returns:** `int` (estimated kilocalories)

```python
estimate_calories(10000)   # 400
daily_cals = [estimate_calories(s) for s in weekly]
```

> This is a rough estimate. Actual calories burned vary with body weight, pace and terrain.

---

### 4. Days on Protocol

**`protocol_summary(protocol_list)`**

Takes a list of daily fasting protocols and returns a count of how many days each protocol was used.

| Parameter | Type | Description |
|-----------|------|-------------|
| `protocol_list` | `list[str]` | The protocol followed on each day |

**Returns:** `dict` mapping each protocol name to its day count.

```python
protocols = ["OMAD", "2MAD", "OMAD", "Autophagy Marathon", "OMAD", "2MAD", "OMAD"]
protocol_summary(protocols)
# {'OMAD': 4, '2MAD': 2, 'Autophagy Marathon': 1}
```

> Protocols are collected with `set()`, so the order of the keys in the output can vary between runs.

---

## 📋 Full Weekly Report

The final script combines all four calculators into one report for a client. The report date is generated automatically with `datetime.date.today()` and formatted as `DD Month YYYY`.

Edit the **DATA** section at the top of the report script:

```python
client_name  = "James"
weight_kg    = 84
height_m     = 1.78
weekly_steps = [9200, 7500, 10500, 8800, 6900, 11000, 9600]
protocols    = ["OMAD", "2MAD", "OMAD", "Autophagy Marathon", "OMAD", "2MAD", "OMAD"]
step_goal    = 8000
```

The report then prints four sections: **Body** (weight and BMI), **Steps** (goal progress, average, best and worst day, estimated calories), and **Protocol Breakdown**.

---

## 🖨 Sample Output

```
==========================================
  WEEKLY REPORT: JAMES
  Date: 02 November 2026
==========================================

BODY
  Weight : 84 kg
  BMI    : 26.5 (Overweight)

STEPS (Goal: 8000)
  Days on goal : 5/7
  Average      : 9071 steps/day
  Best day     : 11000 steps
  Worst day    : 6900 steps
  Cals burned  : ~2540 kcal

PROTOCOL BREAKDOWN
  OMAD: 4 day(s)
  2MAD: 2 day(s)
  Autophagy Marathon: 1 day(s)

==========================================
```

The date reflects the day you run the script, and the order of the protocol lines may vary.

---

## ✏️ Customising the Data

- **Different client:** change `client_name`, `weight_kg` and `height_m`.
- **Different week:** replace the `weekly_steps` and `protocols` lists. Keep both at 7 entries so the report's "x/7" label stays correct.
- **Different goal:** change `step_goal`.
- **Different calorie rate:** pass `rate` (or `calories_per_step` in the standalone function) to `estimate_calories()`.

---

## 🧠 Concepts Demonstrated

- Writing small, reusable, single-purpose functions
- Default parameters (`goal=8000`, `calories_per_step=0.04`)
- List comprehensions and dictionary comprehensions
- The `math` module (`math.floor`)
- Working with dates using `datetime.date`
- Returning dictionaries from functions
- Combining several functions into one formatted report with f-strings

---

## 🗺 Roadmap

- [ ] Input validation (e.g. zero or negative height, empty step lists)
- [ ] Unit tests with `unittest` or `pytest`
- [ ] Command-line interface using `argparse`
- [ ] Save and load client history from a JSON file
- [ ] Sorted, consistent protocol ordering in the report

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Denno**
Built with Python 🐍 and a love for fitness.
