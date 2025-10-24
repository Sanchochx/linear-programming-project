# Contributing to Linear Programming Calculator

First off, thank you for considering contributing to Linear Programming Calculator! It's people like you that make this project better for everyone.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Enhancements](#suggesting-enhancements)

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When you create a bug report, include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps to reproduce the problem**
- **Provide specific examples** (input values, screenshots, etc.)
- **Describe the behavior you observed** and what you expected to see
- **Include your environment details** (OS, Python version, browser)

### Suggesting Enhancements

Enhancement suggestions are welcome! When suggesting an enhancement:

- **Use a clear and descriptive title**
- **Provide a detailed description** of the suggested enhancement
- **Explain why this enhancement would be useful**
- **Include examples** of how it would work

### Pull Requests

Pull requests are the best way to propose changes to the codebase. We actively welcome your pull requests:

1. Fork the repo and create your branch from `main`
2. Make your changes
3. Test your changes thoroughly
4. Update documentation if needed
5. Submit your pull request

## Development Setup

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/YOUR-USERNAME/linear-programming-project-flask.git
   cd linear-programming-project-flask
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Create a new branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

5. **Make your changes and test**
   ```bash
   python main.py
   ```

## Coding Standards

### Python Code Style

- Follow [PEP 8](https://pep8.org/) style guide
- Use meaningful variable and function names
- Add docstrings to functions and classes
- Keep functions focused on a single task
- Maximum line length: 100 characters

### HTML/CSS Standards

- Use semantic HTML5 elements
- Maintain consistent indentation (2 spaces for HTML/CSS)
- Use Bootstrap 5 classes where appropriate
- Keep CSS organized and commented

### Example Python Function

```python
def calculate_optimal_solution(problem, decision_vars):
    """
    Calculate the optimal solution for a linear programming problem.

    Args:
        problem (pulp.LpProblem): The linear programming problem
        decision_vars (list): List of decision variables

    Returns:
        dict: Solution containing variable values and optimal value
    """
    problem.solve()
    solution = {
        'vars': [],
        'optimal_value': pulp.value(problem.objective)
    }
    for var in problem.variables():
        solution['vars'].append({var.name: var.varValue})
    return solution
```

## Commit Guidelines

### Commit Message Format

```
type: brief description

Detailed explanation of what changed and why
```

### Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation changes
- **style**: Code style changes (formatting, missing semicolons, etc.)
- **refactor**: Code refactoring
- **test**: Adding or updating tests
- **chore**: Maintenance tasks

### Examples

```
feat: add support for integer programming problems

Added functionality to specify integer constraints on variables.
Updated UI to include checkbox for integer variables.
```

```
fix: correct constraint operator handling

Fixed bug where equality constraints were not properly processed.
Now correctly handles =, <=, and >= operators.
```

## Pull Request Process

1. **Update the README.md** if your changes affect user-facing functionality
2. **Update the CHANGELOG.md** with details of your changes
3. **Ensure all tests pass** and the application runs without errors
4. **Reference any related issues** in your PR description
5. **Wait for review** - a maintainer will review your PR and may request changes
6. **Address feedback** if requested
7. **Celebrate** when your PR is merged!

### Pull Request Template

```markdown
## Description
Brief description of what this PR does

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Code refactoring

## Testing
Describe how you tested your changes

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have tested my changes
- [ ] I have updated the documentation
- [ ] I have added comments to complex code
- [ ] My changes generate no new warnings
```

## Testing Guidelines

Before submitting a PR, test the following:

1. **Basic Functionality**
   - Can you access all pages?
   - Does the navigation work correctly?
   - Can you submit forms without errors?

2. **Edge Cases**
   - What happens with 0 variables or constraints?
   - What happens with very large numbers?
   - What happens with invalid input?

3. **Different Scenarios**
   - Test maximization problems
   - Test minimization problems
   - Test all three constraint operators (≤, ≥, =)
   - Test with different numbers of variables and constraints

## Questions?

Feel free to reach out if you have questions:

- Email: santiagosanchezmarquez@gmail.com
- GitHub: [@Sanchochx](https://github.com/Sanchochx)

## Recognition

Contributors will be recognized in the project README. Thank you for your contributions!

---

**Happy Contributing!**

λ-SanchoDev
