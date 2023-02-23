# Phonopy Crystal Slurm Job Generator
A python script to generate and submit a batch of slurm job

This should be use as a more sophisicaed bash script as you can make changes to various part of the `.py` and `.template` file to suit your need

## Requirements
- `phonopy`: `2.17.1` from `conda-forge` (This is the only tested system)
- `CRYSTAL23` compiled version run usuing `Pcrystal`
- You need a output file from an optimisation run from `CRYSTAL23` captured using `Pcrystal 2> >(tee {file_name})`
- (Optional) `euphonic`: `1.2.0` from `conda-forge`

## To run
1. Edit the parameter section in the `.py` file.
2. Edit the template files to suit your needs. Refer to [Python3 - Template strings](https://docs.python.org/3/library/string.html#template-strings) on how to set this up.
3. Edit the `*_dict` objects of the corresponding template if you make changes to the template that changes the variables.
4. You can either test run one of them or run it on a remote using `source submit.sh` .
5. Results are collected to `./result` folder.

## Analysis
This part is from personal project but can be adapted for other research as well.
1. Copy the `phonopy_disp.yaml` and the **optimised output** to the result folder
2. `cd` to the result folder and run `phonopy --crystal -f {system_name}*.crys_out --include-all` to get the force (change the `{system_name}` as it is a variable in the script)
3. Run `phonopy --crystal -c {path to optimised structure} --dim="{your_kpoint_dimension}" --dos --mesh="{your_mash size}" --include-all` to get the dos
4. Run `euphonic-dispersion phonopy.yaml` to plot and view the DOS.

