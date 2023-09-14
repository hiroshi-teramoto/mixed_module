Let us explain how to use the library in example_codimension_transverse_fold.exe (See 3.1.1 Example (transverse fold) in the paper).

In this example, the definition of the base ring is as follows: 

```Singular
nx = 2;
ny = 2;
ring R = (0,a), (x(1..nx),y(1..ny)), (M(imat),C);
```

In this implementation, all the parameters in the ring, "a" in the example above, are treated as parameters in comprehensive standard system. To use the library, you need to specify the family of variables $(X_i)_{i \in J}$. In this implementation, $X_1$ is the set of all the variables in the base ring. In this example, that is {x(1..nx), y(1..ny)}, where x(i) and y(j) correspond to $x_i$ and $y_i$ in the paper. You need to specify $X_2$, $X_3$. In the current implementation, X[i-1] = $X_i$ and the list of variables should be of type ideal. For example, 

```Singular
list X = list();
X[1] = ideal(y[1]);
X[2] = ideal(y[2]);
X[3] = ideal(0); // this correspond $X_3 = \emptyset$
```

In the subsequent lines, $\eta$ in the paper (See 2. Setting in the paper) is computed for the given X[1], X[2], and X[3]. For example, if $X[1] \cap X[2] = X[3]$ holds, then eta[1,2] = 3.

Ideals $E$ and $N$ specify the entire range of parameters $V(E) \setminus V(N)$ in which comprehensive standard system is computed. If you want to compute a comprehensive standard system for all the parameter range, set 

```Singular
ideal E = 0; // zero ideal
ideal N = 1; // ideal containing 1, that is, R
```

Then, $V(E)$ is the whole parameter range and $V(N) = \emptyset$ holds, and thus $V(E) \setminus V(N)$ is the whole parameter range. 

In this example, 

$M_1$ = TR1K;
$M_2$ = Q[1];
$M_3$ = Q[2];
$M_4$ = Q[3];

in the paper. 

Finally, you are ready to compute comprehensive standard system for $(M_i)_{i \in \{ 1,2,3,4 \}}$. $M_1$ is supposed to have finite $K$-codimension. 

```Singular
list Lg = cssm(X,eta,E,N,TR1K,Q);
```
### Parameters
- `X`: family of variables (Note that X[i-1] = $X_i$ in the paper)
- `eta` ( $=\eta$ ): $(\left| J \right|-1) \times (\left| J \right|-1)$ matrix of positive integer entries that satisfies $X[i] \cap X[j] = X[\eta[i,j]]$ for all $i, j$
- `E`, `N`: ideals to specify the parameter range in which comprehensive standard system is computed. $V \left( E \right) \setminus V \left( N \right)$ is the resulting range.
- `TR1K`: $M_1$ in the paper.
- `Q`: list of modules (`Q[i]` corresponds to $M_{i+1}$ in the paper for $i \ge 2$)
### Outputs
The format of Lg is as follows:
```Singular
[i]: information of mixed standard basis in the parameter range $V(E_i) \setminus V(N_i)$.
  [i][1]: generators of $E_i$
  [i][2]: generators of $N_i$
  [i][3]: information of local cohomologies and standard basis of $M_1$ in the parameter range $V(E_i)\V(N_i)$.
    [i][3][1]: $E_i$
    [i][3][2]: $N_i$
    [i][3][3]: local cohomology of $M_1$
    [i][3][4]: standard basis of $M_1$ ($S^{(1)}$ in the paper)
  [i][4][j]: $S^{(j+1)}$ in the paper
 ```

The comprehensive mixed-standard system `Lg` can be used in the following functions:
```Singular
reduce_mixed_with_E(list X, vector p, module Nc, list Q, ideal E)
```
### Parameters
- `X`: family of variables (Note that X[i-1] = $X_i$ in the paper)
- `p`: input vector to be reduced
- `Nc`: local cohomology of $M_1$
- `Q`: list of mixed standard basis $S^{(j+1)}$ for $j \ge 1$
- `E`: ideal in the polynomial ring of parameters (`Nc` and `Q` is defined on the parameter range $V(E) \setminus V(N)$.
### Output
- the reduced normal form of `p`
### Example
Suppose `p` is a vector you want to reduce. If you want to do that in the $i$-th parameter range $V(E_i) \setminus V(N_i)$, you can compute that by the command `reduce_mixed_with_E(X,p,Lg[i][3][3],Lg[i][4],Lg[i][3])`.

```Singular
kbase_mixed(list X, list Lgi)
```
### Parameters
- `X`: family of variables (Note that X[i-1] = $X_i$ in the paper)
- `Lgi`: list of mixed standard basis in the $i$-th parameter range (`Lg[i]`)
### Outputs
- set of monomials not $X_i$-involutive multiple of $S^{(i)}$ for all $i \in J$
### Example
The command `kbase_mixed(X,Lg[i])` outputs the set of monomials not $X_i$-involutive multiple of $S^{(i)}$ for all $i \in J$. The set is the basis of the quotient regarded as a $K$-vector space.
