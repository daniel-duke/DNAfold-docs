# Running the Code

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
- "test" contains several test simulations.

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

## Automating the Process

In order to automate this process and store the standard output in a "report.out" file, it may be useful to employ the following bash script. Make sure to define the "path_to_dnafold" variable with the path to the "dnafold" executable.

```
path_to_dnafold = 

set -e
rm -rf report.out
touch report.out
pwd >> report.out
echo "Job started: $(date)" >> report.out
START_EPOCH=$(date +%s)

printf "\n------ prepare clone ------\n" >> report.out
(cd $path_to_dnafold/src; make clean;  make) >> report.out 2>&1

printf "\n------ running ------\n" >> report.out
$path_to_dnafold/dnafold input.txt >> report.out 2>&1

END_EPOCH=$(date +%s)
echo "Job completed: $(date) - $(($END_EPOCH - $START_EPOCH)) seconds elapsed" >> report.out
```