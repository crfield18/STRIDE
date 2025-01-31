# STRIDE: Protein secondary structure assignment from atomic coordinates

## About STRIDE

STRIDE [1] is a program to recognize secondary structural elements in proteins from their atomic coordinates. It performs the same task as DSSP by Kabsch and Sander [2] but utilizes both hydrogen bond energy and mainchain dihedral angles rather than hydrogen bonds alone. It relies on database-derived recognition parameters with the crystallographers' secondary structure definitions as a standard-of-truth. Please see Frishman and Argos [1] for detailed description of the algorithm.

1. *Frishman, D. & Argos, P. (1995) Knowledge-based secondary structure assignment. Proteins: structure, function and genetics, 23, 566-579.*

2. *Kabsch, W. & Sander, C. (1983) Dictionary of protein secondary structure: pattern recognition of hydrogen-bonded and geometrical features. Biopolymers, 22: 2577-2637.*

## Changes in fork
- Removed lines from [stride.c](src/stride.c) needed to compile for (very) old Mac computers. The program compiles on modern M-series Macs fine now.
- Fixed warning from `passing arguments to a function without a prototype` at compile for [hydrbond.c](src/hydrbond.c).
- Added the missing volume and page numbers to the citation in [report.c](src/report.c).