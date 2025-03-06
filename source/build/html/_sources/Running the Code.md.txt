# Running the Code

## Requirements

In order to run DNAfold, your must have the following installed on your system:

- Git
- GNU Make
- C++ compiler

Furthermore, we recommend running the code in WSL, MacOS, or a Linux OS (we have tested on Ubuntu and CentOS).

## Cloning

The dnafold code is hosted on GitHub. Before cloning, enter the folder in which you want to store the code.

```
mkdir myclone
cd myclone
```

Then clone the repository.

```
git clone https://github.com/marcello-deluca/dnafold
```

This creates a folder called "dnafold" which contains two relevant folders:
- "src" contains the source simuation code.
- "examples" contains several example structures with corresponding input files.

To create the executable required to run the code, execute the following commands:

```
cd src
make clean
make
```

This creates an executable called "dnafold" in the root directory. The code is now ready to run.

## Running

First, create and enter a folder in which you want to store all the input and output files for your simulation.

```
mkdir mysim
cd mysim
```

Add the caDNAno design (see {doc}`caDNAno Examples`) and the parameters file (see {doc}`Parameter Descriptions`) to the folder. Make sure the parameters file correctly references the name of your caDNAno design.

Finally, run the following command to begin the simulation, making sure to substitute "path_to_dnafold" with the path to the "dnafold" executable created earlier.

```
path_to_dnafold/dnafold input.txt
```

The simulation should then begin!

## Visualization

We recommend using OVITO ([link](https://ovito.org)) to visualize the simulation results.

## Automating the Process

If you plan to run several simulations, it may be useful to employ the following "run_simulation.sh" bash script. Make sure to define the "path_to_dnafold" variable with the path to the "dnafold" executable.

```
path_to_dnafold=

set -e
echo "Directory: $(pwd)"
echo "Job started: $(date)"
START_EPOCH=$(date +%s)

printf "\n------ prepare clone ------\n"
(cd $path_to_dnafold/src; make clean;  make)

printf "\n------ running ------\n"
$path_to_dnafold/dnafold input.txt

END_EPOCH=$(date +%s)
echo "Job completed: $(date) - $(($END_EPOCH - $START_EPOCH)) seconds elapsed"
```

If order to run the simulation in the background and store the output in a file with the name of your choice, use the following command:

```
nohup ./run_simulation.sh > report.out 2>&1 &
```