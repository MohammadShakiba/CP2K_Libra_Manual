# Hybrid functionals with CP2K

CP2K can perform hybrid functional calculations with a relatively good speed. You need to install CP2K with `LBINT` and `LIBXC` packages to be able to perform hybrid functional 
calculations. To access a library of exchange-correlation functionals you can use [LIBXC](https://www.tddft.org/programs/libxc/functionals). For different versions of CP2K one
needs a specific version of `LIBXC` or `LIBINT`. So, it is recommended to use the `./install_tool_chain.sh` to compile CP2K or look for the correct version of these libraries and compile them manually and then use them in compilation of CP2K (for more information take a look over [this link](https://xconfigure.readthedocs.io/en/latest/cp2k/)). 
The key to do the hybrid functional calculation speed is the initial guess for the SCF cycle. 
In order to do so, we need to first obtain an initial converged PBE `wfn` file and then use the PBE `wfn` file for the initial SCF guess of the hybrid functional. Here, we have
provided three files: `pbe.inp`, `hse06.inp`, and `b3lyp.inp`. The `pbe.inp` file runs a pure functional calculations and after the complete convergence, produces a `wfn` file. We use this file as an initial 
guess for the `hse06.inp` and `b3lyp.inp` using the `SCF_GUESS RESTART` and `WFN_RESTART_FILE_NAME BA2_PbI4_PBE-RESTART.wfn`.
For HSE06 caclulations we have adopted an input from [here](https://www.cp2k.org/_media/events:2018_summer_school:cp2k-uk-stfc-june-2018-sanliang-ling.pdf). We can use the
PBE potentials for HSE06 but for B3LYP, we need to use the BLYP potentials. The BLYP potentials are available for different atoms in [`GTH_POTENTIALS`](https://github.com/mkrack/cp2k-data/blob/master/potentials/Goedecker/cp2k/GTH_POTENTIALS) file.

In hybrid functional calculations, we need to add this part for HSE06 for the `&XC` section:
```
&XC
  &XC_FUNCTIONAL
  &XWPBE
    SCALE_X -0.25
    SCALE_X0 1.0 
    OMEGA 0.11
  &END
  &PBE
    SCALE_X 0.0
    SCALE_C 1.0
  &END PBE
  &END XC_FUNCTIONAL
  &HF
    &SCREENING
      EPS_SCHWARZ 1.0E-6
      EPS_SCHWARZ_FORCES 1.0E-5
      SCREEN_ON_INITIAL_P FALSE
    &END SCREENING
    &INTERACTION_POTENTIAL
      CUTOFF_RADIUS 10
      POTENTIAL_TYPE SHORTRANGE
      OMEGA 0.11
      !T_C_G_DATA t_c_g.DAT
    &END INTERACTION_POTENTIAL
    ! Defines the maximum amount of memory [MiB] to be consumed by the full HFX module.
    !&MEMORY
    !  MAX_MEMORY  10000
    !  EPS_STORAGE_SCALING 0.1
    !&END MEMORY
    FRACTION 0.3
  &END HF
&END XC
```
For hybrid functionals, CP2K uses Auxiliary Density Matrix Method (ADMM). This needs to be added to the `&DFT` section:
```

```
