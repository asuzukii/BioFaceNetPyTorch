# BioFaceNetPyTorch
My Attempt at recreating BioFaceNet using PyTorch

## Some Notes on the Research Paper
### Introduction
* Many existing generic models that study facial appearance assume faces are lambertian and ignore specular components
* diffuse albedo is often implemented with a statistical model or with an unconstrained albedo map
  * this might lead to implausible skin colours and not enough non-linearities
* modelling in the biophysical domain has advatanges in that it allows intuitive editing of parameter maps with physical meaning
* BioFaceNet -> DCNN that learns to decompose a single RGB image into various intrinsic components in the spectral domain
  * knowledge encapsulated in a model-based decoder that is used to train a CNN-based encoder
  * ill-posed problem in face-value, so there has to be numerous constraints to make it a solvable problem
  * combine a dichromatic reflectance model and biophysical spectral skin coloring model to make a melanin and hemoglobin maps
  * other factors to consider may be camera sensitivity and spectral illumination
#### 1.1 Deep Face Appearance Decomposition
