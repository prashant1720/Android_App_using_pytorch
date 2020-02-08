# Android_App_using_pytorch
# This App is build using Pytoch model for classification of Objects
# Now let me break down all the steps which you require to make a App similar to this
##First download Pytorch in your system
### Go to this link https://pytorch.org/get-started/locally/
 - If You are having Anconda Navigator installed in your system you can run this command on anaconda prompt 
  - conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
  
 ### now we are assuming Pytorch is installed on your system
 ### Now you need to make a model
  - https://ai.googleblog.com/2018/04/mobilenetv2-next-generation-of-on.html
  
  ######The big idea behind MobileNet V1 is that convolutional layers, which are essential to computer vision tasks but are quite expensive to compute, can be replaced by so-called depthwise separable convolutions.

The job of the convolution layer is split into two subtasks: first there is a depthwise convolution layer that filters the input, followed by a 1×1 (or pointwise) convolution layer that combines these filtered values to create new features:
A depthwise separable convolution block

Together, the depthwise and pointwise convolutions form a “depthwise separable” convolution block. It does approximately the same thing as traditional convolution but is much faster.

The full architecture of MobileNet V1 consists of a regular 3×3 convolution as the very first layer, followed by 13 times the above building block.

There are no pooling layers in between these depthwise separable blocks. Instead, some of the depthwise layers have a stride of 2 to reduce the spatial dimensions of the data. When that happens, the corresponding pointwise layer also doubles the number of output channels. If the input image is 224×224×3 then the output of the network is a 7×7×1024 feature map.

As is common in modern architectures, the convolution layers are followed by batch normalization. The activation function used by MobileNet is ReLU6. This is like the well-known ReLU but it prevents activations from becoming too big:

y = min(max(0, x), 6)

The authors of the MobileNet paper found that ReLU6 is more robust than regular ReLU when using low-precision computation. (I think “low-precision” here refers to fixed-point arithmetic and not so much the 16-bit floats used with Metal on iOS.)

It also makes the shape of the function look more like a sigmoid:
The ReLU6 activation function

In a classifier based on MobileNet, there is typically a global average pooling layer at the very end, followed by a fully-connected classification layer or an equivalent 1×1 convolution, and a softmax.

There is actually more than one MobileNet. It was designed to be a family of neural network architectures. There are several hyperparameters that let you play with different architecture trade-offs.

The most important of these hyperparameters is the depth multiplier, confusingly also known as the “width multiplier”. This changes how many channels are in each layer. Using a depth multiplier of 0.5 will halve the number of channels used in each layer, which cuts down the number of computations by a factor of 4 and the number of learnable parameters by a factor 3. It is therefore much faster than the full model but also less accurate.

Thanks to the innovation of depthwise separable convolutions, MobileNet has to do about 9 times less work than comparable neural nets with the same accuracy. This type of layer works so well that I’ve been able to get models with 200+ layers to run in real-time, even on an iPhone 6s.

All right, so that’s all old news. For a more in-depth look, check out my previous blog post or the original paper.
