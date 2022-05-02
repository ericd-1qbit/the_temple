
### Basic linear programming branch-and-bound

1. relax the original MIP: remove all of the integrality restrictions, eg. allow variables to be non-integer
2. solve this LP
	- does result fulfill all integrality restrictions? Lucky! Done.
	- if not: pick integer restricted variable whose solution in LP is fractional
3. Impose a restriction on the relaxed LP which EXCLUDES the fractional value.
	- eg. $x=1.337$ then imposeboth restrictions $1\leq x$ and $x \geq 2$



![[Pasted image 20220502121755.png]]