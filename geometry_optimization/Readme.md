# Geometry optimization

We first need to obtain an optimized geometry of the structure. When we make a new structure, like heterostructures, we may also need to obtain an optimum cell as well. The cell 
optimization has only one more variable than geometry optimization which is pressure and the optimizer will let the cell changes its size after each cell optimization step. In 
CP2K it is better to perform both cell and geometry optimization together which is done by the keyword `TYPE DIRECT_CELL_OPT` in the  `&CELL_OPT` section of the input. We have the cell optimization inputs in `cell_optimization` folder.

For other structures, like supercells, usually obtained from cif files, the structure may be optimized when geometry optimization is performed but usually this is not the case 
because the energy calculations in each software package may be different. Therefore, you need to perform geometry optimization first. If the changes in the structure is massive
then you need to move to cell optimization as well. You can first use an initial cutoff value for this purpose, which is obtained through the convergence analysis for the initial
cell, and then after obtaining the optimized geometry performing the convergence analysis to obtain a good cutoff and if the initial cutoff is not the same as the one obtained 
form convergence analysis you can redo the geometry optimization by the new cutoff value. This will not take longer than the previous geometry optimization and will finish sooner. 

Note that the CP2K optimizer works based on the forces for each of the geometry and cell optimization. In fact, the movement of the atoms is based on their computed forces. The 
lower the convergence criteria of the SCF cycle (`EPS_DEFAULT`) the more accurate the computed forces. This will lead to a better optimized geometry and will not confuse the 
optimizer. So, it is recommended that for the geometry or cell optimization to use a relatively high cutoff value and a smaller target accuracy of SCF cycle defined by `EPS_SCF`, like `10E-8.0`. After you obtained the optimized 
geometry, for the MD you can use lower `EPS_SCF` values like `10E-6.0`. But the more accurate the forces in MD the more accurate the time-overlaps are and therefore the more accurate the nonadiabatic couplings will be. This is up to the user on which `EPS_DEFAULT` value to choose and is totally dependent on the studied system.

