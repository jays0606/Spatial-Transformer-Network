# Spatial-Transformer-Network

## Description

This is based on the thesis Spatial Transformer Networks.

### 1. Introduction 

One limitation of CNN is its inability to be spatially invariant to the position of features. Although Max-pooling does solve this problem to some degree, it typically has small spatial support, thus CNNs still are vulnerable to large transformations of the input data. In order to solve this problem, the author of this thesis introduces a Spatial Transformer module, which provides the network with spatial transformation capabilities. This Spatial Transformer can spatially transform an image by applying mechanisms such as scaling, cropping, rotating, and non-rigid deformations.

As shown in the above figure, the spatial transformer successfully captures only the particular pixels to be used in classification, and transforms in a way that enhances the classification.
### 2. Spatial Transformers

<img src="model.png" height="300"/>

Spatial Transformers are mainly composed of three parts - the localisation network, grid generator, and the sampler. The below figure shows the basic outline of the transformer.



## Results
Grad-CAM output results for four different classes in ImageNet. 
<p align="center">
    <img src="Results/Result0.jpg" height="500px">
    <img src="Results/Result1.jpg" height="500px">
    <img src="Results/Result2.jpg" height="500px">
    <img src="Results/Result3.jpg" height="500px">
</p>

## Discussion

Previously, CNNs were vulnerable to transformations of the input data. With the rise of Visual STNs, this inability of CNNs has been solved by a significant amount. To testify this, I made intentional distortions to the MNIST data, such as rotating, scaling, shifting, and applied the Spatial Transformer in the beginning of the network. This outcome of this model was then compared with the same data into an intact CNN model to verify the ability of spatial transformers. 

Spatial Transformers consists of thee components - the localisation net, grid generator, and the sampler. Luckily, pytorch already provides modules for the grid generator and the sampler. Thus I only had to build the localisation net, which is placed in the very beginning of the network before the original CNN layers. This localisation net computes 6 parameters which successfully transforms the input image into a more desirable form. The input which passes through the grid generator and the sampler turns into the same shape of the original image. Then, training was done through the latter layers as usual. 

The result was applied to some of the distorted images, and proves that the spatial transformers worked successfully. Although some rotations were still not generated smoothly, most of the results show the digits shifted toward the center, and grown in appropriate sizes. 
The accuracy of the STN_module also shows much better result than that of CNN module's. STN shows the highest accuracy of about 98.3%, and CNN about 96.1%, which is 2-3% different. Also, the time taken to train both models does not differ by a lot - within 11-12 seconds per epoch. 

Therefore, spatial transformers are great method to implement in classification tasks where the input images are volatile, as in most cases. It not only boosts the accuracy to a significant amount, but also does not take much longer for the whole training process. 


