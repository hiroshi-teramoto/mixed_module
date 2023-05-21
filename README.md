# mixed_module
Implementation of Algorithms in the paper "Comprehensive Standard System for Generalized Mixed Module and its Application to Singularity Theory" by Hiroshi Teramoto and Katsusuke Nabeshima

To use the libraries, download all the files and place them into a single directory. You will need Singular installed on your machine. We have prepared three examples to demonstrate the libraries:

* example_codimension_transverse_fold.exe
  - See 3.1.1 Example (transverse fold) in the paper
* example_codimension_beak_to_beak.exe
  - See 3.1.2 Example (beak to beak) in the paper
* example_divergent_diagram_j1.exe
  - See 4.1.1 Example: Mather's lemma

Let us explain how to use the library by using the first example. We assume you are familiar with Singular. 
In this example, the definition of the base ring is as follows: 

```Singular
nx = 2;
ny = 2;
ring R = (0,a), (x(1..nx),y(1..ny)), (M(imat),C);
```

In this implementation, all the parameters in the ring, "a" in the example above, are treated as parameters in comprehensive standard system. To use the library, you need to specify the family of variables $(X_i)_{i \in J}$. In this implementation, $X_1$ is the set of all the variables in the base ring. In this example, that is {x(1..nx), y(1..ny)}. You need to specify $X_2$, $X_3$. In the current implementation, X[i-1] = X_i and the list of variables should be of type ideal. For example, 

```Singular
list X = list();
X[1] = ideal(y[1]);
X[2] = ideal(y[2]);
X[3] = ideal(0); // this correspond $X_3 = \emptyset$
```

In the subsequent lines, $\eta$ in the paper (See 2. Setting in the paper) is computed for the given X[1], X[2], and X[3]. For example, if $X[1] \cap X[2] = X[3]$ holds, then eta[1,2] = 3.

ideals $E$ and $N$ specify the entire range of parameters $V(E)\V(N)$ in which comprehensive standard system is computed.

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

The format of Lg is as follows:
```Singular
[i]: information of mixed standard basis in the parameter range $V(E_i)\V(N_i)$.
  [i][1]: generators of $E_i$
  [i][2]: generators of $N_i$
  [i][3]: information of local cohomologies and standard basis of $M_1$ in the parameter range $V(E_i)\V(N_i)$.
    [i][3][1]: $E_i$
    [i][3][2]: $N_i$
    [i][3][3]: local cohomology of $M_1$
    [i][3][4]: standard basis of $M_1$ ($S^{(1)}$ in the paper)
  [i][4][j]: $S^{(j+1)}$ in the paper
 ```



