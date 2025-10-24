# API Documentation

This document describes the routes and endpoints available in the Linear Programming Calculator web application.

## Table of Contents

- [Overview](#overview)
- [Routes](#routes)
- [Request/Response Examples](#requestresponse-examples)
- [Error Handling](#error-handling)
- [Data Models](#data-models)

## Overview

The application is built with Flask and provides a web interface for solving linear programming problems. All routes serve HTML pages except where noted.

**Base URL**: `http://127.0.0.1:5000/`

## Routes

### Home Page

```
GET /
```

**Description**: Displays the home page with information about Linear Programming and PuLP.

**Parameters**: None

**Returns**: HTML page (inicio.html)

**Template Variables**: None

---

### Problem Setup Page

```
GET /index
POST /index
```

**Description**:
- GET: Displays form to input problem dimensions
- POST: Processes form submission and redirects to calculator

**GET Parameters**: None

**POST Parameters**:
| Parameter | Type | Required | Description | Constraints |
|-----------|------|----------|-------------|-------------|
| num_variables | int | Yes | Number of decision variables | 1-100 |
| num_constraints | int | Yes | Number of constraints | 1-50 |
| optimization_type | string | Yes | Type of optimization | "Maximizar" or "Minimizar" |

**Returns**:
- GET: HTML form (index.html)
- POST: Redirect to `/calculator` with query parameters

**Example POST**:
```html
<form action="/index" method="post">
    <input type="number" name="num_variables" value="2">
    <input type="number" name="num_constraints" value="2">
    <select name="optimization_type">
        <option value="Maximizar">Maximizar</option>
    </select>
</form>
```

**Redirect URL**: `/calculator?num_constraints=2&num_variables=2&optimization_type=Maximizar`

---

### Calculator Page

```
GET /calculator
POST /calculator
```

**Description**:
- GET: Displays form to input coefficients for objective function and constraints
- POST: Solves the linear programming problem and displays results

#### GET Request

**Query Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| num_variables | int | Yes | Number of decision variables |
| num_constraints | int | Yes | Number of constraints |
| optimization_type | string | Yes | "Maximizar" or "Minimizar" |

**Returns**: HTML form (calculator.html) with dynamic input fields

**Template Variables**:
- `num_variables`: Number of variables
- `num_constraints`: Number of constraints
- `optimization_type`: Optimization type

#### POST Request

**Form Parameters**:

**Hidden Fields**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| num_variables | int | Yes | Number of decision variables |
| num_constraints | int | Yes | Number of constraints |
| optimization_type | string | Yes | "Maximizar" or "Minimizar" |

**Objective Function Coefficients**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| coef_1, coef_2, ..., coef_n | float | Yes | Coefficients for each variable |

**Constraint Coefficients** (for each constraint i):
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| constraint_i_1, constraint_i_2, ..., constraint_i_n | float | Yes | Coefficients for each variable in constraint i |
| relation_i | string | Yes | Constraint operator: "<=", ">=", or "=" |
| constant_i | float | Yes | Right-hand side constant |

**Returns**: HTML page (solution.html) with optimal solution

**Success Response**:
```python
{
    'vars': [
        {'x1': 2.0},
        {'x2': 1.5}
    ],
    'optimal_value': 9.0
}
```

**Error Response** (400):
```
"Invalid input. Please check your data."
```

**Example POST**:
```html
<form action="/calculator" method="post">
    <!-- Hidden fields -->
    <input type="hidden" name="num_variables" value="2">
    <input type="hidden" name="num_constraints" value="2">
    <input type="hidden" name="optimization_type" value="Maximizar">

    <!-- Objective coefficients -->
    <input type="number" name="coef_1" value="3" step="any">
    <input type="number" name="coef_2" value="2" step="any">

    <!-- Constraint 1 -->
    <input type="number" name="constraint_1_1" value="1" step="any">
    <input type="number" name="constraint_1_2" value="1" step="any">
    <select name="relation_1">
        <option value="<=">≤</option>
    </select>
    <input type="number" name="constant_1" value="4" step="any">

    <!-- Constraint 2 -->
    <input type="number" name="constraint_2_1" value="2" step="any">
    <input type="number" name="constraint_2_2" value="1" step="any">
    <select name="relation_2">
        <option value="<=">≤</option>
    </select>
    <input type="number" name="constant_2" value="5" step="any">
</form>
```

---

### About Page

```
GET /about
```

**Description**: Displays contact and developer information.

**Parameters**: None

**Returns**: HTML page (about.html)

**Template Variables**: None

---

## Request/Response Examples

### Example 1: Maximization Problem

**Problem**:
```
Maximize: Z = 3x₁ + 2x₂
Subject to:
  x₁ + x₂ ≤ 4
  2x₁ + x₂ ≤ 5
  x₁, x₂ ≥ 0
```

**Step 1**: POST to `/index`
```
num_variables=2
num_constraints=2
optimization_type=Maximizar
```

**Step 2**: POST to `/calculator`
```
num_variables=2
num_constraints=2
optimization_type=Maximizar
coef_1=3
coef_2=2
constraint_1_1=1
constraint_1_2=1
relation_1=<=
constant_1=4
constraint_2_1=2
constraint_2_2=1
relation_2=<=
constant_2=5
```

**Response** (solution.html displays):
```
x1 = 1.0
x2 = 3.0
Optimal value = 9.0
```

### Example 2: Minimization Problem

**Problem**:
```
Minimize: Z = 2x₁ + 3x₂
Subject to:
  x₁ + x₂ ≥ 5
  2x₁ + x₂ ≥ 8
  x₁, x₂ ≥ 0
```

**Step 1**: POST to `/index`
```
num_variables=2
num_constraints=2
optimization_type=Minimizar
```

**Step 2**: POST to `/calculator`
```
num_variables=2
num_constraints=2
optimization_type=Minimizar
coef_1=2
coef_2=3
constraint_1_1=1
constraint_1_2=1
relation_1=>=
constant_1=5
constraint_2_1=2
constraint_2_2=1
relation_2=>=
constant_2=8
```

**Response** (solution.html displays):
```
x1 = 3.0
x2 = 2.0
Optimal value = 12.0
```

## Error Handling

### Input Validation

The application performs the following validations:

1. **Variable Count Limits**:
   - Minimum: 1
   - Maximum: 100
   - Values outside this range are clamped

2. **Constraint Count Limits**:
   - Minimum: 1
   - Maximum: 50
   - Values outside this range are clamped

3. **Type Validation**:
   - All numeric inputs must be valid floats
   - Invalid types return 400 error

### Error Responses

**400 Bad Request**: Returned when input validation fails

```
"Invalid input. Please check your data."
```

**Causes**:
- Non-numeric values in numeric fields
- Missing required form fields
- Type conversion errors

## Data Models

### Problem Configuration

```python
{
    'num_variables': int,        # 1-100
    'num_constraints': int,      # 1-50
    'optimization_type': str     # "Maximizar" or "Minimizar"
}
```

### Objective Function

```python
{
    'coefficients': [float],     # Length = num_variables
}
```

### Constraint

```python
{
    'coefficients': [float],     # Length = num_variables
    'operator': str,             # "<=", ">=", or "="
    'constant': float
}
```

### Solution

```python
{
    'vars': [
        {
            'variable_name': float  # e.g., {'x1': 2.0}
        }
    ],
    'optimal_value': float
}
```

## Internal Processing

### PuLP Problem Construction

The application constructs a PuLP `LpProblem` as follows:

1. **Create Problem**:
   ```python
   problem = pulp.LpProblem("Problema de Programación Lineal",
                            pulp.LpMaximize or pulp.LpMinimize)
   ```

2. **Create Variables**:
   ```python
   decision_vars = [pulp.LpVariable(f'x{i}', lowBound=0)
                    for i in range(1, num_variables + 1)]
   ```

3. **Add Objective**:
   ```python
   objective = pulp.lpSum([coef * var
                           for coef, var in zip(objective_coefficients, decision_vars)])
   problem += objective
   ```

4. **Add Constraints**:
   ```python
   for i, constraint_coeffs in enumerate(constraint_entries_list):
       constraint = pulp.lpSum([coef * var
                                for coef, var in zip(constraint_coeffs, decision_vars)])
       if relation_operators[i] == '<=':
           problem += constraint <= constraint_constants[i]
       elif relation_operators[i] == '>=':
           problem += constraint >= constraint_constants[i]
       elif relation_operators[i] == '=':
           problem += constraint == constraint_constants[i]
   ```

5. **Solve**:
   ```python
   problem.solve()
   ```

## Notes

- All decision variables have a non-negativity constraint (`lowBound=0`)
- The application uses PuLP's default solver (usually CBC)
- Solutions are displayed in the browser; no API endpoints return JSON
- The application runs in debug mode by default (should be disabled in production)

## Future Enhancements

Potential API improvements for future versions:

- RESTful JSON API endpoints
- Support for integer programming
- Sensitivity analysis results
- Graphical solution for 2-variable problems
- Export results to CSV/PDF
- API authentication
- Rate limiting

---

**Version**: 1.0.0
**Last Updated**: 2024

For questions or issues, please contact: santiagosanchezmarquez@gmail.com
