# MLMedic
Putting great tools in the hand of clinicians.
https://github.com/MLMedic/MLMedic

This is the project repository for the Brisbane health hack 2019. The goal is to develop an interface for applying mashine learning models to medical imaging data.

# Feature List:
1) platform-independent GUI in Python / Electron / ?
2) Import of Dicom data
3) Applying Machine Learning models to this dicom data (example: Segmentation and Highlighting of Brain Lesions)
4) Visualising Output

# Optional Feature List:
- Model zoo online with upload possibility
- Model conversion from Tensorflow, PyTorch, Caffe, Theano .... to be able to be used in our GUI
- Local Transfer Learning to adjust models to available data at the local site


# Getting started:
## Data:
- 3T and 7T MPRAGE and MP2RAGE anatomical scans
- dicom and nii format
- link via email

## Available Models:
- https://github.com/DLTK/models/tree/master/ukbb_neuronet_brain_segmentation
- https://github.com/josedolz/LiviaNET
- https://github.com/Entodi/MeshNet 
- http://64.234.162.248:3000/about (Same as above)

## Availabe Tools (need to be trained first):
- https://github.com/kaczmarj/nobrainer
- https://github.com/GUR9000/Deep_MRI_brain_extraction

## Example how a current applicaiton of a model looks like:
https://github.com/DLTK/models/tree/master/ukbb_neuronet_brain_segmentation

- install miniconda https://conda.io/miniconda.html or anaconda
 - wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
  - bash Miniconda3-latest-Linux-x86_64.sh
- conda install tensorflow
- pip install dltk
- clone model repo:
  - git clone https://github.com/DLTK/models
- download Models:
 - wget http://www.doc.ic.ac.uk/~mrajchl/dltk_models/model_zoo/neuronet/spm_tissue.tar.gz
 - tar -xzf spm_tissue.tar.gz (into /models/ukbb_neuronet_brain_segmentation/
 - copy files from spm_tissue/0/1513180449 up one level to spm_tissue/0
 - adjust paths in /models/ukbb_neuronet_brain_segmentation/config_spm_tissue.json so they point to the path /models/ukbb_neuronet_brain_segmentation/spm_tissue or whatever  is relevant.
 - create and add this to /models/ukbb_neuronet_brain_segmentation/files.csv in two lines: id,t1,fsl_fast,fsl_first,spm_tissue,malp_em,malp_em_tissue
5404127,3T.nii.gz,T1_brain_seg.nii.gz,all_fast_firstseg.nii.gz,T1_brain_seg_spm.nii.gz,T1_MALPEM.nii.gz,T1_MALPEM_tissues.nii.gz  
  - download 3T file from link provided on owncloud and name it 3T.nii.gz, place it in /models/ukbb_neuronet_brain_segmentation/
- run the model!
  - python deploy.py --csv files.csv --config config_spm_tissue.json
## Another example:
 From https://github.com/Entodi/MeshNet
  - First you need Torch! 
 Steps taken from https://dwijaybane.wordpress.com/2017/07/22/installing-torch-7-deep-learning-on-ubuntu-16-04/
 - sudo apt-get install --no-install-recommends git software-properties-common
 - export TORCH_ROOT=~/torch
 - git clone https://github.com/torch/distro.git $TORCH_ROOT --recursive
 - cd $TORCH_ROOT
 - ./install-deps
 - ./install.sh -b
 - Now download the models for MeshNet AKA BrainChop
 - git clone https://github.com/Entodi/MeshNet.git
 - Download the 3T data from owncloud link
 - Install python and dependencies if you haven't:
 - pip install nipy
 - Conform T1 to 1mm voxel size in coronal slice direction with side length 256.
 - (Freesurfer required) mri_convert *brainDir*/t1.nii *brainDir*/t1_c.nii -c
 - Convert nifti to numpy format
 - python nifti2npy.py *brainDir*/t1_c.nii --npy_file *brainDir*/T1.npy
 - Create segmentation using predict.lua providing path to directory with brain npy file brainDir
 - th predict.lua -modelFile ./saved_models/model_Mon_Jul_10_16:43:55_2017/model_219.t7 -brainPath *brainDir*
 - Convert numpy segmentation file to nifti format by providing base nifti file
 - python npy2nifti.py segmentation.npy t1_c.nii
 
## Can we replace this with a nice GUI that ideally doesnt need a python installation?
- Electron
- https://www.npmjs.com/package/dicom
- https://www.npmjs.com/package/imageviewer
- TF.js (https://js.tensorflow.org/)
