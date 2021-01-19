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
  &END TDDFPT
&END PROPERTIES
```
The `NGRIDS` and cutoff are chosen the same as in the SCF calculations although you can run another convergence analysis for that too. 
