# plotting_stringdefs
This script is used for automatically plots some variables saved for BASEMENT stringdefs.  

This script need to be used in combination with the python script provided by ETHZ, available at the link https://basement.ethz.ch/download/tools/python-scripts.html, taking care of selecting the script for the correct BASEMENT version, under the voice "Extract Nodestrings (Stringdefs) results from a BASEMENT result container (result.h5)".  Note that the original python script from ETHZ is built to read and write file in the same folder the script is located, the version present here is writing its outputs into "csv_files/" folder for keeping the workspace clearer instead.  

The folders "csv_files" and "images" MUST be already present when running both BMv**NodestringResults.py and src/plot_file.jl.  

## src/
It contains the julia script wich is plotting the data

## csv_files/
It contains the csv file with the results for each Nodestring. This files are automatically created by the BMv**NodestringResults.py python script, which creates one file for each Nodestring and two additional files: results.csv and Discharge.csv. The lattest two are not used in this workflow, that is why they are located (manually) into the csv_files/unused/ folder. The julia script src/plot_file.jl will produce an error in case they are located into the csv_files/ folder together with the other csv files.  

## images/
It contains the plot automatically produced by the src/plot_file.jl script.

Note that all file are automatically replaced when a new file with the same name is saved into the same folder.

## results.h5
This is the input file containing the data to be plotted, it must have this exact name and it must be located in the same folder as BMv**NodestringResults.py script.

# Workflow
Once the working directory is set-up, the easiest way to use the tool is via the terminal, making them executable. The procedure differs depending on the OS installed:

## Linux OS
locate to the working directory using

````
cd working_directory
````

Then make the python script executable and run it

````
chmod +x BMv**NodestringResults.py
./BMv**NodestringResults.py
````

Now the csv_files/ folder is filled by the csv files. Remeber to move away the files "results.csv" and "Discharge.csv". Now to the same for the julia script

````
chmod +x src/plot_file.jl
./src/plot_file.jl
````

## Windows OS

In this case it is necessary to run the script typing

````
python BMv**NodestringResults.py
````

Now the csv_files/ is filled by the csv files, then run

````
julia --project=@. src/plot_file.jl
````


# Final notes
Tt could be necessary to install the h5py package if not already done: 

````
python -m pip install h5py
````

It is necessary to have python and julia installed to use the tool.  

To use the julia script you must have both the project.toml and manifest.toml files into the working directory. The project.toml file is downloaded cloning the repository, the manifest bust be created entering the REPL mode and performing the instantiate command, typing 
````
julia 
julia>  altgr + ]
pkg>    activate .
pkg>    instantiate
````