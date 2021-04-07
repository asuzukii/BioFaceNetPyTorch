# BioFaceNetPyTorch
My Attempt at recreating BioFaceNet using PyTorch

## Some Notes on the Research Paper
### 1 Introduction
**tl;dr: lot's of approaches were made to try reconstructing facial lighting interactions**
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
* MoFA- a self-supervised learning approach to train a model-based autoencoder CNN architecture
  * fits a 3D morphable model to single images
  * loss is the error between the constructed image and the input
* InverseFaceNet- estimates 3DMM params inclusing reflectance and illumination
  * again, uses statistical appearannce model
* others include unspupervised autoencoder networks (still not realistic), and supervised synthetic -> real (relies on lambertian)
#### 1.2 Biophysical skin modelling
* Various approaches to model the appearance of human skin
  * Independent Compaonent Analysis (ICA) - restricted to specific light and camera combinations
  * mutispectral/polarized light to derive skin parameter maps from a 2D planar sample
  * Biospec- 24 meaningful parameters to simulate the light interaction w/ skin (computationally expensive)

### 2 Preliminaries
* number of assumptions:
  * images are captured by camera that correctly white balances the scene and uses a fixed gamme
  * scene illumination is spectrally uniform -> (essentially no shadows)
  * skin reflectance follows the dichromatic reflectance model
#### 2.1 Spectral Image Formation
#### 2.2 Wavelength-Discrete Spectral Image Formation
#### 2.3 Color Transformation Pipeline
#### 2.4 Multispectral Dichromatic Model
#### 2.5 Statistical Camera Model
#### 2.6 Physical Lighting Model

### 3 Biophysical spcetral skin model

### 4 Architecture
#### 4.1 Trainable Encoder
#### 4.2 Model-based Decoder
#### 4.3 Losses

### 5 Experiments

### 6 Conclusion
* Restricting reflectance helps break SOTA which was the inverse rendering method
* obvious extension - to combine this work with methods that estimate 3D face geometry
