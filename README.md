# photon-hdf5-labview-write
Example of how to write the files needed to use phforge, and how to call phforge in LabVIEW (to learn more about phforge, please visit: https://github.com/Photon-HDF5/phforge).

This repository contains 5 LabVIEW (version 2010) VIs:

- phforge Script.vi
- Write Temp YAML File.vi
- Write Temp Data HDF5 File.vi
- Write Simple smFRET Photon-HDF5 File.vi
- Boolean to String.vi

The first two "Write" VIs need to be executed before running phforge Script.vi, as the files they generate need to be passed as arguments of the Script.

![Write Temp YAML File.vi Front Panel](Figures/Write Temp YAML File.vi Front Panel.png?raw=true "Write Temp YAML File.vi Front Pane;")

<b>Write Temp YAML File.vi</b> (shown above) is a VI used to write the information needed to describe a single-laser, two detectors smFRET experiment. <b>Boolean to String.vi</b> is a utility used by this VI. The VI takes a Metadata cluster as input argument. Note that measurement types other than "smFRET" will require additional parameters and a modified Write Temp YAML File.vi code. Modifications should be easy based on this example and referring to the photon-HDF5 documentation.

![Write Temp Data HDF5 File.png](Figures/Write Temp Data HDF5 File.png?raw=true "Write Temp Data HDF5 File.vi")

<b>Write Temp Data HDF5 File.vi</b> (shown above) is a VI that writes the measurement's data in a temporary HDF5 file used by <b>phforge Script.vi</b>. The VI takes two arrays (Photon Detector IDs and Photon Time Stamps) as input arguments. This VI requires that the HDF5 library and h5labview wrapper be installed.

![phforge Script.png](Figures/phforge Script.png?raw=true "phforge Script.vi")

<b>phforge Script.vi</b> (shown above) takes the two files generated by the above VIs as input arguments, and requires an additional file path to save the final Photon-HDF5 file.
Warning: if the destination file path is already used by another file, this file will be overwritten!

phforge Script returns the following parameters:
- Error out: standard LabVIEW error structure
- Standard Output: message returned by phforge
- Standard Error: error message returned by phforge
- Return Code: 0 if no error, 1 if an error occurred during the execution of phforge.

![Write Simple smFRET Photon-HDF5 File.png](Figures/Write Simple smFRET Photon-HDF5 File.png?raw=true "Write Simple smFRET Photon-HDF5 File.vi")

<b>Write Simple smFRET Photon-HDF5 File.vi</b> (shown above) puts things together and takes 4 input arguments (Metadata cluster, Photon Detector IDs and Photon Time Stamps arrays and Destination File Path).
