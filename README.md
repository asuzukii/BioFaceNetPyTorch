# BioFaceNetPyTorch
My Attempt at recreating BioFaceNet using PyTorch

# Table of Contents
- [Introduction](#heading)
- [Procedure Steps I took](#heading)
    - [Getting to Know the Paper](#sub-heading)
    - [Data Preparation](#sub-heading)
- [Conclusion](#heading)

# Introduction
Hello- this is my attempt at recreating the BioFaceNet in PyTorch.

To check out the colab, please click [here](google.com).

To access and download the images, masks, and ground truths, click [here](google.com).

# Procedure Steps I took

## Getting to Know the Paper
First, I read and took some notes on the paper, which could be seen [here](https://github.com/asuzukii/BioFaceNetPyTorch/blob/main/Notes.md), or just click the Notes.md file. Brief summary of what I understood from the research paper should be listed there. 

## Data Preparation
Then, I attempted to run the model given in matlab. However, I couldn't get it to work, namely because the data input was missing. To get an image set ready, I took the celebA imdb cropped face data set (given [here](https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/), under IMDB, faces-only), and took out all the images that had dimensions smaller than 100 pixels, or the height and width differed by more than 100 pixels (just a heuristic). I then reshaped the images to 256x256 for pipelining reasons. Next, I created skin masks (with [this code](https://github.com/WillBrennan/SemanticSegmentation)) for the first 100,000, and after that, took out masked skin images that were too sparse. Specifically, took out images with <50000 non-black pixels.

These masked images were then split into various maps with this paper.

# Conclusion

Some improvements that could be done for this assessment was:
* to have actual concrete ground truths as opposed to pseudo-ground truths shadowing, normals, etc.
    * this could be possibly done by artificial faces using applications like blender?
* celebA imdb dataset is massively biased towards people with paler skin tones. Diversifying the dataset might lead to better results.




