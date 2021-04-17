# Some Notes on the Research Paper
## 1 Introduction
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
### 1.1 Deep Face Appearance Decomposition
* MoFA- a self-supervised learning approach to train a model-based autoencoder CNN architecture
  * fits a 3D morphable model to single images
  * loss is the error between the constructed image and the input
* InverseFaceNet- estimates 3DMM params inclusing reflectance and illumination
  * again, uses statistical appearannce model
* others include unspupervised autoencoder networks (still not realistic), and supervised synthetic -> real (relies on lambertian)
### 1.2 Biophysical skin modelling
* Various approaches to model the appearance of human skin
  * Independent Compaonent Analysis (ICA) - restricted to specific light and camera combinations
  * mutispectral/polarized light to derive skin parameter maps from a 2D planar sample
  * Biospec- 24 meaningful parameters to simulate the light interaction w/ skin (computationally expensive)

## 2 Preliminaries
**tl;dr: lot's of background theory- mainly how light, camera, reflection from object interacts into the photo**
* number of assumptions:
  * images are captured by camera that correctly white balances the scene and uses a fixed gamme
  * scene illumination is spectrally uniform -> (essentially no shadows)
  * skin reflectance follows the dichromatic reflectance model
### 2.1 Spectral Image Formation
* The RGB image is formde by the integration over the wavelength of the product of the illumination, reflectance, and camera spectral sensitivity.
### 2.2 Wavelength-Discrete Spectral Image Formation
* We approximate the above equation by discretizing wavelength at D locations
### 2.3 Color Transformation Pipeline
* various transformations to make the photo actually pleasing to the eye:
  * first transformation divides each channel by the color of light source as recorded by sensor
  * second transformation converts from the camera-specific color space to the standard XYZ space
  * finally, gamma correction is applied
### 2.4 Multispectral Dichromatic Model
* scene radiance can be divided into diffuse and specular components
  * the diffuse part modifies the SPD of light thru absorption, 
  * the specular part is at the surface, and so no absorption
### 2.5 Statistical Camera Model
* Since the camera spectral sensitivities are low dimensional, using PCA, one can capture 97% of the variance of the data set 
### 2.6 Physical Lighting Model
* using a linear combination of representation of tungsten, fluorescent, and natural light, the lighting was estimated

## 3 Biophysical spcetral skin model
* 2 free biophysical params
* A 2-layer skin model was applied 
  * the epidermis (outer skin) is modelled so that everything but blue light is mainly forward scattered
  * the dermis (inner skin) is supposed to contain the blood vessels, and it absorbs blue/green wavelengths
  
## 4 Architecture
* at the most abstract, the trainable encoder estimates a semantically meaningful parameters and a fixed decoder that implements these back into an image.
* 4 image quantities: hemoglobin, melanin, difuse, specular maps
### 4.1 Trainable Encoder
* encoder itself has both a encoder/decoder
* invert the gamma first for heuristic improvement
* seperate decoder for each parameter
* positivity constraints -> use of softmax/sigmoid to bound it to a range
### 4.2 Model-based Decoder
* all components implemented in a differentiable manner, so that the gradients can be backpropagated all the way back to the encoder
* various lookup tables to streamline the decoding process
### 4.3 Losses
* 4 losses to keep track of
  * RMSE of produced image vs. actual
  * L2 camera sensitivity param regularization loss
  * L1 specular reflections regularization loss
  * L2 diffuse shading loss
  
## 5 Experiments
* use the CelebA Dataset
* some reconstruction, editing applications

## 6 Conclusion
* Restricting reflectance helps break SOTA which was the inverse rendering method
* obvious extension - to combine this work with methods that estimate 3D face geometry
