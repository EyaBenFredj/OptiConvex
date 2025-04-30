
# 📊 Convex Optimization Project: KKT & Projected Gradient Descent

🎯 This project solves a **constrained convex optimization problem** using:
- Symbolic analysis with **Karush-Kuhn-Tucker (KKT)** conditions
- Numerical optimization using **Projected Gradient Descent (PGD)**
- Exact solution comparison using **CVXPY**

> 📁 You’ll find the full notebook, report, results, and comparison in this repository.

---

## 🧩 Problem Statement

We aim to minimize a **strictly convex quadratic function** subject to **convex linear inequality constraints**.

### 🔢 Objective Function

The function to minimize is the squared Euclidean norm:

\[
f(x, y, z) = x^2 + y^2 + z^2
\]

This is a strictly convex function because its Hessian is a positive definite diagonal matrix (2I₃).

### 📐 Constraints

The feasible region \( \mathcal{X} \) is defined by 5 convex constraints:

\[
\begin{cases}
x + y + z \leq 5 & \text{(constraint 1)} \\
x - y \leq 1 & \text{(constraint 2)} \\
x \geq 0 & \text{(constraint 3)} \\
y \geq 0 & \text{(constraint 4)} \\
z \geq 0 & \text{(constraint 5)}
\end{cases}
\]

Or equivalently, in standard form \( g_i(x) \leq 0 \):

\[
\begin{cases}
g_1(x, y, z) = x + y + z - 5 \leq 0 \\
g_2(x, y, z) = x - y - 1 \leq 0 \\
g_3(x) = -x \leq 0 \\
g_4(y) = -y \leq 0 \\
g_5(z) = -z \leq 0
\end{cases}
\]

---

## 📌 Mathematical Formulation

### ✅ Convexity

- **f(x, y, z)** is a convex function (quadratic with positive definite Hessian).
- All constraints are affine (i.e., linear), and hence convex sets.
- Thus, this is a **convex optimization problem**, and any local minimum is global.

---

## 🧠 Step 1: Karush-Kuhn-Tucker (KKT) Conditions

We define the Lagrangian:

\[
\mathcal{L}(x, y, z; \lambda_1, ..., \lambda_5) = f(x, y, z) + \sum_{i=1}^5 \lambda_i g_i(x, y, z)
\]

### 🧮 Stationarity (∇L = 0)

\[
\begin{cases}
2x + \lambda_1 + \lambda_2 - \lambda_3 = 0 \\
2y + \lambda_1 - \lambda_2 - \lambda_4 = 0 \\
2z + \lambda_1 - \lambda_5 = 0
\end{cases}
\]

### ✅ Primal Feasibility

All original constraints must be satisfied:

\[
g_i(x, y, z) \leq 0,\quad i = 1,...,5
\]

### ✅ Dual Feasibility

\[
\lambda_i \geq 0,\quad i = 1,...,5
\]

### ✅ Complementary Slackness

\[
\lambda_i g_i(x, y, z) = 0,\quad i = 1,...,5
\]

Solving this full nonlinear system gives the optimal point. We used **SymPy** to symbolically derive all conditions.

---

## 🚀 Step 2: Projected Gradient Descent (PGD)

PGD is an iterative algorithm for constrained optimization:

### 🔁 Algorithm:

Initialize \( x_0 = [x^{(0)}, y^{(0)}, z^{(0)}] \), step size \( \alpha > 0 \)

Repeat until convergence:
1. Take a gradient step:
   \[
   x_{k+1/2} = x_k - \alpha \nabla f(x_k)
   \]
   where \( \nabla f(x_k) = [2x_k, 2y_k, 2z_k] \)
2. Project onto feasible region:
   \[
   x_{k+1} = P_{\mathcal{X}}(x_{k+1/2})
   \]
   This is done by solving:
   \[
   x_{k+1} = \arg\min_{x' \in \mathcal{X}} ||x' - x_{k+1/2}||^2
   \]

This projection step is formulated and solved as a **convex quadratic program** using CVXPY.

---

## ✅ Step 3: Comparison with Exact Solution (CVXPY)

We also solved the same problem directly using CVXPY:

```python
cp.Problem(cp.Minimize(cp.sum_squares(x)), constraints).solve()
```

This gives the exact solution \( x^*_{\text{cvxpy}} \), which we compared to the result of PGD.

✅ PGD converged very close to this exact solution — confirming correctness.

---

## 📈 Results

- ✅ Convergence of PGD shown in `results/convergence_plot.png`
- ✅ Final solution: `x ≈ [ ..., ..., ... ]`
- ✅ Optimal value: `f(x*) ≈ ...`

> The PGD solution matches the CVXPY solution up to small numerical error — confirming the algorithm works correctly!

---

## 📂 Files

| File | Description |
|------|-------------|
| `optimization_project.ipynb` | Full Jupyter notebook with code, math & plots |
| `report.pdf` / `report.pptx` | Final report export |
| `video_presentation.mp4` | 5-minute explanation |
| `results/` | Contains plots and exported files |
| `README.md` | This file |

---

## 💡 How to Run

> Requirements:
```bash
pip install numpy matplotlib sympy cvxpy
```

> Then open in Jupyter:
```bash
jupyter notebook optimization_project.ipynb
```

---



