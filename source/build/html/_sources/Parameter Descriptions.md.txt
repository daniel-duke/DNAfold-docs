# Parameter Descriptions

Parameters are set by adding their values to an input file using the "key = value" form. This file must then be passed as an argument to the to the `dnafold` executable when running the code (see {doc}`Running the Code`).

Parameters surrounded in [ brackets ] are optional. The value after "=" denotes the default value, which are set in `src/parameters.hpp` file. For parameters with a finite number of acceptable values, the possible values are separated by "|" in parentheses beside the parameter.

## Simulation Units

Unless noted otherwise, all numerical values in the code use the corresponding units below.

| Description | Unit |
| ----------- | ----------- |
| Distance | nm |
| Time | ns |
| Force | pN |
| Temperature | K |
| Energy | pN-nm |

## File Input/Output

**inFile**

The `.json` file from caDNAno describing the structure of the origami. See {doc}`caDNAno Examples` for a guide on creating compatible caDNAno structures.

**outFile**

Name of the output files. For example, using `output` will store the results of the simulation in `output.dat` (the trajectory), "output_BINDTIMES.dat" (staple hybridization times), and so forth.

**[stepsPerFrame=1E4]**

Number of simulation steps between printing the bead positions to the ouptput trajectory file.

**[print_to_stdout_every=2E4]**

Number of simulation steps between printing updates (timings, hybridizations, temperature, etc.) to the standard output.

## Computational

**[lsim=1E9]**

Number of simulation steps.

**[dt=0.01]**

Length of the timestep. Should not exceed 0.01, else the simulation could destabilize.

**[stepsPerNeighborListRefresh=1E3]**

Number of simulation steps between refreshing the neighbor lists.

**NTHREADS**

Number of pthreads on which to run the simulation.

## Simulation Conditions

**[CIRCULAR_SCAFFOLD=false]** (true|false)

If true, the code adds a bond between the two ends of the scaffold.

**[FORCED_BINDING=true]** (true|false)

If true, the code applies a long-range force that directs the staples to their respecitve binding positions on the scaffold. Depending on the size of the size of the origami and the simlation box, staples usually each their binding sites within 1E4-1E5 steps.

**[pbc=true]** (true|false)

If true, the code applies a periodic boundary condition.

**[bindStrength=10]**

Hybridization energy of DNA. Note that this energy is in kcal/mol. 

**[temp=300]**

Initial temperature of the simuation.

**[final_temp=300]**

Final temperature of the simulation. Once the temperature reaches this value, it stays constant for the remainder of the simulation.

**[annealing_rate=1E-5]**

Decrease in temperature per simulation step until `final_temp` is reached. For example, if starting at 310K and ending at 300K with the default annealing rate, the temperature will constantly decrease from 310K until it reaches 300K after 1E6 time steps, at which point the temperature will stay constant.

**[BoxSize=200]**

Initial diameter of the cubic simulation box.

**[FinalSizeRatio=0.5]**

Final diameter of the simulation box, as a fraction of the inital diameter.

**[ShrinkRate=1E-5]**

Decrease in box diameter per simulation step until `FinalSizeRatio` is reached. For example, if starting at 200nm and ending at half this diameter with the default shrink rate, the box will constantly shrink from 200nm until it reaches 100nm after 1E7 time steps, at which point the box size will stay constant.
