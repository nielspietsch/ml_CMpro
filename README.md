# ml_CMpro
Python-based Machine learning pipeline for accurate determination of cardiomyocyte proliferation in engineered tissues
The approach consists of 5 scripts that allow for quantification of proliferating cardiomyocytes based on nuclear Ethynyl-deoxyuridine (EdU) and pericentriolar marker 1 (PCM1) signals. The basis are confocal images of engineered 3D tissues. Stardist nuclear segmentation is run via the GPU to improve speed. This pipeline should be readily adaptable to different cardiac tissues, with the imaging approach depending on nuclear density.
VS code is used as python editor. 

Basic structure:   
  1) Maximum intensity projection generation from Z-Stack images. 2 Images with a Z distance of 1 µm are compressed into one. 
  2) Nuclear segmentation with Stardist deeplearning (GPU).
  3) Annotation of nuclei and feature generation for machine learning (napari) Nuclei are classified by PCM1+/- for cardiomyocyte discrimination and EdU +/- for DNA synthesis detection.
  4) Training of random forest algorithm and cross-validation.
  5) Analysis of images with pre-trained model (CPU).

Script 1: Z-stack generation.
Z-stacks are imported with the CziFile plugin (Zeiss specific image format). MIPs are created using numpy and tifffile libraries.

Script 2: Nuclear segmentation (GPU).
The pre-trained deep learning model Stardist is employed to accurately annotate nuclei in tissue slices. 

Script 3: Feature annotation recognition.
Napari is used to annotate nuclei across genotypes/conditions to account for staining variability. Nuclei are classified as cardiomyocyte nuclei by PCM1+ signal and EdU+ nuclei. EdU+ nuclei are relatively sparse, which has to be accounted for by annotating enough images (50 EdU+/PCM1+ nuclei minimum). The annotated features are then recognized with this script.

Script 4: Training of machine learning algorithm for classification of nuclei into cardiomyocyte or non-myocyte nuclei and EdU +/-.
Takes the annotation (features.csv) from script 3 and trains a random forest classifier. 5-fold cross validation is used.

Script 5: Batch analysis of images for proliferating cardiomyocyte nuclei.
Batch processing of all images with the model trained in script 5.
