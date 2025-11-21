# BigDataViewer HDF5 to OpenVDB converter

This simple script uses Blender's built-in `pyopenvdb` library to parse HDF5 XMLs and convert them to a list of sparse OpenVDB files. OpenVDB stores data in a hierarchical tree-like structure, making it highly efficient for sparse data. For rendering, you probably don't need all the background voxels anyway, so we can discard them in exchange for smaller storage size. The script will calculate a global median value for each channel, and use that value as a threshold. For threshold parameter details, see below.

<img width="500" alt="3D render of cells" src="https://github.com/user-attachments/assets/edbe8606-b066-4b24-94b0-01e6d6fe2035" />


## How to run

The quickest way is to run the script from inside Blender. The only missing dependency is `h5py`, which the script will attempt to automatically install in Blender's Python environment. If this fails (check the system console), you might need to launch Blender as administrator. Once the package is installed, you can run the Blend file as normal user.

### Run as Jupyter notebook

If you want to take a closer look at your data before exporting, you can use the script from inside a Jupyter notebook instead. To set up a compatible Jupyter kernel, use [the Notebook connector addon](https://github.com/BradyAJohnston/NotebookConnector), which you may have to run as Admin. A slightly cluttered test notebook that I used to develop the script is also included in this repo.

## How to use

There are currently a few parameters available in the script:
- **xml_path**: the path to your HDF5 XML file (not the H5 file!)
- **sparse_threshold**:  This parameter is a factor by which the median value will be multiplied. A factor of 2 will get rid of most of the unwanted background fairly aggressively, while still keeping the important data. You can lower this threshold to 1 or 0.5 if needed.
- **selected_timepoints**: an optional list that, if populated, will export only the timepoints specified. Otherwise, all timepoints in the HDF5 file will be converted.
- **append_to_scene**: automatically import the VDB sequence into the current Blend file after conversion has finished.
