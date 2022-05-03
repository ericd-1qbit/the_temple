# Mixed Integer Programming
Some of the optimisation variables are not discrete.


- **Mixed Integer Linear Programming (MILP):**
	- constraint and objective function are linear
$$
\begin{aligned}
&{\text{minimize}}&&\mathbf {c} ^{\mathrm {T} }\mathbf {x} \\
&{\text{subject to}}&&A\mathbf {x} = \mathbf {b} ,\\
&&&\mathbf{l}\leq\mathbf {x} \leq \mathbf {u} ,\\
&{\text{and}}&&\mathbf {x} \in \mathbb {Z} ^{n}\,{\text{or}}\,\mathbf {x} \in \mathbb {R} ^{n}
\end{aligned}$$
	- generally solved using [[Branch and Bound Algorithm]]
- **Mixed Integer Quadratic Programming (MIQP)**:
	- quadratic objective $$
\begin{aligned}
&{\text{minimize}}&&\mathbf {x}^T\mathbf {Q} ^{\mathrm {T} }\mathbf {x} +\mathbf {q}^{\mathrm {T}}\mathbf {x}\\
&{\text{subject to}}&&A\mathbf {x} = \mathbf {b} ,\\
&&&\mathbf{l}\leq\mathbf {x} \leq \mathbf {u} ,\\
&{\text{and}}&&\mathbf {x} \in \mathbb {Z} ^{n}\,{\text{or}}\,\mathbf {x} \in \mathbb {R} ^{n}
\end{aligned}$$
- **Mixed Integer Quadratically Constrained Programming (MIQCP)**:
	- quadratic constraints:
		- $$\begin{aligned}
&{\text{minimize}}&&\mathbf {x}^T\mathbf {Q} ^{\mathrm {T} }\mathbf {x} +\mathbf {q}^{\mathrm {T}}\mathbf {x}\\
&{\text{subject to}}&&A\mathbf {x} = \mathbf {b} ,\\
&&&\mathbf{l}\leq\mathbf {x} \leq \mathbf {u} ,\\
&&&\mathbf {x}^T\mathbf {Q_i} ^{\mathrm {T} }\mathbf {x} +\mathbf {q_i}^{\mathrm {T}}\mathbf {x}\leq b_i,\\
&{\text{and}}&&\mathbf {x} \in \mathbb {Z} ^{n}\,{\text{or}}\,\mathbf {x} \in \mathbb {R} ^{n}
\end{aligned}$$


## General Algorithm Components
### Presolve
Collection of strategies to reduce a given problem in size and complexity prior to applying the branch-and-bound algorithm. 

- **Size/LP-presolve reduction**: substitute variables by applying constraints for example. The validity does not depend on integrality restrictions.
	$$\begin{align}
	&x_1+x_2+x_3\geq15\\
	\text{constraint:}\; &x_1\leq7,\;x_2\leq3,\;x_3\leq5\\
	\text{reduction:}\; &x_1=7,\;x_2=3,\;x_3=5
	\end{align}
	$$
-  **MIP reduction**: reduce the number of feasible solutions to the LP relaxation, while the set of feasible integer solutions (no relaxation) remains the same. Very important tool for MIP solution algorithms!
	 	$$\begin{align}
	&2x_1+2x_2\leq1\\
	\text{constraint:}\; &x_1,x_2\in \mathbb{N}_0\\
	\text{reduction:}\; &x_1+x_2\leq\frac{1}{2}\\
	\text{integrality} &\Rightarrow x_1+x_2\leq0\\
	\text{non-negativity}&\Rightarrow x_1=x_2=0\;
	\end{align}
	$$

### Cutting Planes
- deep and extensive theory
- most important contributor to computational MIP advances
- basic idea: remove undesirable fractional solutions (like presolve) but during solution process w/o introducing sub-MIPs (unlike branching).
	- example: *knapsack cover*
$$\begin{align}
&6x_1+5x_2+7x_3+4x_4+5x_5\leq15\\
\text{constraint:}\; &x_i\in \{0,1\}\\
\text{a LP-relaxed solution:}\; &x_1=0,x_2=1,x_{3,4,5}=\frac{3}{4}\\
\text{observation:}\; &x_{3,4,5}=1\Rightarrow 7+4+5=16>15\;\\
\text{new constraint:}\; &\Rightarrow x_3+x_4+x_5\leq2\\
\text{removes solution:}\; &x_{3,4,5}=\frac{3}{4}
\end{align}$$
- ![[Pasted image 20220503085406.png]]

### Heuristics
Good incumbent nodes (eg. approximations to the optimal solutions) are important, as it might suffice to use a non-optimal solution in some settings.
Examnple of a heuristic approach: take a LP relaxed solution and try to find a solution with all integrality restrictions applied (by rounding for example). If the solution prooves to have a better objective value than the incumbent, replace and proceed with the branch and bound algorithm.
Multiple such heuristics exist in Gurobi.

### Parallelism
The search tree splits into sub-MIPs. Each can be solved in parallel. Especially effective for large search trees.

### Others
- mostly concerned with reduction of search tree size:
	- branch variable selection techniques
	- node presolve
	- symmetry detection 