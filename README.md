# Neural_Style_Transfer
You want to change your image style?
Here is the way 
        |
        |
        |
        |
        ٧
        
## What is Neural Style Transfer?

Neural Style Transfer is the technique of blending style from one image into another image keeping its content intact. The only change is the style configurations of the image to give an artistic touch to your image.

The content image describes the layout or the sketch and Style being the painting or the colors. It is an application of Computer Vision related to image processing techniques and Deep Convolutional Neural Networks.
Neural style transfer performed on Mona Lisa painting:
![613ebc713d78bd6d64e763b8_IJBbdBDp67rtR1bfd0GVlcu5kQIIOX5ExT3I8w7f7UGV90_-SwP-lOfF61k6Npq_4SqPiXnQnVgRXwFmNe8c0OctDfb0p_ScrJGWNkgu7S1UKZmk_BsYb-_C11OGXciC8IjqMfO2=s0](https://user-images.githubusercontent.com/66647024/198833278-142eb9d8-0347-4de0-b883-6f0c77b5effd.png)


Neural Style Transfer deals with two sets of images: Content image and Style image.

This technique helps to recreate the content image in the style of the reference image. It uses Neural Networks to apply the artistic style from one image to another.

Neural style transfer opens up endless possibilities in design, content generation, and the development of creative tools.
How does Style Transfer work?

Now, let’s explore how NST works.

The aim of Neural Style Transfer is to give the Deep Learning model the ability to differentiate between the style representations and content image.

NST employs a pre-trained Convolutional Neural Network with added loss functions to transfer style from one image to another and synthesize a newly generated image with the features we want to add.

Style transfer works by activating the neurons in a particular way, such that the output image and the content image should match particularly in the content, whereas the style image and the desired output image should match in texture, and capture the same style characteristics in the activation maps.

These two objectives are combined in a single loss formula, where we can control how much we care about style reconstruction and content reconstruction.

Here are the required inputs to the model for image style transfer:

    A Content Image –an image to which we want to transfer style to
    A Style Image – the style we want to transfer to the content image
    An Input Image (generated) – the final blend of content and style image

## Neural Style Transfer basic structure

Training a style transfer model requires two networks: a pre-trained feature extractor and a transfer network.

NST uses a pre-trained model trained on ImageNet- VGG in TensorFlow.

Images themselves make no sense to the model. These have to be converted into raw pixels and given to the model to transform it into a set of features, which is what Convolutional Neural Networks are responsible for.

Thus, somewhere in between the layers, where the image is fed into the model, and the layer, which gives the output, the model serves as a complex feature extractor. All we need to leverage from the model is its intermediate layers, and then use them to describe the content and style of the input images.

The input image is transformed into representations that have more information about the content of the image, rather than the detailed pixel value.

The features that we get from the higher levels of the model can be considered more related to the content of the image.

To obtain a representation of the style of a reference image, we use the correlation between different filter responses.
<img width="620" alt="613ebf63d399e5f400cce8f8_neural-style-transfer-basic-structure" src="https://user-images.githubusercontent.com/66647024/198833346-81656c24-0bef-4c4b-915b-3e41301523e9.png">

Content loss

It helps to establish similarities between the content image and the generated image.

It is intuitive that higher layers of the model focus more on the features present in the image i.e. overall content of the image.

Content loss is calculated by Euclidean distance between the respective intermediate higher-level feature representation of input image (x) and content image (p) at layer l.
![613ebc7136aa8c7496734312_56ROWESLNXGVVcGPVUcAe14Jsvs57Pgw09cPjgkTcUGRTWgYHaSZNKA0dbuRRprg_ikMM3Bxx972m0ibc0D1ow9cfGWrxXk9jQ-g0Zlj7MA9RE_j5uoxTVn-dVj-5T3s6KtQHubg=s0](https://user-images.githubusercontent.com/66647024/198833369-6d2fca8b-109f-4fa4-8db7-43f5b628edbe.png)


It is natural for a model to produce different feature maps in higher layers being activated in the presence of different objects.

This helps us to deduce that images having the same content should also have similar activations in the higher layers.
Style loss

Style loss is conceptually different from Content loss.

We cannot just compare the intermediate features of the two images and get the style loss.

That's why we introduce a new term called Gram matrices.

Gram matrix is a way to interpret style information in an image as it shows the overall distribution of features in a given layer. It is measured as the amount of correlation present between features maps in a given layer. 
<img width="620" alt="613ebf8ae34aaf0aaa8f01f8_neural-style-transfer-basic-structure-1" src="https://user-images.githubusercontent.com/66647024/198833388-ddf39f9f-1c25-4862-87d9-55f4ef2c6be9.png">

Style loss is calculated by the distance between the gram matrices (or, in other terms, style representation) of the generated image and the style reference image.

The contribution of each layer in the style information is calculated by the below formula: 
![613ebc7136aa8c7488734313_khncG_qMQ3Yu5DR3zxgRLBxHQLsopZl-C-xvlIu32aetMVsnL1lxcR62LSzhXmZnTOH74GZeYPSA4bNXtZ6-_SnS8mtoQzHAJH_jfuMmI28W3CuDkHWlXXROcdvXStqYpvEMJ7eR=s0](https://user-images.githubusercontent.com/66647024/198833407-83812f0e-1f04-479b-8e3d-e340dd0acd9a.png)

Thus, the total style loss across each layer is expressed as:
Total style loss formula
![613ebc723ae59bd6043998c2_-s3RqIoVoQSgqbrHve0_PXFHkUF5UFXbveiAvIXZFUk_qkV5MC7bUgddT7s5hixKx52d_5j7x1uQJ2ixy6k8KfIqeaNaSuvFgYB-khwJnrhgnyJtz5Ju7mom7jF04HP7c7Tf8Zvn=s0](https://user-images.githubusercontent.com/66647024/198833426-769c0350-5fef-4ee3-93b0-26c646150d4e.png)

where the contribution of each layer in the style loss is depicted by some factor wl.
