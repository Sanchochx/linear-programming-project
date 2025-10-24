# User Guide

Complete guide for using the Linear Programming Calculator web application.

## Table of Contents

- [Getting Started](#getting-started)
- [Understanding the Interface](#understanding-the-interface)
- [Step-by-Step Tutorial](#step-by-step-tutorial)
- [Features Explained](#features-explained)
- [Tips and Best Practices](#tips-and-best-practices)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)

## Getting Started

### What is Linear Programming?

Linear Programming (LP) is a mathematical method for finding the best outcome (maximum profit, minimum cost, etc.) in a mathematical model with linear relationships. It's widely used in business, economics, engineering, and operations research.

### What Can This Calculator Do?

The Linear Programming Calculator helps you:
- **Solve optimization problems** with multiple variables and constraints
- **Maximize or minimize** any linear objective function
- **Handle complex constraints** with different operators (≤, ≥, =)
- **Get instant solutions** without manual calculations

### Who Should Use This?

- **Students** learning linear programming
- **Business analysts** optimizing resources
- **Engineers** solving design problems
- **Researchers** conducting operations research
- **Anyone** needing to solve LP problems quickly

## Understanding the Interface

### Navigation Menu

The application has a fixed sidebar navigation:

1. **Home**: Learn about linear programming and PuLP
2. **Calculator**: Access the problem-solving interface
3. **About**: Contact information and developer details

### Pages Overview

#### Home Page (/)
Provides educational content about:
- Linear programming concepts
- PuLP library information
- Links to get started

#### Index Page (/index)
First step in solving a problem:
- Enter number of variables
- Enter number of constraints
- Select optimization type

#### Calculator Page (/calculator)
Main problem-solving interface:
- Input objective function coefficients
- Define constraint coefficients
- Choose constraint operators
- Enter constraint constants

#### Solution Page (/solution)
Displays results:
- Optimal values for each variable
- Optimal value of objective function

## Step-by-Step Tutorial

### Example: Maximize Profit

Let's solve a real problem step by step.

**Problem**:
A bakery makes cakes and cookies. Each cake gives $3 profit, each batch of cookies gives $2 profit. Constraints:
- Total production ≤ 4 units
- Making capacity: 2 cakes + 1 cookie batch ≤ 5

Find production to maximize profit.

#### Step 1: Navigate to Calculator

1. Open your browser
2. Go to `http://127.0.0.1:5000/`
3. Click **Calculator** in the sidebar

#### Step 2: Define Problem Dimensions

On the index page:
1. **Number of Variables**: Enter `2`
   - Variable 1 (x₁) = number of cakes
   - Variable 2 (x₂) = number of cookie batches

2. **Number of Constraints**: Enter `2`
   - Constraint 1: total production
   - Constraint 2: making capacity

3. **Optimization Type**: Select `Maximizar`

4. Click **Continue**

#### Step 3: Enter Objective Function

On the calculator page, enter coefficients for profit:
- **Coefficient x1** (cake profit): `3`
- **Coefficient x2** (cookie profit): `2`

This represents: Z = 3x₁ + 2x₂

#### Step 4: Enter First Constraint

For constraint "x₁ + x₂ ≤ 4":
- **Constraint 1, Coefficient x1**: `1`
- **Constraint 1, Coefficient x2**: `1`
- **Operator**: Select `≤`
- **Constant**: `4`

#### Step 5: Enter Second Constraint

For constraint "2x₁ + x₂ ≤ 5":
- **Constraint 2, Coefficient x1**: `2`
- **Constraint 2, Coefficient x2**: `1`
- **Operator**: Select `≤`
- **Constant**: `5`

#### Step 6: Solve

1. Review all inputs
2. Click **Solve** button
3. Wait for solution (usually instant)

#### Step 7: Interpret Results

The solution page shows:
```
x1 = 1.0
x2 = 3.0
Optimal value = 9.0
```

**Interpretation**:
- Make 1 cake
- Make 3 batches of cookies
- Maximum profit = $9

## Features Explained

### Input Validation

The application automatically validates:
- **Variable count**: 1-100 (values outside are clamped)
- **Constraint count**: 1-50 (values outside are clamped)
- **Numeric values**: Must be valid numbers
- **Required fields**: All fields must be filled

### Constraint Operators

Three types supported:

1. **≤ (Less than or equal)**
   - Use when the left side cannot exceed the right
   - Example: Production ≤ Capacity

2. **≥ (Greater than or equal)**
   - Use when the left side must meet minimum
   - Example: Nutrition ≥ Requirement

3. **= (Equal)**
   - Use when the left must exactly equal the right
   - Example: Total allocation = Budget

### Optimization Types

**Maximize**:
- Finding maximum value (profit, revenue, production)
- Example: Maximize profit = 3x₁ + 2x₂

**Minimize**:
- Finding minimum value (cost, waste, time)
- Example: Minimize cost = 2x₁ + 3x₂

### Non-Negativity Constraints

All variables automatically have x ≥ 0:
- You don't need to enter these constraints
- Prevents negative solutions (can't produce -5 items)
- Standard assumption in LP problems

## Tips and Best Practices

### Before You Start

1. **Identify Variables**
   - What are you trying to find?
   - Clearly define what each variable represents
   - Example: x₁ = chairs, x₂ = tables

2. **Define Objective**
   - What are you optimizing?
   - Is it maximization or minimization?
   - Get the coefficients right

3. **List Constraints**
   - What limitations exist?
   - Resource constraints (labor, materials)
   - Requirement constraints (minimum production)
   - Policy constraints (maximum inventory)

### During Input

1. **Double-Check Numbers**
   - Verify each coefficient
   - Ensure operators are correct
   - Confirm constants

2. **Units Matter**
   - Keep units consistent
   - If using hours, use hours everywhere
   - If using dollars, use dollars throughout

3. **Use Decimals When Needed**
   - The calculator accepts decimal values
   - Example: 0.5, 1.25, 3.14159

### After Solving

1. **Verify Feasibility**
   - Check if solution makes sense
   - Can you actually implement it?

2. **Check Constraint Satisfaction**
   - Manually verify a few constraints
   - Ensure solution doesn't violate any limit

3. **Interpret in Context**
   - Round if necessary (can't make 2.7 cars)
   - Consider practical implications

## Troubleshooting

### Problem: "Invalid input" Error

**Cause**: Non-numeric values in number fields

**Solution**:
- Check all inputs are numbers
- Remove any text or special characters
- Use decimals, not fractions (0.5 not 1/2)

### Problem: Unexpected Results

**Cause**: Incorrect formulation

**Solution**:
- Review constraint operators
- Check if you want ≤ instead of ≥ or vice versa
- Verify objective coefficients
- Ensure problem is correctly formulated

### Problem: Page Won't Load

**Cause**: Application not running

**Solution**:
1. Ensure Flask server is running
2. Check terminal for errors
3. Verify port 5000 is not in use
4. Restart application: `python main.py`

### Problem: Solution Seems Wrong

**Cause**: Mathematical formulation issue

**Solution**:
1. Write out problem on paper
2. Verify each constraint mathematically
3. Check if problem has a feasible solution
4. Try a simpler version first

### Problem: Form Inputs Not Appearing

**Cause**: JavaScript or browser issue

**Solution**:
- Refresh the page
- Try a different browser
- Clear browser cache
- Check browser console for errors

## FAQ

### General Questions

**Q: Is this calculator free?**
A: Yes, it's completely free and open source.

**Q: Do I need to create an account?**
A: No, no account or registration needed.

**Q: Can I use this for commercial purposes?**
A: Yes, it's licensed under MIT License.

**Q: Does it work offline?**
A: Yes, if you run it locally on your machine.

### Technical Questions

**Q: What solver does it use?**
A: PuLP library with default solver (usually CBC).

**Q: Can it handle integer programming?**
A: Currently no, only continuous variables.

**Q: What's the maximum problem size?**
A: Up to 100 variables and 50 constraints.

**Q: Can I save my problems?**
A: Currently no, but this is a planned feature.

### Mathematical Questions

**Q: What if my problem has no solution?**
A: The solver will indicate infeasibility.

**Q: Can I have equality constraints?**
A: Yes, use the "=" operator.

**Q: Are variables always non-negative?**
A: Yes, all variables have x ≥ 0 constraint.

**Q: Can I have unbounded solutions?**
A: The solver will indicate if solution is unbounded.

### Usage Questions

**Q: How accurate are the results?**
A: Very accurate, using professional-grade solver.

**Q: Can I export results?**
A: Not currently, but you can copy from the page.

**Q: Can I solve multiple problems at once?**
A: No, solve one at a time.

**Q: Is there a mobile app?**
A: No, but the website works on mobile browsers.

## Additional Help

### Educational Resources

For learning more about linear programming:
- See [EXAMPLES.md](EXAMPLES.md) for detailed examples
- Check [API.md](API.md) for technical details
- Visit [PuLP documentation](https://coin-or.github.io/pulp/)

### Getting Support

If you need help:
1. **Read this guide** thoroughly
2. **Check examples** in EXAMPLES.md
3. **Report issues** on GitHub
4. **Contact developer**: santiagosanchezmarquez@gmail.com

### Contributing

Want to improve the calculator?
- See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines
- Submit bug reports or feature requests
- Contribute code via pull requests

## Quick Reference Card

### Problem Setup Checklist
- [ ] Define variables (x₁, x₂, ...)
- [ ] Write objective function
- [ ] List all constraints
- [ ] Determine optimization type
- [ ] Ensure units are consistent

### Input Guide
```
Step 1: Enter dimensions
  - Variables: 1-100
  - Constraints: 1-50
  - Type: Max or Min

Step 2: Enter coefficients
  - Objective: one per variable
  - Constraints: matrix of coefficients
  - Operators: ≤, ≥, or =
  - Constants: right-hand side values

Step 3: Solve and interpret
```

### Operator Guide
- `≤` : Less than or equal (capacity limits)
- `≥` : Greater than or equal (minimum requirements)
- `=` : Exactly equal (exact allocation)

---

**User Guide Version**: 1.0.0

**Last Updated**: 2024

**Created by**: λ-SanchoDev

For questions: santiagosanchezmarquez@gmail.com
