# 📚 Installation & Setup Guide

## Prerequisites

### System Requirements
- Python 3.8 or higher
- Git (for version control)
- ~500 MB free disk space
- Internet connection (for installing packages)

### Supported Platforms
- ✅ macOS 10.14+
- ✅ Windows 10/11
- ✅ Linux (Ubuntu 18.04+, Fedora, etc.)

---

## Installation Steps

### Step 1: Clone the Repository

```bash
# Using HTTPS
git clone https://github.com/yourusername/knapsack-problem-optimization.git
cd knapsack-problem-optimization

# Or using SSH
git clone git@github.com:yourusername/knapsack-problem-optimization.git
cd knapsack-problem-optimization
```

### Step 2: Create Virtual Environment

#### On macOS/Linux:
```bash
# Create virtual environment
python3 -m venv venv

# Activate it
source venv/bin/activate
```

#### On Windows:
```bash
# Create virtual environment
python -m venv venv

# Activate it
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
# Upgrade pip first
pip install --upgrade pip

# Install all requirements
pip install -r requirements.txt
```

This will install:
- PuLP (Linear programming)
- Pandas (Data manipulation)
- NumPy (Numerical computing)
- Matplotlib/Seaborn (Visualization)
- Jupyter (Interactive notebooks)
- And other development tools

### Step 4: Verify Installation

```bash
# Check Python version
python --version

# Check PuLP installation
python -c "import pulp; print(pulp.__version__)"

# Check Jupyter
jupyter --version
```

---

## Running the Analysis

### Option 1: Using Jupyter Notebook (Recommended)

```bash
# Start Jupyter
jupyter notebook

# Or use Jupyter Lab (more modern)
jupyter lab

# Then open: notebooks/mochila.ipynb
```

The browser will open automatically. Click on `mochila.ipynb` to start.

### Option 2: From Command Line

```bash
# Run all cells in the notebook
jupyter nbconvert --to notebook --execute notebooks/mochila.ipynb \
  --output=output.ipynb
```

### Option 3: Using Python Script

```bash
# Convert notebook to Python script
jupyter nbconvert --to script notebooks/mochila.ipynb

# Run the script
python mochila.py
```

---

## Project Structure

```
knapsack-problem-optimization/
├── README.md                 # Main documentation
├── LICENSE                   # MIT License
├── requirements.txt          # Python dependencies
├── .gitignore               # Git ignore rules
│
├── notebooks/
│   └── mochila.ipynb        # Main analysis notebook
│
├── data/
│   ├── datos_peso.csv       # Input: weights (29 cases)
│   ├── datos_beneficio.csv  # Input: benefits (29 cases)
│   └── resultados_*.csv     # Output: results table
│
├── src/
│   ├── __init__.py
│   ├── knapsack_solver.py   # CBC solver
│   ├── greedy_solver.py     # Greedy heuristic
│   └── utils.py             # Utilities
│
├── results/
│   ├── grafico_*.png        # All visualization graphs
│   ├── resumen_*.html       # HTML summary report
│   └── resumen_*.txt        # Text summary report
│
└── docs/
    ├── ALGORITHMS.md        # Algorithm details
    ├── RESULTS.md          # Results analysis
    └── INSTALL.md          # This file
```

---

## Quick Start Checklist

```
□ Clone repository
□ Create virtual environment
□ Activate venv
□ Install requirements
□ Navigate to project folder
□ Run: jupyter notebook
□ Open: notebooks/mochila.ipynb
□ Execute: Cell > Run All
□ View results and graphs
□ Check output files in results/
```

---

## Troubleshooting

### Issue: "Python command not found"
**Solution:**
```bash
# Use python3 explicitly
python3 -m venv venv
python3 -m pip install -r requirements.txt
```

### Issue: "PuLP solver not found"
**Solution:**
PuLP will automatically download CBC solver on first use. If that fails:
```bash
# Install CBC explicitly
pip install pyomo[solvers]
```

### Issue: "Jupyter command not found"
**Solution:**
```bash
# Ensure jupyter is installed
pip install jupyter jupyterlab

# Run with module syntax
python -m jupyter notebook
```

### Issue: "Permission denied" on macOS/Linux
**Solution:**
```bash
# Give execute permissions
chmod +x venv/bin/activate
```

### Issue: "ModuleNotFoundError" when running notebook
**Solution:**
```bash
# Make sure venv is activated
# Check: prompt should show (venv)

# Reinstall packages
pip install -r requirements.txt --force-reinstall
```

---

## IDE Setup

### VS Code

1. **Install Extensions:**
   - Python (Microsoft)
   - Jupyter (Microsoft)
   - Pylance (optional, for linting)

2. **Select Python Interpreter:**
   - `Ctrl+Shift+P` → "Python: Select Interpreter"
   - Choose: `./venv/bin/python`

3. **Open Notebook:**
   - Right-click `mochila.ipynb`
   - "Open With..." → "Jupyter"

### PyCharm

1. **Configure Interpreter:**
   - Settings → Project → Python Interpreter
   - Click gear icon → Add → Existing Environment
   - Select: `./venv/bin/python`

2. **Open Notebook:**
   - File → Open → `mochila.ipynb`
   - PyCharm will automatically recognize it

### Jupyter Lab (Recommended)

```bash
# Install Jupyter Lab
pip install jupyterlab

# Start with extensions
jupyter lab

# Open notebook from UI
```

---

## Running Tests

```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_solvers.py

# Run with coverage
pytest --cov=src tests/
```

---

## Development Workflow

### Making Changes

```bash
# Create new branch
git checkout -b feature/your-feature-name

# Make your changes
# Edit files, run experiments, etc.

# Commit changes
git add .
git commit -m "Description of changes"

# Push to GitHub
git push origin feature/your-feature-name
```

### Creating Pull Request

1. Push your branch to GitHub
2. Go to repository on GitHub
3. Click "New Pull Request"
4. Select your branch
5. Write description
6. Submit for review

---

## Documentation

### Notebook Cells

The main notebook (`mochila.ipynb`) contains:

1. **Installation** - Install dependencies
2. **Data Loading** - Load CSV files
3. **Algorithms** - Heuristic implementations
4. **Exact Solver** - CBC configuration
5. **Comparative Analysis** - Run all 29 test cases
6. **Results Tables** - Detailed comparison
7. **Visualizations** - 6 comprehensive graphs
8. **Summary** - Executive summary

### Additional Documentation

- `docs/ALGORITHMS.md` - Technical details
- `docs/RESULTS.md` - Analysis and findings
- `docs/INSTALL.md` - This guide

---

## Next Steps

1. ✅ Installation complete
2. 🚀 Run: `jupyter notebook`
3. 📊 Execute the notebook
4. 📈 Review graphs and results
5. 🔬 Analyze findings
6. 🎯 Apply recommendations

---

## Getting Help

### Documentation
- README.md - Overview and quick start
- ALGORITHMS.md - Algorithm details
- RESULTS.md - Analysis and interpretation

### Online Resources
- [PuLP Documentation](https://coin-or.github.io/pulp/)
- [Jupyter Documentation](https://jupyter.org/documentation)
- [Knapsack Problem](https://en.wikipedia.org/wiki/Knapsack_problem)

### Community
- GitHub Issues - Report bugs or ask questions
- GitHub Discussions - Community support

---

## System Information

To help with troubleshooting, gather your system info:

```bash
# Python version
python --version

# Package versions
pip list

# System info
python -c "import platform; print(platform.platform())"

# PuLP solver info
python -c "import pulp; print(pulp.listSolvers(onlyAvailable=True))"
```

Share this info when reporting issues! ✨

---

**Last Updated**: November 13, 2025
**Version**: 1.0.0
