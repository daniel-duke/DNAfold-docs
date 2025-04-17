# Running the Code

## Requirements

In order to run DNAfold, your must have the following installed on your system:

- Git
- GNU Make
- C++ Compiler

Furthermore, we recommend running the code on WSL, MacOS, or a Linux OS (we have tested Ubuntu and CentOS).

## Cloning

The DNAfold code is hosted on GitHub. Before cloning, enter the folder in which you want to store the code.

```
mkdir <MYCLONE>
cd <MYCLONE>
```

Then clone the repository.

```
git clone https://github.com/marcello-deluca/dnafold
```

This creates a folder called `dnafold/` which contains two relevant folders:
- `src/` contains the source simuation code.
- `examples/` contains several example structures with corresponding input files.

To create the executable required to run the code, run the following commands:

```
cd src
make clean
make
```

This creates an executable called `dnafold` in the root directory. The code is now ready to run.

## Running

First, create and enter a folder in which you want to store all the input and output files for your simulation.

```
mkdir <MYSIM>
cd <MYSIM>
```

Add the caDNAno design (see {doc}`page_cadnano_ex`) and the parameters file (see {doc}`page_params`) to the folder. Make sure the parameters file correctly references the name of your caDNAno design.

Finally, run the following command to begin the simulation, making sure to substitute `<PATH_TO_DNAFOLD>` with the path to the `dnafold` executable created earlier.

```
<PATH_TO_DNAFOLD>/dnafold input.txt
```

To run the program in the background and save the standard output to a file, use the following command:

```
nohup <PATH_TO_DNAFOLD>/dnafold input.txt >> report.out 2>&1 &
```

The simulation should then begin!

## Visualization

We recommend using [OVITO](https://ovito.org) to visualize the simulation results.

