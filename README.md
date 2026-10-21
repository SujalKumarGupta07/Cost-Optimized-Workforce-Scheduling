# Cost-Optimized Workforce Scheduling with Linear Programming

A linear programming project using **Python, Pyomo, and the CBC solver** to determine a cost-effective allocation of system-administrator working hours across five weekdays while satisfying availability and minimum weekly working-hour requirements.

## Problem Overview

A department requires system-administrator coverage from **8:00 AM to 10:00 PM, Monday through Friday**. This corresponds to 14 hours of coverage per weekday.

Six candidates are available, each with a different hourly wage rate, daily availability, and minimum weekly working-hour requirement. The objective is to allocate working hours among these candidates while minimizing the total weekly wage cost.

The optimization model considers:

- Different hourly wage rates for each candidate.
- Candidate-specific availability on each weekday.
- Exactly 14 hours of administrator coverage per weekday.
- Minimum weekly working hours for every candidate.
- Minimum total wage cost while satisfying all constraints.

## Tools and Technologies

- **Python** — implementation of the optimization model.
- **Pyomo** — algebraic modeling and formulation of the linear programming problem.
- **CBC** — open-source linear programming solver.
- **Jupyter Notebook** — implementation, execution, and presentation of the results.

## Mathematical Formulation

### 1. Decision Variables

Let $x_{ij}$ represent the number of hours assigned to candidate $i$ on weekday $j$, where $i$ indexes the six candidates and $j$ indexes the five weekdays.

The decision variables are nonnegative:

$$
x_{ij} \geq 0
$$

### 2. Objective Function

The objective is to minimize the total weekly wage cost.

Let $w_i$ denote the hourly wage rate of candidate $i$.

$$
\min Z = \sum_{i=1}^{6}\sum_{j=1}^{5} w_i x_{ij}
$$

### 3. Constraints

**Daily availability constraints**

Each candidate's assigned hours must not exceed their availability on the corresponding weekday.

Let $a_{ij}$ denote the available hours of candidate $i$ on weekday $j$.

$$
0 \leq x_{ij} \leq a_{ij}
\quad \forall i,j
$$

**Daily coverage constraints**

Exactly 14 administrator-hours must be allocated each weekday.

$$
\sum_{i=1}^{6}x_{ij}=14
\quad \forall j
$$

**Minimum weekly working-hour constraints**

Each candidate must receive at least their required number of working hours during the week.

Let $h_i$ represent the minimum weekly working hours required for candidate $i$.

$$
\sum_{j=1}^{5}x_{ij}\geq h_i
\quad \forall i
$$

The minimum weekly requirements are:

- K.C., D.H., H.B., and S.C.: 8 hours each.
- K.S. and N.K.: 7 hours each.

## Optimization Results

The notebook's saved solver output reports a total weekly wage cost of **10,692 wage units**.

### Optimal Hour Allocation

| Candidate | Monday | Tuesday | Wednesday | Thursday | Friday | Weekly Total |
|:---|---:|---:|---:|---:|---:|---:|
| K.C. | 2 | 0 | 4 | 0 | 3 | 9 |
| D.H. | 0 | 2 | 0 | 6 | 0 | 8 |
| H.B. | 4 | 7 | 4 | 0 | 4 | 19 |
| S.C. | 5 | 5 | 5 | 0 | 5 | 20 |
| K.S. | 3 | 0 | 1 | 3 | 0 | 7 |
| N.K. | 0 | 0 | 0 | 5 | 2 | 7 |
| **Daily Total** | **14** | **14** | **14** | **14** | **14** | **70** |

### Results Interpretation

- The daily allocation provides exactly 14 hours of coverage on every weekday.
- Every candidate satisfies their minimum weekly working-hour requirement.
- The allocation respects the candidates' daily availability limits.
- The reported objective value is 10,692 wage units for the week.

## How to Run the Project

### Prerequisites

- Python 3.10 or later.
- The Python dependencies listed in `requirements.txt`.
- The CBC optimization solver installed separately.

### Step 1: Clone the Repository

```bash
git clone https://github.com/SujalKumarGupta07/Cost-Optimized-Workforce-Scheduling
cd Cost-Optimized-Workforce-Scheduling
```

Replace `YOUR_USERNAME` with your GitHub username.

### Step 2: Install Python Dependencies

```bash
python -m pip install -r requirements.txt
```

### Step 3: Install the CBC Solver

Pyomo defines the optimization model, while CBC solves it. The CBC executable must be installed separately and available on your system's `PATH`.

**macOS (Homebrew)**

```bash
brew install cbc
```

**Ubuntu/Debian**

```bash
sudo apt-get update
sudo apt-get install coinor-cbc
```

**Windows**

Install a compatible CBC distribution and add its executable directory to the system `PATH`.

Verify the installation by running:

```bash
cbc
```

### Step 4: Run the Notebook

Open `workforce_scheduling_optimization.ipynb` using Jupyter Notebook, JupyterLab, or a compatible notebook editor.

Run the cells to construct the model, invoke the solver, and inspect the allocation and objective value.

## Model Scope and Assumptions

- Decision variables are continuous and nonnegative, so fractional working hours are permitted.
- Daily coverage is modeled as a total of 14 assigned hours per weekday.
- The model does not explicitly represent shift start times, shift end times, or coverage at every instant of the day.
- A practical shift-roster system would require additional time-indexed constraints to verify continuous coverage and account for overlapping shifts.
- Wage costs use the wage-rate units specified in the original exercise.

## Repository Structure

```text
workforce-scheduling-optimization/
├── workforce_scheduling_optimization.ipynb
├── README.md
├── requirements.txt
└── problem_statement.png
```

The problem statement image is optional. Include it only if sharing the original assignment is permitted.

## Key Learning Outcomes

- Formulating real-world resource allocation problems as linear programs.
- Defining decision variables, objective functions, and constraints.
- Implementing optimization models using Pyomo.
- Solving linear programming problems using CBC.
- Interpreting optimization results and validating constraint satisfaction.
- Understanding the distinction between daily hour allocation and detailed shift scheduling.

## Project Summary

This project demonstrates how **linear programming can support cost-effective workforce allocation** under availability and working-hour constraints. It provides practical experience in mathematical optimization, constraint modeling, solver integration, and interpreting optimization results for an Operations Research application.
