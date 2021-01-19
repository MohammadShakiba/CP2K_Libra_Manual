# Cutoff analysis for cube files overlaps

The last part in this manual is about the effect of CP2K parameters on the overlap matrices. CP2K uses the converged wavefunction to produce the cube files for each molecular 
orbital. It will append the numerical values of the wavefunction computed at each grid point in a cube file. The grid points is dependent on the cutoff value. 
The larger the cutoff the higher the number of grid points are. In fact, the cutoff value "defines" the number of grid points. 

Now, if we have a huge cutoff value, like 1000 Ry, and we want to append all the values of the plane waves in all the grid points, then each cube file size will rise up to
hundreds of MBs or even some GBs. This is also dependent on the system cell size as well and the larger the cell size the larger the cube files will be. There are different 
ways to avoid high computational cost for outputting the cube files by CP2K. Specially, if we are going to use a large number of states, for example 30 states in valence 
band and 20 in conduction band. Each cube file is 600 MB, for example, and therefore all the cube files will be up to 30 GB for only one time step and for two consecutive 
time step this would be 60 GB that in some cases may cause overflow of the disk.

One way to overcome this problem and avoiding the overflow of the disk space is to use the keyword `STRIDE` in the input file. The `STRIDE` keyword will use and evaluate 
the wave functions only at some grid points. To clarify what it means, it is better to give an example. The `STRIDE 1 1 1` will use all the grid points in all the three X, Y, 
and Z axis. The `STRIDE 2 2 2` will use half of the grid points on each of the X, Y, and Z axis and `STRIDE 3 3 3` will use one third of the grid points on each of the axes and 
so on. The choice of the `STRIDE` needs to be studied for each system separately. For example if one chooses a huge cutoff value, say 1500 Ry, the cube files will be massively 
large and the computational times will increase. It is worth noting that Libra uses multiprocessing for reading the cube files and it is fast enough and may not take a very long 
time but note that one should also be very careful about the memory of the computer. If it overflows the code will crash. Therefore, the use of `STRIDE` is necessary. Now, if we 
want to check which `STRIDE` we should use we can start with a few number of Kohn-Sham states, say only 5 in valence band and 5 in conduction band, and start from `STRIDE 1 1 1`, 
and save the overlap matrices obtained from this parameter. Then we can move to `STRIDE 2 2 2` and compare the computed overlaps with the ones obtained from the finer mesh points 
(`STRIDE 1 1 1`). This loop is continued until we get to a large difference between the overlap values that can change the matrix elements significantly. The latter is the optimum 
`STRIDE` to use. Note that if one uses `STRIDE n` it is equivalent to `STRIDE n n n` in which `n` is an integer value.



