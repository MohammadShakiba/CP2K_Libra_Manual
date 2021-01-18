# Covergence analysis 

Here, we perform convergence analysis to obtain an appropriate cutoff value. This is required for other electronic structure calculations. 
The convergence analysis is performed with different cutoff values and the `SCF_GUESS` is set to `ATOMIC` and the first guess of the total energy is used to check the
convergence for different cutoff values and ther is no need to wait until it fully converges although one can check the results for the fully converged total energies as well 
but the results will be almost the same and the difference is negligible. Because of this the `MAX_SCF  1` is used in the `energy.inp`.

As is known the cutoff value unit in CP2K is in Ry which is for the expansion of the electron density in GPW (see [this link](https://groups.google.com/g/cp2k/c/x3fadRBYOXU) for further information). The usual cutoff values range between 100-2000 Ry. But here we use up to 3000 Ry for our 2D perovskite system. 

Higher values with the default settings of CP2K is not possible and therefore we need to increase the `NGRIDS` in order to spread the cutoff values over the multi-grid levels. 
The `NGRIDS` we set here is more than 10 (the default is 4). It is recommended to use a square 
number of processors, `n^2`, for CP2K. This is different from the QE which one need to use `2n` number of processors to get a better functionality. One more thing is to extend the 
Fast Fourier Transform (FFT) grid in the `&GLOBAL` section. This will allow you to perform calculations with cutoff values of more than 1500 Ry. This should be along with `NGRIDS` 
higher than the default value (here we set it to 16). It is set by adding `EXTENDED_FFT_LENGTHS .TRUE.` to the input.

Now, in order to run the convergence analysis, one needs to run the bash file `conv_anal.sh`. First, it is needed to make the bash file executable by running the command:
```
chmod +x conv_anal.sh
```
Then one should have loaded the CP2K executable. Note that the extension of the CP2K should be modified in the bash file (we use `.psmp` version). This is done either by `module load` or adding the CP2K executable file to the `PATH` variable. Another way is to create a 
shortcut of the excutable in this folder. Here are three examples:
```
module load cp2k-6.1
```
```
export PATH=/full/path/to/cp2k/executable:$PATH
```
```
ln -s /full/path/to/cp2k/executable 
```

