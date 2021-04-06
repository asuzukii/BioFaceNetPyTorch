# BioFaceNetPyTorch
My Attempt at recreating BioFaceNet using PyTorch

## Some Notes on the Research Paper
### Introduction
* Many existing generic models that study facial appearance assume faces are lambertian and ignore specular components
* diffuse albedo is often implemented with a statistical model or with an unconstrained albedo map
  * this might lead to implausible skin colours and not enough non-linearities
