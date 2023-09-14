Let us explain how to use the library by taking example_divergent_diagram_j1.exe (See 4.1.1 Example: Mather's lemma in the paper) as an example. Specifically, this example involves several parameters and through this example you can learn how to handle that. For background, please refer to 4.1.1 Example: Mather's lemma.

The purpose here is to classify $1$-jet of the divergent diagram 
$$\left( f_1; f_2 \right) \colon \left( \mathbb{R}, 0 \right) \xleftarrow{f_1} \left( \mathbb{R}^2, 0 \right) \xrightarrow{f_2} \left( \mathbb{R}, 0 \right)$$
by using Mather's lemma. The general form of the $1$-jet can be written as:
$$j^1 f_1 \left( x \right) = c_1 x_1 + c_2 x_2 + \mathcal{M}_2^2 \mathcal{E}_2^2$$
$$j^1 f_2 \left( x \right) = c_3 x_1 + c_4 x_2 + \mathcal{M}_2^2 \mathcal{E}_2^2$$

Through that expression, we can see that the $1$-jet space is coordinated by $c_1, c_2, c_3, c_4 \in \mathbb{R}$.

The group acting on the divergent diagram $\mathcal{G}$ induces the Lie group $j^1 \mathcal{G}$ acting on the $1$-jet space and we want to decompose the $1$-jet space into distinct orbits of the induced action. Since the dimension of every orbit is constant under the setting, we first decompose the $1$-jet space into several components so that 
$$\dim_{\mathbb{R}} T_{j^1 f} \left( j^1 \mathcal{G} \cdot j^1 f \right)$$
is constant for each component. 

By the isomorphism as an $\mathbb{R}$-vector spaces in the paper (4.1), we obtain 

$$j^1 \mathcal{M}_2 \mathcal{E} \_2 \^2 / T \_{j^1 f} \left( j^1 \mathcal{G} \cdot j^1 f \right) \cong \langle x_1, x_2 \rangle \left( \mathbb{R} \left[ X_1 \right] \_{\langle X_1 \rangle} \right)^2 / M$$

(Note that the right hand side of (4.1) should have $\langle x_1, x_2 \rangle$.), where 
- $I = \lbrace 1, 2, 3, 4 \rbrace$,
- $X_1 = \lbrace x_1, x_2, y_1, y_2 \rbrace$,
- $X_2 = \lbrace y_1 \rbrace$,
- $X_3 = \lbrace y_2 \rbrace$,
- $X_4 = \emptyset$,
and
- $M = \sum_{j \in I} M_j$
  - Expressions of $M_j \ \left( j \in I \right)$ are lengthy and please refer to the paper for details.

By using the isomorphism, the computation of the codimension of the tangent space $T \_{j^1 f} \left( j^1 \mathcal{G} \cdot j^1 f \right)$ is reduced to that of the mixed-module $M$. The latter can be computed by using the comprehensive standard system for mixed-module. 

First, let us define a ring having parameters `c(1)`, `c(2)`, `c(3)`, and `c(4)` which correspond to $c_1, c_2, c_3$, and $c_4$, respectively, with variables $\lbrace x_1, x_2, y_1, y_2 \rbrace$.
```Singular
ring R = (0,c(1..4)), (x(1..nx),y(1..ny)), (M(imat),C);
```

Then, let us define a family of variables `X` as:
```Singular
list X = list();
for(i=1;i<=ny;i++){
	X[i] = ideal(y(i));
	X[i] = std(X[i]);
}
X[ny+1] = ideal(0);
```

In the subsequent lines, we (for detail, see the code.)
- compute $\eta$,
- define the ideals $E$ and $N$,
- define $f$,
- define `TR1K` (= $M_1$),
- define `Q` (list of $M_2, M_3, M_4$, where `Q[i]` = $M_{i+1}$)

After the above parameters are set, we are readly to compute the comprehensive standard system for mixed-module:
```Singular
list Lg = cssm(X,eta,E,N,TR1K,Q);
```
For the detail of `cssm`, please refer to [example_codimension_transverse_fold.exe](https://github.com/hiroshi-teramoto/mixed_module/blob/main/example_codimension_transverse_fold.md) or [the code](https://github.com/hiroshi-teramoto/mixed_module/blob/main/cssm_multi_v2.lib).

`cssm` decomposes the parameter space $\mathbb{C}^4$ into several locally closed sets $V \left( E_i \right) \setminus V \left( N_i \right)$ and the set of the standard system for mixed-module that is valid on each locally closed set. The codimension of the quotient space on each locally closed set is constant and it can be computed by 
```Singular
```









