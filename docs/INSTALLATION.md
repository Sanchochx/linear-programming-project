# Installation Guide

This guide provides detailed instructions for installing and setting up the Linear Programming Calculator on various platforms.

## Table of Contents

- [System Requirements](#system-requirements)
- [Installation Methods](#installation-methods)
- [Platform-Specific Instructions](#platform-specific-instructions)
- [Troubleshooting](#troubleshooting)
- [Verification](#verification)
- [Next Steps](#next-steps)

## System Requirements

### Minimum Requirements

- **Operating System**: Windows 10/11, macOS 10.14+, or Linux (Ubuntu 18.04+, Debian, Fedora, etc.)
- **Python**: Version 3.7 or higher
- **RAM**: 512 MB minimum
- **Disk Space**: 100 MB free space
- **Browser**: Modern web browser (Chrome, Firefox, Safari, Edge)

### Recommended Requirements

- **Python**: Version 3.9 or higher
- **RAM**: 1 GB or more
- **Internet Connection**: For downloading dependencies

### Required Software

1. **Python 3.7+**: Download from [python.org](https://www.python.org/downloads/)
2. **pip**: Python package installer (usually included with Python)
3. **Git** (optional): For cloning the repository

## Installation Methods

### Method 1: Using Git (Recommended)

```bash
# Clone the repository
git clone https://github.com/Sanchochx/linear-programming-project-flask.git

# Navigate to the project directory
cd linear-programming-project-flask

# Install dependencies
pip install -r requirements.txt
```

### Method 2: Manual Download

1. Download the ZIP file from [GitHub repository](https://github.com/Sanchochx/linear-programming-project-flask)
2. Extract the ZIP file to your desired location
3. Open terminal/command prompt in the extracted folder
4. Run: `pip install -r requirements.txt`

### Method 3: Using Virtual Environment (Best Practice)

```bash
# Clone or download the repository
git clone https://github.com/Sanchochx/linear-programming-project-flask.git
cd linear-programming-project-flask

# Create virtual environment
python -m venv venv

# Activate virtual environment (see platform-specific commands below)

# Install dependencies
pip install -r requirements.txt
```

## Platform-Specific Instructions

### Windows

#### Step 1: Install Python

1. Download Python from [python.org](https://www.python.org/downloads/)
2. Run the installer
3. **Important**: Check "Add Python to PATH" during installation
4. Verify installation:
   ```cmd
   python --version
   pip --version
   ```

#### Step 2: Setup Project

```cmd
# Navigate to your desired directory
cd C:\Projects

# Clone repository (or download manually)
git clone https://github.com/Sanchochx/linear-programming-project-flask.git
cd linear-programming-project-flask

# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

#### Step 3: Run Application

```cmd
python main.py
```

### macOS

#### Step 1: Install Python

macOS comes with Python, but you may need to install Python 3:

```bash
# Check if Python 3 is installed
python3 --version

# If not installed, install using Homebrew
brew install python3
```

#### Step 2: Setup Project

```bash
# Navigate to your desired directory
cd ~/Projects

# Clone repository
git clone https://github.com/Sanchochx/linear-programming-project-flask.git
cd linear-programming-project-flask

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### Step 3: Run Application

```bash
python main.py
```

### Linux (Ubuntu/Debian)

#### Step 1: Install Python and Dependencies

```bash
# Update package list
sudo apt update

# Install Python 3 and pip
sudo apt install python3 python3-pip python3-venv git

# Verify installation
python3 --version
pip3 --version
```

#### Step 2: Setup Project

```bash
# Navigate to your desired directory
cd ~/projects

# Clone repository
git clone https://github.com/Sanchochx/linear-programming-project-flask.git
cd linear-programming-project-flask

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

#### Step 3: Run Application

```bash
python main.py
```

### Linux (Fedora/RHEL/CentOS)

```bash
# Install Python 3 and dependencies
sudo dnf install python3 python3-pip git

# Follow same steps as Ubuntu above
```

## Troubleshooting

### Common Issues and Solutions

#### Issue 1: "python: command not found"

**Solution**:
- Windows: Reinstall Python with "Add to PATH" checked
- macOS/Linux: Use `python3` instead of `python`

#### Issue 2: "pip: command not found"

**Solution**:
```bash
# Windows
python -m ensurepip --upgrade

# macOS/Linux
python3 -m ensurepip --upgrade
```

#### Issue 3: Permission Denied (Linux/macOS)

**Solution**:
```bash
# Don't use sudo with pip in virtual environment
# If you must install globally:
pip install --user -r requirements.txt
```

#### Issue 4: SSL Certificate Error

**Solution**:
```bash
# Upgrade pip
python -m pip install --upgrade pip

# Or install with trusted host
pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt
```

#### Issue 5: Port Already in Use

**Error**: `Address already in use`

**Solution**:
```python
# Edit main.py and change the port
if __name__ == '__main__':
    app.run(debug=True, port=5001)  # Change to different port
```

#### Issue 6: ModuleNotFoundError

**Solution**:
```bash
# Ensure virtual environment is activated
# Reinstall dependencies
pip install -r requirements.txt --force-reinstall
```

#### Issue 7: Flask-Bootstrap Version Conflict

**Solution**:
```bash
# Install specific compatible version
pip install Flask-Bootstrap5==2.0.0
```

### Dependency Issues

If you encounter dependency conflicts:

```bash
# Create fresh virtual environment
deactivate  # if currently in a venv
rm -rf venv  # or rmdir /s venv on Windows
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

## Verification

### Verify Installation

1. **Check if server starts**:
   ```bash
   python main.py
   ```
   You should see:
   ```
   * Running on http://127.0.0.1:5000
   * Debug mode: on
   ```

2. **Access the application**:
   - Open browser
   - Navigate to `http://127.0.0.1:5000/`
   - You should see the home page

3. **Test calculator**:
   - Click "Calculator" in navigation
   - Enter: Variables=2, Constraints=2, Optimization=Maximize
   - Fill in coefficients and solve a test problem

### Expected File Structure

After installation, your directory should look like:

```
linear-programming-project-flask/
├── venv/                  (if using virtual environment)
├── static/
│   ├── css/
│   │   └── styles.css
│   └── images/
├── templates/
│   ├── about.html
│   ├── calculator.html
│   ├── footer.html
│   ├── header.html
│   ├── index.html
│   ├── inicio.html
│   └── solution.html
├── docs/
├── main.py
├── requirements.txt
├── README.md
└── LICENSE
```

## Next Steps

After successful installation:

1. **Read the Documentation**:
   - [README.md](../README.md) - Project overview and usage
   - [API.md](API.md) - API documentation
   - [CONTRIBUTING.md](../CONTRIBUTING.md) - How to contribute

2. **Explore the Application**:
   - Try solving example problems
   - Experiment with different constraints
   - Test maximization and minimization

3. **Development Setup** (if contributing):
   - Set up your IDE (VS Code, PyCharm, etc.)
   - Install development dependencies
   - Read contributing guidelines

4. **Deployment** (for production use):
   - See [DEPLOYMENT.md](DEPLOYMENT.md) for production setup
   - Configure production WSGI server
   - Set up reverse proxy (nginx/Apache)

## Getting Help

If you encounter issues not covered here:

1. Check [GitHub Issues](https://github.com/Sanchochx/linear-programming-project-flask/issues)
2. Create a new issue with:
   - Your operating system and version
   - Python version
   - Error messages and logs
   - Steps to reproduce

3. Contact the maintainer:
   - Email: santiagosanchezmarquez@gmail.com
   - GitHub: [@Sanchochx](https://github.com/Sanchochx)

---

**Installation Guide Version**: 1.0.0

**Last Updated**: 2024

**Maintained by**: λ-SanchoDev
