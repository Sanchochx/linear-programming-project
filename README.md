# Linear Programming Calculator

A web-based Linear Programming problem solver built with Flask and PuLP. This application provides an intuitive interface to define and solve linear programming optimization problems with support for both maximization and minimization.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Overview

Linear Programming is an optimization method used to find the best solution to a mathematical problem subject to a set of linear constraints. This web application allows users to:

- Define custom linear programming problems
- Specify the number of variables and constraints
- Choose between maximization or minimization
- Get optimal solutions instantly

The application uses the PuLP library, which provides an intuitive Python interface for defining and solving linear and integer optimization problems.

## Features

- **User-Friendly Interface**: Clean, responsive web interface built with Bootstrap 5
- **Flexible Problem Definition**: Support for custom number of variables (1-100) and constraints (1-50)
- **Multiple Constraint Types**: Supports ≤, ≥, and = operators
- **Optimization Types**: Both maximization and minimization problems
- **Real-Time Solutions**: Instant calculation and display of optimal values
- **Educational Content**: Built-in information about linear programming and PuLP
- **Responsive Design**: Works on desktop and mobile devices

## Technologies Used

- **Backend**: Flask (Python web framework)
- **Optimization**: PuLP (Linear programming library)
- **Frontend**: Bootstrap 5
- **Template Engine**: Jinja2
- **Language**: Python 3.x

## Installation

### Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/Sanchochx/linear-programming-project-flask.git
   cd linear-programming-project-flask
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment**

   - Windows:
     ```bash
     venv\Scripts\activate
     ```

   - macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

4. **Install required dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Run the application**
   ```bash
   python main.py
   ```

6. **Access the application**

   Open your web browser and navigate to:
   ```
   http://127.0.0.1:5000/
   ```

## Usage

### Step 1: Define Your Problem

1. Navigate to the **Calculator** page from the navigation menu
2. Enter the number of variables for your problem
3. Enter the number of constraints
4. Select the optimization type (Maximize or Minimize)
5. Click **Continue**

### Step 2: Enter Coefficients

1. **Objective Function**: Enter the coefficients for each variable in the objective function
2. **Constraints**: For each constraint, enter:
   - Coefficients for each variable
   - Relationship operator (≤, ≥, or =)
   - Constant value on the right side

### Step 3: Get Solution

Click **Solve** to compute the optimal solution. The application will display:
- Optimal values for each variable
- The optimal value of the objective function

### Example Problem

**Maximize**: Z = 3x₁ + 2x₂

**Subject to**:
- x₁ + x₂ ≤ 4
- 2x₁ + x₂ ≤ 5
- x₁, x₂ ≥ 0

**Input**:
- Number of variables: 2
- Number of constraints: 2
- Optimization type: Maximize
- Objective coefficients: 3, 2
- Constraint 1: 1, 1, ≤, 4
- Constraint 2: 2, 1, ≤, 5

## Project Structure

```
linear-programming-project-main/
│
├── main.py                 # Main Flask application file
├── requirements.txt        # Python dependencies
├── README.md              # Project documentation
├── readme.txt             # Original ASCII art signature
│
├── static/                # Static files (CSS, images)
│   ├── css/
│   │   └── styles.css     # Custom CSS styles
│   └── images/
│       ├── usta_logo.jpg
│       ├── github.png
│       ├── instagram.jpg
│       └── linkedinLogo.png
│
└── templates/             # HTML templates
    ├── header.html        # Navigation header
    ├── footer.html        # Footer
    ├── inicio.html        # Home page
    ├── index.html         # Problem setup page
    ├── calculator.html    # Coefficient input page
    ├── solution.html      # Results display page
    └── about.html         # About/Contact page
```

## How It Works

### Backend Logic (main.py)

The application follows a three-step flow:

1. **Problem Definition** (`/index` route):
   - Accepts number of variables, constraints, and optimization type
   - Validates input ranges (1-100 variables, 1-50 constraints)

2. **Coefficient Input** (`/calculator` GET route):
   - Dynamically generates input fields based on problem dimensions
   - Allows users to enter objective function and constraint coefficients

3. **Problem Solving** (`/calculator` POST route):
   - Constructs a PuLP `LpProblem` object
   - Creates decision variables with non-negativity constraints
   - Adds objective function
   - Adds all constraints with appropriate operators
   - Solves using PuLP's default solver
   - Displays optimal variable values and objective function value

### Key Code Components

**Decision Variables**: Each variable is created with a lower bound of 0 (non-negativity)
```python
decision_vars = [pulp.LpVariable(f'x{i}', lowBound=0) for i in range(1, num_variables + 1)]
```

**Constraint Handling**: Supports three types of constraints
```python
if relation_operators[i] == '<=':
    problem += pulp.lpSum([...]) <= constraint_constants[i]
elif relation_operators[i] == '>=':
    problem += pulp.lpSum([...]) >= constraint_constants[i]
elif relation_operators[i] == '=':
    problem += pulp.lpSum([...]) == constraint_constants[i]
```

## Screenshots

(Add screenshots of your application here if available)

## Contributing

Contributions are welcome! Please check the [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines on how to contribute to this project.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

**Santiago Sánchez Márquez**
- Email: santiagosanchezmarquez@gmail.com
- Phone: +57 3229426989
- GitHub: [@Sanchochx](https://github.com/Sanchochx)
- LinkedIn: [Santiago Sánchez Márquez](https://www.linkedin.com/in/santiago-sánchez-márquez-821b742b1)
- Instagram: [@sanchx_s](https://www.instagram.com/sanchx_s/)

---

**λ-SanchoDev**

Built with dedication for solving linear programming problems efficiently.

### -------------------- λ-SanchoDev -------------------- ###
⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣀⣠⣤⣤⣴⣦⣤⣤⣄⣀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⢀⣤⣾⣿⣿⣿⣿⠿⠿⠿⠿⣿⣿⣿⣿⣶⣤⡀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⣠⣾⣿⣿⡿⠛⠉⠀⠀⠀⠀⠀⠀⠀⠀⠉⠛⢿⣿⣿⣶⡀⠀⠀⠀⠀
⠀⠀⠀⣴⣿⣿⠟⠁⠀⠀⠀⣶⣶⣶⣶⡆⠀⠀⠀⠀⠀⠀⠈⠻⣿⣿⣦⠀⠀⠀
⠀⠀⣼⣿⣿⠋⠀⠀⠀⠀⠀⠛⠛⢻⣿⣿⡀⠀⠀⠀⠀⠀⠀⠀⠙⣿⣿⣧⠀⠀
⠀⢸⣿⣿⠃⠀⠀⠀⠀⠀⠀⠀⠀⢀⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠸⣿⣿⡇⠀
⠀⣿⣿⡿⠀⠀⠀⠀⠀⠀⠀⠀⢀⣾⣿⣿⣿⣇⠀⠀⠀⠀⠀⠀⠀⠀⣿⣿⣿⠀
⠀⣿⣿⡇⠀⠀⠀⠀⠀⠀⠀⢠⣿⣿⡟⢹⣿⣿⡆⠀⠀⠀⠀⠀⠀⠀⣹⣿⣿⠀
⠀⣿⣿⣷⠀⠀⠀⠀⠀⠀⣰⣿⣿⠏⠀⠀⢻⣿⣿⡄⠀⠀⠀⠀⠀⠀⣿⣿⡿⠀
⠀⢸⣿⣿⡆⠀⠀⠀⠀⣴⣿⡿⠃⠀⠀⠀⠈⢿⣿⣷⣤⣤⡆⠀⠀⣰⣿⣿⠇⠀
⠀⠀⢻⣿⣿⣄⠀⠀⠾⠿⠿⠁⠀⠀⠀⠀⠀⠘⣿⣿⡿⠿⠛⠀⣰⣿⣿⡟⠀⠀
⠀⠀⠀⠻⣿⣿⣧⣄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⣾⣿⣿⠏⠀⠀⠀
⠀⠀⠀⠀⠈⠻⣿⣿⣷⣤⣄⡀⠀⠀⠀⠀⠀⠀⢀⣠⣴⣾⣿⣿⠟⠁⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠈⠛⠿⣿⣿⣿⣿⣿⣶⣶⣿⣿⣿⣿⣿⠿⠋⠁⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠉⠛⠛⠛⠛⠛⠛⠉⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
### -------------------- λ-SanchoDev -------------------- ###