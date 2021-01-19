# Molecular dynamics in CP2K

The input of the molecular dynamics (MD) is almost the same as geometry optimization. For this case, you will have to change the `RUN_TYPE` to `MD` in the `&GLOBAL` section. 
Also, you need to change the `&MOTION` section as well. The obtained trajectory is stored in the `*-pos-1.xyz` file. The same as in geometry optimization, CP2K will print out 
a `.restart` file if the calculations are interrupted. The production of such files can be controlled in the [`&PRINT`](https://manual.cp2k.org/trunk/CP2K_INPUT/MOTION/PRINT.html) section of `&MOTION` section.

The timings, temperature, potential, kinetic, and total energy are printed out in a `.ener` file. To see if the system is equilibrated, you can use Python by plotting the 
temperature vs time or total energy vs time. This is done using the following command:
```
import numpy as np
import matplotlib.pyplot as plt
# Load the .ener file
ener_data = np.loadtxt('project_name-1.ener', skiprows=1)
# Plot the temperature (4th column) vs time (second column)
plt.figure()
plt.plot(ener_data[:,1], ener_data[:,3])
plt.xlabel('Time, fs')
plt.ylabel('Temperature, K')
plt.title('Temperature vs time')
plt.savefig('temp_vs_time.png',dpi=300)
plt.close()
```
It is highly recommended to plot the 
