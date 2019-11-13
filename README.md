# OBSOLETE
This repository has become obsolete as the latest version of the toolkit is now available in [this](https://github.com/pulp-platform/fann-on-mcu) repository. 


# -----------------------------------------------------------------

Copyright (c) 2018 ETH Zurich, Ferdinand von Hagen, Michele Magno, Lukas Cavigelli

# FANN-on-ARM: Optimized FANN Inference for ARM Cortex M-series

This repository contains optimized code to perform 
inference of FANN-trained neural network on the 
ARM Cortex M-series platform.  

Given a data file and pre-trained network in FANN's format, 
all necessary files to run and test the network on the 
microcontroller are generated. 

### Prerequisites
You should have data and a pre-trained network in the FANN format. 
To run the script, python2 needs to be installed. 
This code has been tested with the MSP432 platform.

### Usage
First, you need to export your data in the FANN default format
and train a neural network with FANN. How to do this is 
explained [here](http://leenissen.dk/fann/html/files2/gettingstarted-txt.html).
You should end up with two files, a `.data` file and a `.net` file. 
An example can be found in the `sample-data` folder.

Then, you can use the `generate.py` script to generate the 
files to run on the microcontroller, e.g. 
> python2 generate.py sample-data/myNetwork

Now all the *.h and *.c files can be copied to you project. 
They include all the data and code to run the network. 
To call it from your code, just include `fann.h` and call 
`fann_type *fann_run(fann_type * input);`, where
`fann_type` is `float` or `int` depending on whether you started
with a fixed-point model or not. Don't forget to include the files 
in your build scripts/makefile/project.

### File Description
Constant files:

- `generate.py`: the script generating the network and data-specific code files based an FANN-format data
- `fann_structs.h` and `fann.c`: contain the implementation of the NN building blocks.
- `fann.h`: the header file to be included in your code providing the `fann_type *fann_run(fann_type * input);` function declaration. 
- `sample-data/{myNetwork.net, myNetwork.data}`: sample data and network pre-trained with FANN. 

Generated files:

- `fann_net.h`: contains the trained parameters and the network structure. 
- `fann_conf.h`: contains some more meta information on the network; #layers, fixed-point parameters (if applicable), ...
- `test_data.h`: contains the test input data and expected result

### License and Attribution
Please refer to the LICENSE file for the licensing of our code. 
We rely on the interfaces, specifications, and some code of the FANN project. 



