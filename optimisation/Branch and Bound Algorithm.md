
### Basic linear programming branch-and-bound

1. relax the original MIP: remove all of the integrality restrictions, eg. allow variables to be non-integer
2. solve this LP
	- does result fulfill all integrality restrictions? Lucky! Done.
	- if not: pick integer restricted variable whose solution in LP is fractional
3. Impose a restriction on the relaxed LP which EXCLUDES the fractional value.
	- eg. $x=1.337$ then imposeboth restrictions $1\leq x$ and $x \geq 2$
		- original MIP $P_0$
		- first restriction - new MIP:  $1\leq x \rightarrow P_1$
		- second restriction - new MIP:  $x \geq 2 \rightarrow P_2$
	- *branch variable* $x$
	- *branched* at x producing *sub-MIPs* $P_1,P_2$ 
4. Calculate optimal solution for $P_{1/2}$. Choose solution which is better for $P_0$ or continue with branching.

##### Search Tree
The continuous splitting generates a tree:
- *nodes* of this tree are the generated MIPs
- *root node* is $P_0$
- *leaves*: not yet branched MIPs

![[Pasted image 20220502121755.png]]

#### Fathomed Nodes
Nodes which fulfill all the integrality requirements of the original MIP. No further branching is necessary - a *permanent leaf* of the search tree.

##### Incumbent Node
Fathomed node with best objective function value found at any point in the search.

##### Infeasible Nodes
Restriction applied by a branch to the current node is infeasible with the relaxation of the original MIP.

##### Less Optimal Nodes
Nodes with a solution but less optimal value than the current incumbent node can be fathomed, as their branching will not result in a better objective value.

#### Bounds
The objective function's value for an incumbent gives certain bounds to the original MIP.

##### Upper Bound
If we have a minimisation problem, then any given incumbent node forms an upper bound on the final solution's objective value.

##### Lower/Best Bound
The minimum objective value taken across all *leaf* nodes (eg. not all constraints applied?)

##### Gap
Difference between upper and lower bound. If the gap is zero, the optimal solution has been found.


