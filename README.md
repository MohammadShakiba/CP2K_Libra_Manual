# CP2K manual for electronic structure calculations


In this repository we have provided the inputs for different types of electronic structure calculations. The same files are aslo available in other places as well 
([project_cp2k_libra](https://github.com/AkimovLab/Project_Libra_CP2K), [project_perovskite_crystal_symmetry](https://github.com/AkimovLab/Project_CsPbI3_MB_vs_SP)) for use in
nonadiabatic dynamics. However, here we provide detailed information on how to use CP2K and how the inputs functionality and timings changes with different inputs.


Here we use CP2K v6.1 compiled with Intel parallel studio 2019. For TDDFT with hybrid functionals we will use CP2K v7.1 which is compiled with GCC-8.3 compiler. This is because 
in lower versions of CP2K the TDDFT calculation does not converge and there is a [problem](https://groups.google.com/g/cp2k/c/SEglKzKlVLQ/m/MyTavEqYBQAJ) with converging ADMM calculations.

