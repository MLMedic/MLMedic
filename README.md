# MLMedic
Putting great tools in the hand of clinicians.

This is the project repository for the Brisbane health hack 2019. The goal is to develop an interface for applying mashine learning models to medical imaging data.

Core Feature List:
1) platform-independent GUI in Python / Electron / ?
2) Import of Dicom data
3) Applying Machine Learning models to this dicom data (example: Segmentation and Highlighting of Brain Lesions)
4) Visualising Output

Optional Feature List:
- Model zoo online with upload possibility
- Model conversion from Tensorflow, PyTorch, Caffe, Theano .... to be able to be used in our GUI
- Local Transfer Learning to adjust models to available data at the local site


Getting started:

Data:
- 3T and 7T MPRAGE and MP2RAGE anatomical scans
- dicom and nii format
- link via email

Available Models:
- https://github.com/DLTK/models/tree/master/ukbb_neuronet_brain_segmentation
- https://github.com/josedolz/LiviaNET
- http://64.234.162.248:3000/about

Availabe Tools (need to be trained first):
- https://github.com/kaczmarj/nobrainer
- https://github.com/GUR9000/Deep_MRI_brain_extraction

Example how a current applicaiton of a model looks like:
https://github.com/DLTK/models/tree/master/ukbb_neuronet_brain_segmentation
- install miniconda https://conda.io/miniconda.html or anaconda
- pip install dltk tensorflow
- download Models:
 - http://www.doc.ic.ac.uk/~mrajchl/dltk_models/model_zoo/neuronet/spm_tissue.tar.gz
- clone model repo:
  - https://github.com/DLTK/models
- run model
  - python deploy.py -p path/to/saved/model -c CUDA_DEVICE --config MY_CONFIG


Can we replace this please with a slick GUI?

possible solutions - replacing all of the above steps with:
- Electron
- https://www.npmjs.com/package/dicom
- https://www.npmjs.com/package/imageviewer
- TF.js (https://js.tensorflow.org/)
- potentially python bindings if necessary
- potentially docker :? only if really needed
