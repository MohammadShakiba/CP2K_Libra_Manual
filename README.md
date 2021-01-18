# CP2K manual for electronic structure calculations


In this repository, we have provided the inputs for different types of electronic structure calculations. The same files are also available in other places as well 
([project_cp2k_libra](https://github.com/AkimovLab/Project_Libra_CP2K), [project_perovskite_crystal_symmetry](https://github.com/AkimovLab/Project_CsPbI3_MB_vs_SP)) for use in
nonadiabatic dynamics. However, here we provide detailed information on how to use CP2K and how the inputs functionality and timings change with different inputs.


Here we use CP2K v6.1 compiled with Intel parallel studio 2019. For TDDFT with hybrid functionals, we will use CP2K v7.1 which is compiled with GCC-8.3 compiler. This is because in lower versions of CP2K the TDDFT calculation does not converge and there is a [problem](https://groups.google.com/g/cp2k/c/SEglKzKlVLQ/m/MyTavEqYBQAJ) with converging ADMM
calculations. It is also worth noting that the computed results are done using Intel(R) Xeon(R) E5-2699 v4 @ 2.20GHz CPUs. 

We will use a 2D perovskite of (BA)2PbI4 and which its [cif](http://crystallography.net/cod/2102937.cif) file is available from the [crystallography website](http://crystallography.net/). We will use the unit 
cell with 156 atoms and a 2x2x2 supercell with 1248 atoms and check the performance of CP2K calculations functionality. 

The procedure adopted here is as follows:

* Obtaining the `xyz` coordinates from a `cif` file
* Convergence analysis for a structure
* Geometry and cell optimization 
* TDDFT calculations
* Molecular dynamics
* Hybrid functionals
* The effect of CP2K parameters on the cube file 
    * Cube file sizes
    * Molecular orbitals overlap 
    * Molecular orbitals time-overlap
        * The effect of time step 
