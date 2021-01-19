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
It is highly recommended to plot the energy levels vs time as well. In order to do this, you need to add the `&MO_CUBE` section without printing out the cube files by setting 
`WRITE_CUBE .FALSE.`. This will print out the energy levels for each step in the log file. If you have set the `&DIAGONALIZATION` to  `ON`, the energies will be printed 
instantly because it has already computed the energies through diagonalization. If you want to use the `OT` (orbital transformation) method, it will take a bit longer to print 
out the energies. After the energies were printed in the log files, you can plot them using Libra. In order to do so, you will need to run the following command in Python (it is recommended to use the Jupyter notebook):
```
from libra_py.CP2K_methods import read_energies_from_cp2k_log_file

params = { }
params["logfile_name"] = 'OUT-BA2PbI4-MD.log' # The log file name
params["min_band"] = # put the minimum band here
min_band = params["min_band"]
params["max_band"] = # put the maximum band here
max_band = params["max_band"]
params["spin"] = 1 # which spin energies to read
params["init_time"] = 50 # the initial time you want
params["final_time"] = 250 # The final time you need

# Read the energies
energies, tot = read_energies_from_cp2k_log_file(params)

# Now it is needed to 
# Only in case you are using Jupyter Notebook
# %matplotlib notebook
plt.figure()
homo_index = # set the HOMO index here

for band in range(0,max_band-min_band+1):
    energy_levels = []
    for time in range(params["init_time"],params["final_time"]):
        energy_levels.append(energies[time-params["init_time"]][band])
    energy_levels = np.array(energy_levels) * 27.211385 # Converting to eV
    if band == homo_index-min_band: # Plot the HOMO with blue color
        plt.plot(energy_levels, color="blue")
    elif band == homo_index-min_band+1: # Plot the LUMO with red color
        plt.plot(energy_levels, color="red")
    else: # Other states are plotted with black color
        plt.plot(energy_levels, color="black")

plt.xlabel("Time, fs")
plt.ylabel("Energy, eV")
plt.title("(BA)$_2$PbI$_4$ energy levels vs time")
plt.savefig('BA2PbI4_energy_levels_vs_time.png', dpi=300)
plt.close()
```
With this method, you can always check the energies vs time live as the MD goes.

