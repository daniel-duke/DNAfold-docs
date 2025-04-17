# caDNAno Examples

DNAfold requires caDNAno files (`.json`) to define the structure of the DNA origami to be simulated. For more information on caDNAno, how to install it, and tutorials on how to use it, please see [this webpage](https://cadnano.org/index.html). For additional guidance, there are excellent tutorial videos available online that outline the most critical steps for designing DNA origami structures with caDNAno. 

In order to simulate DNA origami using DNAfold, the caDNAno design must fulfill two requirements: 

- For computational reasons, the scaffold strand must contain a break at some point in the strand. This applies to both linear and circular scaffolds. Whether the scaffold is actually circular or linear can be specified in the input file, as explained in {doc}`page_params`.
- Each crossover and strand break must be separated by a multiple of 8 bp. This is because DNAfold coarsens the DNA into beads, each of which represent exactly 8 bp, no more, no less. If a caDNAno design contains a crossover or strand break at a non-integer multiple of 8 bp away from another crossover or strand break, DNAfold will attempt to place a bead over the crossover or strand break, causing the code to throw an error.

To make adherence to the multiple of 8 rule simple when designing a DNA origami structure, first choose the square grid option in caDNAno. Notice that becuase square lattice origamis naturally have crossover opportunities at multiples of 8 bp, the grid in caDNAno has bold vertical bars every 8 bp. When drawing your scaffold and staple strands on the grid, simply ensure all crossovers and strand breaks fall across one of these bold bars.

Copies of the correct examples discussed below are located in the examples folder within the DNAfold GitHub repository. Corresponding input files are also provided.

## Incorrect 2D Structure

![image](images/donut_bad.png)

This caDNAno structure has several issues that would cause DNAfold to fail.

- As highlighed in the blue circle, a staple strand ends on a non-integer multiple of 8 bp.
- As highlighed by the black circle, a crossover exists on a non-integer multiple of 8 bp.
- As highlighed by the red oval, two staple strand breaks exist on a non-integer multiple of 8 bp.
- There is no break in the scaffold.

## Correct 2D Structure

![image](images/donut_good.png)

This caDNAno structure addresses all of the issues with the first example. Thus, DNAfold can successfully simulate this design.

## Incorrect 3D structure

![image](images/4HB_bad.png)

This caDNAno design raises two red flags:

- The offset of the scaffold in the top two helices does not conform to the multiple of 8 rule, and therefore both the scaffold and several staple strands would cause DNAfold to fail.
- There is no break in the scaffold.

Furthermore, this design exemplifies several design flaws that should be generally avoided when creating DNA origami:

- The light blue staple strand on the far right is less than 16 bp, which is too short.
- The same light blue staple strand contains a binding domain with less than 8 bp, which is too few.
- At the scaffold crossover between the two center helices, beaks in the staple strands line up with the scaffold crossover. Thus, there is a complete break in both the helices at this point.

## Correct 3D structure

![image](images/4HB_good.png)

This caDNAno remediates the issues with the above design. Thus, it is compatible with DNAfold.

## Smiley Face

This is another example of a more complex structure that can be simulated with DNAfold because it follows the rules described above.

![image](images/smile.png)
