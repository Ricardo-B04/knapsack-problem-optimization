# 🔬 Algorithms: Detailed Analysis

## Table of Contents
1. [Exact Method: CBC](#exact-method-cbc)
2. [Heuristic Method: Greedy Ratio](#heuristic-method-greedy-ratio)
3. [Complexity Analysis](#complexity-analysis)
4. [Performance Comparison](#performance-comparison)
5. [When to Use Each](#when-to-use-each)

---

## Exact Method: CBC

### Overview
**CBC (Coin-or-Branch and Cut)** is a complete MIP (Mixed Integer Programming) solver that guarantees finding the optimal solution to the 0/1 Knapsack Problem.

### Algorithm: Branch & Bound

```
ALGORITHM: Branch & Bound for 0/1 Knapsack
INPUT: Items with weights and values, knapsack capacity
OUTPUT: Optimal selection and maximum value

1. Create root node with LP relaxation (allows fractional items)
2. Solve LP relaxation → get upper bound on optimal value

3. WHILE (unexplored nodes exist):
   a. Select node with highest upper bound (best first strategy)
   b. IF upper bound ≤ current best integer solution:
      - Prune this branch (can't improve current best)
   c. ELSE:
      - Solve LP relaxation at this node
      - IF solution is integer:
        * Update best integer solution
      - ELSE:
        * Branch on fractional variable
        * Create two child nodes (variable = 0, variable = 1)
        * Add to queue

4. RETURN best integer solution found
```

### Mathematical Formulation

```
Maximize:     z = Σ(benefit[i] * x[i]) for i in 1..n

Subject to:   Σ(weight[i] * x[i]) ≤ capacity
              x[i] ∈ {0, 1} for all i
```

### Implementation Details

**PuLP Library:**
```python
import pulp

# Create problem
prob = pulp.LpProblem('Knapsack', pulp.LpMaximize)

# Decision variables: binary (0 or 1)
x = {i: pulp.LpVariable(f'x_{i}', cat='Binary') 
     for i in items}

# Objective function
prob += pulp.lpSum(value[i] * x[i] for i in items)

# Constraint: weight capacity
prob += pulp.lpSum(weight[i] * x[i] 
                   for i in items) <= capacity

# Solve
solver = pulp.PULP_CBC_CMD(msg=False)
prob.solve(solver)
```

### Complexity Analysis

**Time Complexity:**
- **Best case**: O(n log n) when solution is found quickly
- **Average case**: O(2^n) exponential
- **Worst case**: O(2^n) - may need to evaluate entire branch tree

**Space Complexity:**
- O(n + 2^d) where d is search tree depth
- Can be exponential in worst case

### Advantages ✅
- ✓ Guarantees optimal solution
- ✓ Provides upper and lower bounds
- ✓ Can handle very large capacity values
- ✓ Efficient pruning strategies
- ✓ Proven and mature algorithm

### Disadvantages ❌
- ✗ Exponential time complexity
- ✗ Not practical for large n (> 100)
- ✗ Time grows dramatically with problem size
- ✗ Unpredictable performance

### Practical Limits

| Problem Size | Expected Time |
|--------------|---------------|
| n = 10-20    | < 100 ms ✓    |
| n = 30-50    | 1-10 seconds  |
| n = 100      | Minutes+      |
| n = 1000     | Impractical   |

---

## Heuristic Method: Greedy Ratio

### Overview
**Greedy Ratio** is a fast approximation algorithm that selects items based on their benefit-to-weight ratio, achieving near-optimal solutions in linear time.

### Algorithm: Greedy Selection

```
ALGORITHM: Greedy by Benefit/Weight Ratio
INPUT: Items with weights and values, knapsack capacity
OUTPUT: Feasible solution (near-optimal)

1. FOR each item i:
   a. Calculate ratio[i] = value[i] / weight[i]

2. Sort items by ratio in DESCENDING order

3. Initialize:
   - current_weight = 0
   - selected_items = {}

4. FOR each item i in sorted order:
   a. IF current_weight + weight[i] ≤ capacity:
      - Add item i to selection
      - current_weight += weight[i]

5. RETURN selected items and total value
```

### Pseudocode

```
FUNCIÓN GreedyRatio(items, weights, values, capacity)
    ENTRADA: List of items, weights, values, capacity
    SALIDA: Selection of items (binary vector)
    
    1. ratios ← [values[i]/weights[i] for i in items]
    2. sorted_items ← sort(items, by=ratios, order=DESC)
    3. selection ← [0 for all items]
    4. current_weight ← 0
    
    5. PARA cada item en sorted_items:
    6.     SI current_weight + weight[item] ≤ capacity:
    7.         selection[item] ← 1
    8.         current_weight ← current_weight + weight[item]
    
    9. RETORNAR selection
FIN FUNCIÓN
```

### Implementation

```python
import time

def greedy_by_ratio(items, weights, values, capacity):
    """
    Greedy heuristic based on benefit/weight ratio.
    
    Args:
        items: List of item identifiers
        weights: Dict {item: weight}
        values: Dict {item: value}
        capacity: Maximum knapsack capacity
        
    Returns:
        Tuple: (selection_dict, total_value, total_weight, exec_time)
    """
    start = time.perf_counter()
    
    # Calculate ratio for each item
    ratios = {i: values[i] / weights[i] for i in items}
    
    # Sort by ratio (descending)
    sorted_items = sorted(items, key=lambda x: ratios[x], reverse=True)
    
    # Greedy selection
    selection = {i: 0 for i in items}
    current_weight = 0
    current_value = 0
    
    for item in sorted_items:
        if current_weight + weights[item] <= capacity:
            selection[item] = 1
            current_weight += weights[item]
            current_value += values[item]
    
    exec_time = time.perf_counter() - start
    
    return selection, current_value, current_weight, exec_time
```

### Complexity Analysis

**Time Complexity:**
- Sorting: O(n log n)
- Selection loop: O(n)
- **Total: O(n log n)**

**Space Complexity:**
- O(n) for storing ratios and selection

### Properties

1. **Approximation Ratio**
   - Worst-case: 50% of optimal value
   - Average-case: ~98% of optimal (empirical)
   - Best-case: 100% (optimal)

2. **Greedy Choice Property**
   - Local optimization doesn't guarantee global optimum
   - Counter-example: Items with high ratio but poor fit

3. **Deterministic**
   - Same input → always same output
   - Reproducible results

### Advantages ✅
- ✓ O(n log n) complexity - very fast
- ✓ Scales to very large n (1000+)
- ✓ Predictable and consistent performance
- ✓ Simple to implement and understand
- ✓ Excellent solution quality in practice

### Disadvantages ❌
- ✗ No optimality guarantee
- ✗ Can be suboptimal in specific cases
- ✗ Greedy choice doesn't always lead to global optimum

### Empirical Performance (From Analysis)

In our 29 test cases:
- Average gap from optimal: **2.03%**
- Gap < 0.5%: 31% of cases
- Gap < 1%: 48% of cases
- Gap < 2%: 59% of cases
- Maximum gap: 6.10%

---

## Complexity Analysis

### Theoretical Comparison

```
Metric              │ CBC (Exact)   │ Greedy Ratio
────────────────────┼───────────────┼─────────────
Time Complexity     │ O(2^n)        │ O(n log n)
Space Complexity    │ O(2^d)        │ O(n)
Optimality          │ Guaranteed    │ ~98% avg
Scalability         │ Poor (n<50)   │ Excellent
Predictability      │ Variable      │ Consistent
────────────────────┴───────────────┴─────────────
```

### Empirical Performance (29 Cases)

```
Metric                    │ CBC      │ Greedy Ratio
──────────────────────────┼──────────┼──────────────
Avg Time (ms)             │ 29.92    │ 0.018
Min Time (ms)             │ 21.54    │ 0.012
Max Time (ms)             │ 70.48    │ 0.033
Avg Objective Value       │ 13,508   │ 13,232
Gap from optimal (avg)    │ 0%       │ 2.03%
Speedup                   │ 1x       │ 1,679x
────────────────────────────┴──────────┴──────────────
```

### Scalability Growth Rates

**For problem size n:**

```
CBC (Exponential):
n=10:  ~20 ms
n=20:  ~30 ms
n=30:  ~100 ms
n=40:  ~500 ms
n=50:  ~2000 ms
n=100: Minutes
n=200: Hours

Greedy (Linear):
n=10:    0.01 ms
n=20:    0.02 ms
n=100:   0.05 ms
n=1000:  0.5 ms
n=10000: 5 ms
```

---

## Performance Comparison

### Graph Analysis

#### Time Growth

**CBC**: Non-linear, exponential growth
- Dependent on problem structure
- Branch & bound efficiency varies
- Some cases better than others

**Greedy**: Linear-logarithmic growth
- Very stable
- Highly predictable
- Minimal variation

#### Quality Comparison

**CBC**: Always optimal (100%)

**Greedy**: 
- 31% of cases: 99.5%+ of optimal
- 48% of cases: 99%+ of optimal
- 59% of cases: 98%+ of optimal

---

## When to Use Each

### Use CBC When:

1. **Optimality is Critical**
   - Medical/safety applications
   - Financial optimization
   - Legal compliance

2. **Problem Size is Small**
   - n < 20: Always practical
   - n < 50: Usually acceptable
   - n > 50: Use only if time permits

3. **Solution Validation**
   - Verify heuristic solutions
   - Benchmark against known optimal

4. **Academic/Research**
   - Need proven optimal reference
   - Theoretical analysis required

### Use Greedy Ratio When:

1. **Speed is Critical**
   - Real-time systems
   - Interactive applications
   - Hard time limits (<100ms)

2. **Problem Size is Large**
   - n > 100: CBC becomes impractical
   - n > 1000: Mandatory for speed

3. **Approximate Solution OK**
   - Business decisions (few % difference acceptable)
   - Exploratory analysis
   - Quick prototyping

4. **Initialization for Metaheuristics**
   - Genetic algorithms
   - Local search
   - Particle swarm optimization

### Hybrid Approach (RECOMMENDED):

```
Step 1: Get quick solution
  └─→ Use Greedy Ratio (< 1ms)

Step 2: Use as initialization
  └─→ Lower bound for B&B
  └─→ Initial solution for local search

Step 3: Refine (optional)
  └─→ Apply 2-opt or 3-opt local search
  └─→ Or run CBC with time limit

Step 4: Result
  └─→ Near-optimal solution
  └─→ Much faster than CBC alone
  └─→ Better than pure Greedy
```

---

## Recommendations by Scenario

| Scenario | n | Recommended | Reason |
|----------|---|------------|--------|
| Research paper | Any | CBC | Need optimal proof |
| Business decision | <20 | Greedy | Speed + accuracy |
| Real-time app | <100 | Greedy | <10ms requirement |
| Large-scale | >100 | Greedy | CBC infeasible |
| Verification | Any | CBC | Validate solutions |
| Production system | <50 | Hybrid | Best balance |
| Rapid prototyping | Any | Greedy | Development speed |

---

## References

- **Knapsack Problem**: https://en.wikipedia.org/wiki/Knapsack_problem
- **Branch & Bound**: https://en.wikipedia.org/wiki/Branch_and_bound
- **CBC Solver**: https://github.com/coin-or/Cbc
- **Greedy Algorithms**: Cormen, Leiserson, Rivest, Stein (2009)

