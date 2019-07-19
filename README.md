# neonatal-5TT
This is the code to create the 5TT file and the parcellation needed to create the connectome using Anatomically-constrained tractography (ACT) (Smith et al. 2012) in the neonatal brain.
Different approaches can be found in the literature (Batalle et al. 2017, Lennartsson et al. 2018, Blesa et al. 2019). The main purpose of this work was to create a fully automated method, freely available and respecting as much as possible the underlying anatomy of the neonatal brain.

# Requirements
This method relies on several different resources/tools:
- FSL (https://fsl.fmrib.ox.ac.uk/fsl/fslwiki)
- MRtrix (http://www.mrtrix.org/)
- ANTs (http://stnava.github.io/ANTs/)
- matlab (https://www.mathworks.com/products/matlab.html)
- M-CRIB atlas (https://github.com/DevelopmentalImagingMCRI/M-CRIB_atlas)
- Developing Human Connectome Project (dHCP) pipeline (https://github.com/BioMedIA/dhcp-structural-pipeline)

Note that matlab is not freely available, this small part of the code could be easily written in Octave or Python.

# Instructions
First of all you need to install all the software mentioned in the previous section and download the 10 manually labelled subjects of the M-CRIB atlas.

The next step is to run the dHCP pipeline to the M-CRIB manually labelles subjects. This is done to obtain the images bias field corrected in the same way as the subject willbe later on and also the brain mask defined with the same criteria. 

Put all the T2w of the M-CRIB processed with dHCP pipeline in a folder, with the brainmask_drawnem.nii.gz and the segmentations. Then run: 

labelconvert ID_seg.nii.gz M-CRIB_labels_FreeSurfer_format.txt M-CRIB_labels_FreeSurfer_format_default.txt ID_seg_mrtrix.nii.gz 
For each subject

Then you only need to download everything to the same folder and is ready to run.

Example:

- Create a folder with the raw T2w data
- mkdir Structural
- dhcp-pipeline.sh ID session AGE -T2 T2w.nii.gz -additional -d $PWD/Structural -t 20

For the example of the dHCP in the abstract the process was a follows:

- Create a folder and download everything from this repository and the raw T2w (defaced) for the subject CC00069XX12

# Tricks
The script generate-Parcellation.sh takes a lot of time, this is because the antsJointLabelFusion.sh by default runs in serial, but you can add the option -c to control for parallel computation. Same applies to the dHCP pipeline call, you can modify the number of cores with the -t option.

# How to cite
If you are using this code, please cite:
XXXXXXXX

Also be aware that all the tools employed here have their own citations, please cite them appropriately.


