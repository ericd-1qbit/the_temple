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
		- 