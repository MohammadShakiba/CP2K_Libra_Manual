# Covergence analysis 

Here, we perform convergence analysis to obtain an appropriate cutoff value. This is required for other electronic structure calculations. 
The convergence analysis is performed with different cutoff values and the `SCF_GUESS` is set to `ATOMIC` and the first guess of the total energy is used to check the
convergence for different cutoff values and ther is no need to wait until it fully converges although one can check the results for the fully converged total energies as well 
but the results will be almost the same and the difference is negligible. Because of this the `MAX_SCF  1` is used in the `energy.inp`.

As is known the cutoff value unit in CP2K is in Ry which is for the expansion of the electron density in GPW (see [this link](https://groups.google.com/g/cp2k/c/x3fadRBYOXU) for further information). The usual cutoff values range between 100-2000 Ry. But here we use up to 3000 Ry for our 2D perovskite system. 

Higher values with the default settings of CP2K is not possible and therefore we need to increase the NGRIDS in order to spread the cutoff values over the multi-grid levels. The NGRIDS we set here is more than 10 (the default is 4). It is recommended that the NGRIDS be dividable by the number of processors. Also, it is recommended to use a square number of processors, n2, for CP2K. This is different from the QE which one need to use 2n number of processors to get a better functionality. One more thing is to extend the Fast Fourier Transform (FFT) grid in the &GLOBAL section. This will allow you to perform calculations with cutoff values of more than 1500 Ry. This should be along with NGRIDS higher than the default value (here we set it to 25). It is set by adding EXTENDED_FFT_LENGTHS .TRUE. to the input.
