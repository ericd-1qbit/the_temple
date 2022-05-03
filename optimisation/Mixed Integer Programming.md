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
	x_1+x_2+x_3\geq15\\
	\text{impose}\; x_1\leq7\;x_2\leq3;x_3\l
	\end{align}
	$$
-  **MIP reduction**: reduce the number of feasible solutions to the LP relaxation. 

### Cutting Planes
### Heuristics
### Parallelism
