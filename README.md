# STRIDE: Protein secondary structure assignment from atomic coordinates

## About STRIDE

STRIDE<sup>[[1]](https://doi.org/10.1002/prot.340230412)</sup> is a program to recognize secondary structural elements in proteins from their atomic coordinates. It performs the same task as DSSP by *Kabsch and Sander (1983)*<sup>[[2]](https://doi.org/10.1002/bip.360221211)</sup> but utilizes both hydrogen bond energy and mainchain dihedral angles rather than hydrogen bonds alone. It relies on database-derived recognition parameters with the crystallographers' secondary structure definitions as a standard-of-truth. Please see *Frishman and Argos (1995)*<sup>[[1]](https://doi.org/10.1002/prot.340230412)</sup> for detailed description of the algorithm.

---

*N.B.* The equations for calculating hydrogen bond energies are printed incorrectly in *Frishman and Argos (1995)*<sup>[[1]](https://doi.org/10.1002/prot.340230412)</sup>. The equations should be:

$$
E_{hb} = E_{r} \cdot E_{t} \cdot E_{p}
$$

> Where $E_{hb}$ is the hydrogen bond energy in **kcal/mol**, $E_{r}$ is the distance-dependent energy contribution, $E_{t}$ is the angle-dependent energy contribution (**no unit**), and $E_{p}$ is the planarity-dependent energy contribution (**no unit**).

$$
E_{r} = \frac{-3 \cdot E_{m} \cdot r_{m}^8}{r^8} - \frac{-4 \cdot E_{m} \cdot r_{m}^6}{r^6}
$$

> Where $E_{m}$ is the optimal hydrogen bond energy (defined as **-2.8 kcal/mol** in [stride.h](src/stride.h)), $r_{m}$ is the optimal hydrogen bond length  (defined as **3.0 Å** in [stride.h](src/stride.h)), and $r$ is the distance between the hydrogen bond donor and acceptor in **Å**.

$$
E_{t} = \begin{cases}
(0.9 + 0.1 \sin{2t_{i}})\cdot \cos{t_0} & 0 \leq t_{i} < 90\degree \\
\frac{0.9}{\cos^6{110\degree}} \cdot (\cos^2{110\degree} - \cos^2{t_i})^3 \cdot \cos{t_0} & 90\degree \leq t_{i} < 110\degree \\
0 & \text{otherwise}
\end{cases}
$$

> Where $t_{i}$ is the angular deviation of the hydrogen atom from the bisector of the lone-pair orbitals within the plane, and $t_{0}$ is the angular deviation from the plane of the lone pair orbitals.

$$
E_{p} = \begin{cases}
\cos^2{p} & 90\degree < p < 270\degree \\
0 & \text{otherwise} \\
\end{cases}
$$

> Where $p$ is the angle between the donor nitrogen, the hydrogen bound to said nitrogen and the acceptor oxygen.

## Changes in fork
- Removed lines from [stride.c](src/stride.c) needed to compile for (very) old Mac computers. The program compiles on modern ARM-based Macs fine now.
- Fixed warning from `passing arguments to a function without a prototype` at compile for [hydrbond.c](src/hydrbond.c).
- Added the missing volume and page numbers to the citation in [report.c](src/report.c).

## References
1. *Frishman, D. & Argos, P. (1995) Knowledge-based secondary structure assignment. Proteins: structure, function and genetics, 23, 566-579. DOI:* [10.1002/prot.340230412](https://doi.org/10.1002/prot.340230412)

2. *Kabsch, W. & Sander, C. (1983) Dictionary of protein secondary structure: pattern recognition of hydrogen-bonded and geometrical features. Biopolymers, 22: 2577-2637. DOI:* [10.1002/bip.360221211](https://doi.org/10.1002/bip.360221211)