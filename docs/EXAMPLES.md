# Examples and Use Cases

This document provides practical examples of linear programming problems that can be solved using the Linear Programming Calculator.

## Table of Contents

- [Basic Examples](#basic-examples)
- [Business Applications](#business-applications)
- [Manufacturing and Production](#manufacturing-and-production)
- [Transportation and Logistics](#transportation-and-logistics)
- [Resource Allocation](#resource-allocation)
- [Diet and Nutrition](#diet-and-nutrition)
- [Advanced Examples](#advanced-examples)

## Basic Examples

### Example 1: Simple Maximization Problem

**Problem Statement**:
A company produces two products, A and B. Product A gives a profit of $3 per unit, and Product B gives a profit of $2 per unit. The company has the following constraints:
- Total production cannot exceed 4 units
- 2 units of A plus 1 unit of B cannot exceed 5 units

Find the production quantities that maximize profit.

**Mathematical Formulation**:
```
Maximize: Z = 3x₁ + 2x₂

Subject to:
  x₁ + x₂ ≤ 4
  2x₁ + x₂ ≤ 5
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2
- Number of constraints: 2
- Optimization type: Maximize
- Objective coefficients: 3, 2
- Constraint 1: 1, 1, ≤, 4
- Constraint 2: 2, 1, ≤, 5

**Solution**:
- x₁ = 1
- x₂ = 3
- Maximum profit = $9

---

### Example 2: Simple Minimization Problem

**Problem Statement**:
A company needs to meet a minimum requirement while minimizing costs. Variable x₁ costs $2 per unit and x₂ costs $3 per unit. Constraints:
- x₁ + x₂ must be at least 5
- 2x₁ + x₂ must be at least 8

**Mathematical Formulation**:
```
Minimize: Z = 2x₁ + 3x₂

Subject to:
  x₁ + x₂ ≥ 5
  2x₁ + x₂ ≥ 8
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2
- Number of constraints: 2
- Optimization type: Minimize
- Objective coefficients: 2, 3
- Constraint 1: 1, 1, ≥, 5
- Constraint 2: 2, 1, ≥, 8

**Solution**:
- x₁ = 3
- x₂ = 2
- Minimum cost = $12

---

## Business Applications

### Example 3: Product Mix Optimization

**Problem Statement**:
A furniture manufacturer produces chairs and tables. Each chair requires 2 hours of labor and 4 units of wood, yielding $45 profit. Each table requires 3 hours of labor and 6 units of wood, yielding $80 profit. Available resources:
- Labor: 60 hours
- Wood: 120 units

Find the optimal production mix.

**Mathematical Formulation**:
```
Maximize: Z = 45x₁ + 80x₂

Subject to:
  2x₁ + 3x₂ ≤ 60  (labor)
  4x₁ + 6x₂ ≤ 120 (wood)
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2 (chairs, tables)
- Number of constraints: 2
- Optimization type: Maximize
- Objective coefficients: 45, 80
- Constraint 1: 2, 3, ≤, 60
- Constraint 2: 4, 6, ≤, 120

**Solution**:
- Chairs (x₁) = 30
- Tables (x₂) = 0
- Maximum profit = $1,350

**Interpretation**: Produce only chairs for maximum profit given the resource constraints.

---

### Example 4: Advertising Budget Allocation

**Problem Statement**:
A company has $10,000 for advertising. They can advertise on TV ($500 per ad, 5000 reach) or radio ($200 per ad, 1500 reach). Constraints:
- Budget: $10,000
- Must run at least 15 total ads
- TV ads cannot exceed 12

Maximize total reach.

**Mathematical Formulation**:
```
Maximize: Z = 5000x₁ + 1500x₂

Subject to:
  500x₁ + 200x₂ ≤ 10000  (budget)
  x₁ + x₂ ≥ 15           (minimum ads)
  x₁ ≤ 12                (TV limit)
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2 (TV ads, Radio ads)
- Number of constraints: 3
- Optimization type: Maximize
- Objective coefficients: 5000, 1500
- Constraint 1: 500, 200, ≤, 10000
- Constraint 2: 1, 1, ≥, 15
- Constraint 3: 1, 0, ≤, 12

---

## Manufacturing and Production

### Example 5: Production Planning

**Problem Statement**:
A factory produces three products. Production hours, materials, and profits:

| Product | Hours | Materials | Profit |
|---------|-------|-----------|--------|
| A       | 2     | 3         | $40    |
| B       | 3     | 2         | $50    |
| C       | 1     | 4         | $30    |

Available: 100 hours, 120 units of materials

**Mathematical Formulation**:
```
Maximize: Z = 40x₁ + 50x₂ + 30x₃

Subject to:
  2x₁ + 3x₂ + x₃ ≤ 100  (hours)
  3x₁ + 2x₂ + 4x₃ ≤ 120 (materials)
  x₁, x₂, x₃ ≥ 0
```

**Input to Calculator**:
- Number of variables: 3
- Number of constraints: 2
- Optimization type: Maximize
- Objective coefficients: 40, 50, 30
- Constraint 1: 2, 3, 1, ≤, 100
- Constraint 2: 3, 2, 4, ≤, 120

---

### Example 6: Assembly Line Optimization

**Problem Statement**:
An assembly line produces two products. Constraints on three workstations:

| Workstation | Product A (min) | Product B (min) | Available Time |
|-------------|-----------------|-----------------|----------------|
| 1           | 5               | 3               | 150            |
| 2           | 2               | 4               | 120            |
| 3           | 4               | 2               | 100            |

Profit: $10 for A, $8 for B

**Mathematical Formulation**:
```
Maximize: Z = 10x₁ + 8x₂

Subject to:
  5x₁ + 3x₂ ≤ 150
  2x₁ + 4x₂ ≤ 120
  4x₁ + 2x₂ ≤ 100
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2
- Number of constraints: 3
- Optimization type: Maximize
- Objective coefficients: 10, 8
- Constraint 1: 5, 3, ≤, 150
- Constraint 2: 2, 4, ≤, 120
- Constraint 3: 4, 2, ≤, 100

---

## Transportation and Logistics

### Example 7: Shipping Cost Minimization

**Problem Statement**:
A company ships products from 2 warehouses to 2 stores. Shipping costs:

| From\To | Store 1 | Store 2 | Supply |
|---------|---------|---------|--------|
| Warehouse 1 | $4 | $6 | 100 |
| Warehouse 2 | $5 | $3 | 150 |
| **Demand** | 120 | 130 | |

Minimize shipping costs while meeting demand.

**Mathematical Formulation**:
Let x₁ = W1→S1, x₂ = W1→S2, x₃ = W2→S1, x₄ = W2→S2

```
Minimize: Z = 4x₁ + 6x₂ + 5x₃ + 3x₄

Subject to:
  x₁ + x₂ ≤ 100      (W1 supply)
  x₃ + x₄ ≤ 150      (W2 supply)
  x₁ + x₃ = 120      (S1 demand)
  x₂ + x₄ = 130      (S2 demand)
  x₁, x₂, x₃, x₄ ≥ 0
```

**Input to Calculator**:
- Number of variables: 4
- Number of constraints: 4
- Optimization type: Minimize
- Objective coefficients: 4, 6, 5, 3
- Constraint 1: 1, 1, 0, 0, ≤, 100
- Constraint 2: 0, 0, 1, 1, ≤, 150
- Constraint 3: 1, 0, 1, 0, =, 120
- Constraint 4: 0, 1, 0, 1, =, 130

---

## Resource Allocation

### Example 8: Workforce Scheduling

**Problem Statement**:
A call center needs to schedule workers. Each shift has different costs and requirements:

| Shift | Cost/Worker | Workers Needed |
|-------|-------------|----------------|
| Morning | $100 | 15 |
| Afternoon | $80 | 20 |
| Night | $120 | 10 |

Workers can work max 2 shifts. Minimize total cost.

**Mathematical Formulation**:
```
Minimize: Z = 100x₁ + 80x₂ + 120x₃

Subject to:
  x₁ ≥ 15  (morning requirement)
  x₂ ≥ 20  (afternoon requirement)
  x₃ ≥ 10  (night requirement)
  x₁, x₂, x₃ ≥ 0
```

**Input to Calculator**:
- Number of variables: 3
- Number of constraints: 3
- Optimization type: Minimize
- Objective coefficients: 100, 80, 120
- Constraint 1: 1, 0, 0, ≥, 15
- Constraint 2: 0, 1, 0, ≥, 20
- Constraint 3: 0, 0, 1, ≥, 10

---

## Diet and Nutrition

### Example 9: Diet Optimization

**Problem Statement**:
Plan a diet with minimum cost while meeting nutritional requirements. Two foods:

| Nutrient | Food A (per unit) | Food B (per unit) | Minimum Required |
|----------|-------------------|-------------------|------------------|
| Calories | 200 | 300 | 2000 |
| Protein (g) | 10 | 15 | 50 |
| Vitamins | 5 | 3 | 30 |

Cost: Food A = $2, Food B = $3

**Mathematical Formulation**:
```
Minimize: Z = 2x₁ + 3x₂

Subject to:
  200x₁ + 300x₂ ≥ 2000  (calories)
  10x₁ + 15x₂ ≥ 50      (protein)
  5x₁ + 3x₂ ≥ 30        (vitamins)
  x₁, x₂ ≥ 0
```

**Input to Calculator**:
- Number of variables: 2
- Number of constraints: 3
- Optimization type: Minimize
- Objective coefficients: 2, 3
- Constraint 1: 200, 300, ≥, 2000
- Constraint 2: 10, 15, ≥, 50
- Constraint 3: 5, 3, ≥, 30

---

## Advanced Examples

### Example 10: Investment Portfolio

**Problem Statement**:
Invest in 3 opportunities with different returns and risks. Maximum investment $100,000. Constraints:
- Stock A: 12% return, max 40% of portfolio
- Stock B: 8% return, max 50% of portfolio
- Bonds: 5% return, at least 20% of portfolio
- Total high-risk (A+B) cannot exceed 70%

**Mathematical Formulation**:
```
Maximize: Z = 0.12x₁ + 0.08x₂ + 0.05x₃

Subject to:
  x₁ + x₂ + x₃ ≤ 100000     (total budget)
  x₁ ≤ 40000                (stock A limit)
  x₂ ≤ 50000                (stock B limit)
  x₃ ≥ 20000                (bonds minimum)
  x₁ + x₂ ≤ 70000           (risk limit)
  x₁, x₂, x₃ ≥ 0
```

**Input to Calculator**:
- Number of variables: 3
- Number of constraints: 5
- Optimization type: Maximize
- Objective coefficients: 0.12, 0.08, 0.05
- Constraint 1: 1, 1, 1, ≤, 100000
- Constraint 2: 1, 0, 0, ≤, 40000
- Constraint 3: 0, 1, 0, ≤, 50000
- Constraint 4: 0, 0, 1, ≥, 20000
- Constraint 5: 1, 1, 0, ≤, 70000

---

## Tips for Using the Calculator

### Best Practices

1. **Start Simple**: Begin with 2 variables and 2 constraints to understand the interface
2. **Check Your Math**: Verify constraint coefficients before solving
3. **Interpret Results**: Understand what each variable represents in your context
4. **Validate Solutions**: Check if the solution makes sense for your problem

### Common Mistakes to Avoid

1. **Wrong Operators**: Ensure you use the correct inequality (≤, ≥, =)
2. **Units**: Keep all units consistent
3. **Sign Errors**: Double-check positive/negative coefficients
4. **Constraint Direction**: Verify if constraints should be ≤ or ≥

### Problem Formulation Checklist

- [ ] Clearly defined decision variables
- [ ] Objective function with correct coefficients
- [ ] All constraints identified
- [ ] Correct inequality directions
- [ ] Non-negativity considered
- [ ] Units are consistent
- [ ] Problem is feasible (has a solution)

## Additional Resources

### Learning Linear Programming

- **Books**:
  - "Introduction to Linear Optimization" by Bertsimas and Tsitsiklis
  - "Linear Programming" by Vasek Chvátal

- **Online Courses**:
  - Coursera: Optimization Methods
  - MIT OpenCourseWare: Linear Programming

- **Practice Problems**:
  - [Linear Programming Problems and Solutions](https://example.com)

### Real-World Applications

Linear programming is used in:
- **Airlines**: Crew scheduling, route planning
- **Manufacturing**: Production planning, inventory management
- **Finance**: Portfolio optimization, risk management
- **Logistics**: Supply chain optimization, vehicle routing
- **Agriculture**: Crop planning, resource allocation
- **Energy**: Power generation scheduling

## Need Help?

If you need assistance with formulating your problem:
- Email: santiagosanchezmarquez@gmail.com
- GitHub: [@Sanchochx](https://github.com/Sanchochx)

---

**Examples Guide Version**: 1.0.0

**Last Updated**: 2024

**Compiled by**: λ-SanchoDev
