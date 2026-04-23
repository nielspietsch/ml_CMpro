# ml_CMpro
Python-based Machine learning pipeline for accurate determination of cardiomyocyte proliferation in engineered tissues
The approach consists of 5 scripts that allow for quantification of proliferating cardiomyocytes based on nuclear Ethynyl-deoxyuridine (EdU) and pericentriolar marker 1 (PCM1) signals. The basis are confocal images of engineered 3D tissues. Stardist nuclear segmentation is run via the GPU to improve speed. This pipeline should be readily adaptable to different cardiac tissues, with the imaging approach depending on nuclear density.

Basic structure:   
  1) Maximum intensity projection generation from Z-Stack images. 2 Images with a Z distance of 1 µm are compressed into one. 
  2) Nuclear segmentation with Stardist deeplearning (GPU).
  3) Annotation of nuclei and feature generation for machine learning (napari) Nuclei are classified by PCM1+/- for cardiomyocyte discrimination and EdU +/- for DNA synthesis detection.
  4) Training of random forest algorithm and cross-validation.
  5) Analysis of images with pre-trained model (CPU).
