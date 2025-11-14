# 🎒 Knapsack Problem Optimization: Comparative Analysis

## 📋 Project Overview

This repository presents a comprehensive comparative analysis of **two approaches** to solve the 0/1 Knapsack Problem:

1. **Exact Method (CBC)**: Branch & Bound algorithm guaranteeing optimal solutions
2. **Heuristic Method**: Greedy algorithm based on benefit/weight ratio

The project evaluates **29 different test cases** with varying problem sizes (10-20 items) and provides detailed performance metrics, visualizations, and recommendations.

### Key Results

| Metric | Value |
|--------|-------|
| **Speedup** | 1,679x faster (Heuristic vs Exact) |
| **Quality Gap** | 2.03% average (Heuristic vs Optimal) |
| **Time Savings** | 99.94% reduction in computation time |
| **Test Cases** | 29 cases evaluated |

---

## 📊 Project Structure

```
knapsack-problem-optimization/
├── README.md                          # This file
├── LICENSE                            # MIT License
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Git ignore rules
│
├── notebooks/
│   └── mochila.ipynb                 # Main Jupyter notebook with full analysis
│
├── data/
│   ├── datos_peso.csv                # Weight data for 29 test cases
│   ├── datos_beneficio.csv           # Benefit data for 29 test cases
│   └── resultados_comparativa.csv    # Output results table
│
├── src/
│   ├── __init__.py
│   ├── knapsack_solver.py            # CBC exact solver implementation
│   ├── greedy_solver.py              # Greedy heuristic implementation
│   └── utils.py                      # Utility functions
│
├── results/
│   ├── grafico_1_tiempo_promedio.png           # Graph 1: Average time comparison
│   ├── grafico_2_diferencia_tiempo_casos.png   # Graph 2: Time savings by case
│   ├── grafico_3_complejidad.png              # Graph 3: Scalability analysis
│   ├── grafico_4_brecha_valor_objetivo.png    # Graph 4: Solution quality gaps
│   ├── grafico_5_comparacion_integral.png     # Graph 5: Comprehensive analysis
│   ├── grafico_6_dashboard_final.png          # Graph 6: Executive dashboard
│   ├── resumen_analisis_mochila.html          # HTML summary report
│   └── resumen_analisis_mochila.txt           # Text summary report
│
└── docs/
    ├── ALGORITHMS.md                  # Detailed algorithm descriptions
    ├── RESULTS.md                     # Detailed results and analysis
    └── INSTALL.md                     # Installation and setup guide
```

---

## 🚀 Quick Start

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/knapsack-problem-optimization.git
cd knapsack-problem-optimization
```

2. **Create virtual environment:**
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

4. **Run Jupyter notebook:**
```bash
jupyter notebook notebooks/mochila.ipynb
```

---

## 📈 Key Findings

### Performance Metrics

#### 1. Computation Time
- **CBC (Exact)**: 29.92 ms average
- **Greedy Ratio**: 0.018 ms average
- **Speedup**: 1,679.7x

#### 2. Solution Quality
- **Average Gap**: 2.03% from optimal
- **Cases with <0.5% gap**: 31% (9/29 cases)
- **Cases with <1% gap**: 48% (14/29 cases)
- **Maximum gap**: 6.10%

#### 3. Scalability
- **CBC**: Exponential growth with problem size (exponential time)
- **Greedy Ratio**: Linear growth (O(n log n) complexity)

---

## 🎯 Algorithms

### Exact Method: CBC (Coin-or-Branch and Cut)

**Characteristics:**
- Guarantees optimal solution
- Uses branch & bound algorithm
- Exponential time complexity
- Suitable for n ≤ 50

**When to use:**
- ✅ Optimality is critical
- ✅ Problem size is small (n < 50)
- ✅ Solution quality is more important than speed

### Heuristic Method: Greedy Ratio

**Characteristics:**
- Fast O(n log n) algorithm
- Based on benefit/weight ratio
- No optimality guarantee
- Highly scalable

**When to use:**
- ✅ Speed is critical (real-time systems)
- ✅ Problem size is large (n > 100)
- ✅ ~2% gap from optimal is acceptable
- ✅ As initialization for metaheuristics

---

## 📊 Visualizations

### Graph 1: Average Time Comparison
Shows the dramatic speedup of the heuristic method (1,679x faster).

### Graph 2: Time Savings by Case
Demonstrates consistent >99% time savings across all test cases.

### Graph 3: Scalability Analysis
Illustrates exponential growth for CBC vs. linear for Greedy.

### Graph 4: Solution Quality Gap
Distribution of solution gaps showing 48% of cases with <1% gap.

### Graph 5: Comprehensive Analysis
Multi-panel visualization with:
- Objective values comparison
- Gap distribution histogram
- Time vs. quality correlation
- Box plots of computation times

### Graph 6: Executive Dashboard
KPI summary with:
- 1,679x speedup indicator
- 2.03% average gap indicator
- 99.94% time savings indicator
- Comprehensive performance metrics

---

## 📋 Test Cases

29 test cases were evaluated with:
- **Problem sizes**: 10-20 items per case
- **Weight range**: 50-120 units per item
- **Benefit range**: 1,000-2,000 units per item
- **Knapsack capacity**: 700 units (constant)

All data located in:
- `data/datos_peso.csv`
- `data/datos_beneficio.csv`

---

## 💡 Recommendations

### Decision Matrix

| Scenario | Recommended | Reason |
|----------|-------------|--------|
| n < 20, critical | CBC | Guarantees optimality |
| n < 20, acceptable gap | Greedy Ratio | 1,679x faster |
| 20 < n < 100 | Hybrid* | Best balance |
| n > 100 | Greedy Ratio | Only viable option |
| Real-time (<10ms) | Greedy Ratio | Critical requirement |
| Maximum quality | CBC + Local Search | Optimal + refinement |

*Hybrid: Use Greedy for initialization, CBC for validation/refinement

### Optimal Strategy

1. **Generate quick solution** using Greedy Ratio (<1ms)
2. **Use as initialization** and lower bound
3. **Apply local search** or branch & cut for refinement
4. **Result**: Excellent balance between quality and speed

---

## 📝 Results Summary

### Average Metrics

```
CBC (Exact Method):
  - Objective value:    13,508.00
  - Avg time:          29.92 ms
  - Guaranteed:        Optimal

Greedy Ratio (Heuristic):
  - Objective value:    13,232.00
  - Avg time:          0.018 ms
  - Gap from optimal:  2.03%

Speedup:              1,679.7x
Time savings:         99.94%
Quality trade-off:    98% of optimal
```

---

## 🛠️ Technologies Used

- **Python 3.8+**
- **PuLP**: Linear programming library (CBC solver)
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Matplotlib/Seaborn**: Data visualization
- **Jupyter**: Interactive notebook environment

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

Ricardo B. - Instituto Tecnológico y de Estudios Superiores de Monterrey

- 📧 Email: [your.email@tec.mx]
- 🔗 GitHub: [@yourusername]
- 💼 LinkedIn: [Your LinkedIn Profile]

---

## 📞 Support & Contributions

### Issues & Questions
- Open an [Issue](https://github.com/yourusername/knapsack-problem-optimization/issues) for bug reports
- Create a [Discussion](https://github.com/yourusername/knapsack-problem-optimization/discussions) for questions

### Contributing
Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -m 'Add improvement'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

## 📚 References

- **Linear Programming**: [PuLP Documentation](https://coin-or.github.io/pulp/)
- **Knapsack Problem**: [Wikipedia](https://en.wikipedia.org/wiki/Knapsack_problem)
- **Branch & Bound**: [Algorithm Details](https://en.wikipedia.org/wiki/Branch_and_bound)
- **Greedy Algorithms**: [Algorithm Design Manual](https://en.wikipedia.org/wiki/Greedy_algorithm)

---

## 🎓 Educational Value

This project serves as:
- Educational resource for algorithm comparison
- Practical example of trade-offs in algorithm selection
- Benchmark for optimization techniques
- Reference for mathematical modeling with Python

### Key Takeaways

✅ Not all problems require exact algorithms
✅ Sometimes 98% quality with 99.9% speedup is the better choice
✅ Algorithm selection depends on problem context
✅ Data-driven decision making leads to better solutions

---

**Last updated**: November 13, 2025

**Status**: ✅ Complete and tested on 29 cases
