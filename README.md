# mixed_module
Implementation of Algorithms in the paper [Comprehensive Standard System for Generalized Mixed Module and its Application to Singularity Theory](https://www.worldscientific.com/doi/abs/10.1142/S0219498824502219?journalCode=jaa) by Hiroshi Teramoto and Katsusuke Nabeshima (In what follows, we denote this paper as the paper.)

To use the libraries, download all the files and place them into a single directory. You will need Singular installed on your machine. We have prepared three examples to demonstrate the libraries:

* [example_codimension_transverse_fold.exe](https://github.com/hiroshi-teramoto/mixed_module/blob/main/example_codimension_transverse_fold.md)
  - See 3.1.1 Example (transverse fold) in the paper
* example_codimension_beak_to_beak.exe
  - See 3.1.2 Example (beak to beak) in the paper
* [example_divergent_diagram_j1.exe](https://github.com/hiroshi-teramoto/mixed_module/blob/main/example_divergent_diagram_j1.md)
  - See 4.1.1 Example: Mather's lemma
* [example_complete_transversal.exe](https://github.com/hiroshi-teramoto/mixed_module/blob/main/example_complete_transversal.md)
  - See 4.1.2 Example: [complete transversal](https://iopscience.iop.org/article/10.1088/0951-7715/10/1/017) (with the degree filtration for class 3 in Table.~1 in the paper)
* [example_Ae_codimension.exe](https://github.com/hiroshi-teramoto/mixed_module/blob/main/example_Ae_codimension.md)
  - Examples to illustrate the computation of the quotients of Ae-tangent space

To run the codes, in the directory, type 

```
Singular example_codimension_transverse_fold.exe
```

We assume you are familiar with Singular. If not please refer to [the singular manual](https://www.singular.uni-kl.de/Manual/4-3-2/index.htm#SEC_Top). If you use windows, one of the ways to install Singular is to install [cygwin](https://www.cygwin.com/) inclusing Singular packages. You can download Singular from [here](https://www.singular.uni-kl.de/index.php/singular-download.html).

## Important notice:
If you use Singular of version(4.3.x), you'll get an error 
```Singular
     ? not enough variables for ordering 1 (dp)
     ? error occurred in or before standard.lib::par2varRing line 520: `
    return (RL);`
     ? leaving standard.lib::par2varRing (520)
     skipping text from `;` error at token `)`
``` 
Older Singular versions (4.0.x) used strings to construct the new ring in par2varRing, while newer versions(4.3.x) used lists
(which had this bug for matrix orderings). It is fixed with commit 3138067d4015d2804d700e33002470444fcd2210
of Singular (see https://github.com/singular/singular) and will be included in the next version of Singular. Tentatively, to avoid the error, use older Singular version (4.0.x) or replace the new standard.lib by the old one. 
