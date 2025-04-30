

# 🧠 Convex Optimization with Projected Gradient Descent (3D Problem)

## 📌 Project Overview

This project solves a **convex optimization problem with inequality constraints** using the **Projected Gradient Descent** algorithm.

It was developed as part of an academic coursework on **Techniques d’Optimisation**.

We solve a 3-variable quadratic minimization problem and apply:

- Mathematical analysis via KKT conditions
- 3D visualization of the feasible region
- Projected Gradient Descent (PGD) implementation
- Validation with CVXPY (exact convex solver)

---

## ✍️ Problem Statement

### Objective Function

\[
\min_{x, y, z} \quad f(x, y, z) = x^2 + y^2 + z^2
\]

This is a convex, differentiable quadratic function — geometrically, it measures the squared distance to the origin.

### Constraints (Feasible Region)

\[
\begin{cases}
x + y + z \leq 5 \\
x - y \leq 1 \\
x \geq 0 \\
y \geq 0 \\
z \geq 0
\end{cases}
\]

These define a **convex polyhedron** in ℝ³. Hence, the entire problem is **convex with inequality constraints**.

---

## 📐 Mathematical Analysis — KKT Conditions

We define the Lagrangian:

\[
L(x, y, z, \lambda_1, ..., \lambda_5) = x^2 + y^2 + z^2 + \lambda_1(x + y + z - 5) + \lambda_2(x - y - 1) - \lambda_3 x - \lambda_4 y - \lambda_5 z
\]

### Karush-Kuhn-Tucker (KKT) Conditions:

1. **Stationarity:**
\[
\begin{cases}
2x + \lambda_1 + \lambda_2 - \lambda_3 = 0 \\
2y + \lambda_1 - \lambda_2 - \lambda_4 = 0 \\
2z + \lambda_1 - \lambda_5 = 0
\end{cases}
\]

2. **Primal Feasibility:** All constraints must be satisfied

3. **Dual Feasibility:** \( \lambda_i \geq 0 \; \forall i \)

4. **Complementary Slackness:**
\[
\lambda_i g_i(x, y, z) = 0
\]

> These were derived symbolically using SymPy and matched our expectations from theory.

---

## ⚙️ Algorithm: Projected Gradient Descent (PGD)

PGD is used to solve constrained convex problems of the form:

\[
x_{k+1} = P_\mathcal{X}(x_k - \alpha_k \nabla f(x_k))
\]

Where:
- \( P_\mathcal{X} \) is the projection onto the feasible set \( \mathcal{X} \)
- \( \nabla f(x_k) = [2x, 2y, 2z] \)
- Step size \( \alpha_k \) is constant or adaptive

### Projection Step

We use CVXPY to project a point onto the feasible region:

```python
objective = Minimize(‖x_var - x_input‖²)
subject to: constraints defining the feasible set
```

---

## 📊 Screenshots & Visuals

### ✅ 3D Visualization of Feasible Region (Matplotlib)

> 📷 _Insert 3D scatter plot screenshot here_  
> ![Feasible Region](results/feasible_region.png)

---

### ✅ Convergence of PGD

> 📷 _Insert convergence plot (objective value vs iteration)_  
> ![Convergence](results/convergence_plot.png)

---

### ✅ Comparison with Exact Solution (CVXPY)

> PGD result:
```python
x ≈ [x1, y1, z1]
f(x) ≈ 𝑓₁
```

> CVXPY result:
```python
x* ≈ [x2, y2, z2]
f(x*) ≈ 𝑓₂
```

> ✔️ Difference: very small → confirms correct convergence.

> 📷 _Insert screenshot of printed values or comparison table_  
> ![Comparison](results/comparison_table.png)

---

## 📁 Project Structure

```
optimization-project/
│
├── optimization_project.ipynb       # Main notebook with code & explanations
├── report.pdf / report.pptx         # Final report version (optional export)
├── video_presentation.mp4           # ≤ 5 min screencast presentation (optional)
├── README.md                        # This file
│
├── results/                         # Auto-generated plots & results
│   ├── feasible_region.png
│   ├── convergence_plot.png
│   └── comparison_table.png
```

---

## 🚀 How to Run This Project

### Prerequisites:
- Python ≥ 3.8
- Jupyter Notebook
- Required packages:
```bash
pip install numpy matplotlib cvxpy sympy
```

### Running:
```bash
jupyter notebook Optimization.ipynb
```

---

## 🎓 Educational Takeaways

- 💡 How to model convex problems symbolically and numerically
- 🔍 How to apply KKT conditions and interpret them geometrically
- 🧮 How Projected Gradient Descent approximates constrained minima
- ✅ How to validate numerical results with exact solvers like CVXPY

---

*
---

## 📝 License

This project is intended for academic use only.
