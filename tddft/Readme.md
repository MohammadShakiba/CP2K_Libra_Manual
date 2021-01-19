# TD-DFT calculations in CP2K

In order to perform TD-DFT calculations in CP2K, you need to the following the `&FORCE_EVAL` section of the input:
```
&PROPERTIES
  &TDDFPT
     NSTATES     20            # number of excited states
     MAX_ITER    200           # maximum number of Davidson iterations
     CONVERGENCE [eV] 1.0e-5   # convergence on maximum energy change between iterations
     &MGRID
        NGRIDS 16
        CUTOFF 500 # separate cutoff for TDDFPT calc
     &END
     ! Only in case you have a tdwfn file from previous calculations
     !RESTART     .TRUE.
     !WFN_RESTART_FILE_NAME RESTART.tdwfn
  &END TDDFPT
&END PROPERTIES
```
The `NGRIDS` and cutoff are chosen the same as in the SCF calculations although you can run another convergence analysis for that too. One can also use the `RESTART` for TD-DFT calculations. To this end, you will need to add the `.tdwfn` file from previous calculations in front of `WFN_RESTART_FILE_NAME`. In CP2K v6.1 one also needs to add
this part to the `&XC` section. For higher versions, this isn't required.
```
&XC_GRID
  XC_DERIV SPLINE2_SMOOTH
&END XC_GRID
```
The results of the TD-DFT calculations for a different number of excited states (`NSTATES`) is shown in the following table.

| NGRIDS  | #Excited states  | #Processors  | Each TD-DFT cycle (s) |Total TD-DFT time (s)   | Maximum excitation energy above band gap (eV)
|---|---|---|---|---|---|
|16   |20   |25   |   |   |   |
|16   |40   |25   |   |   |   |
|16   |60   |25   |   |   |   |

To plot the excitation analysis results or the TD-DFT spectrum please refer to [this link](https://github.com/AkimovLab/Project_Libra_CP2K) or [this link](https://github.com/AkimovLab/Project_CsPbI3_MB_vs_SP). 


