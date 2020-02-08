# Android_App_using_pytorch
# This App is build using Pytoch model for classification of Objects
# Now let me break down all the steps which you require to make a App similar to this
## First download Pytorch in your system
### Go to this link https://pytorch.org/get-started/locally/
 - If You are having Anaconda Navigator installed in your system you can run this command on anaconda prompt 
  - conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
  
 ### now we are assuming Pytorch is installed on your system
 ### Now you need to make a model
  - https://ai.googleblog.com/2018/04/mobilenetv2-next-generation-of-on.html
  
    # we are using MobileNet V2 
     ## But Before that you should understand what is MobileNet V1
  ## MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications
  
 #### We present a class of efficient models called MobileNets for mobile and embedded vision applications. MobileNets are based on a streamlined architecture that uses depth-wise separable convolutions to build light weight deep neural networks. We introduce two simple global hyper-parameters that efficiently trade off between latency and accuracy. These hyper-parameters allow the model builder to choose the right sized model for their application based on the constraints of the problem. after performing extensive experiments on resource and accuracy tradeoffs it showed strong performance compared to other popular models on ImageNet classification. We can demonstrate  effectiveness of MobileNets across a wide range of applications and use cases including object detection, finegrain classification, face attributes and large scale geo-localization.
 
 ## For my Project I choosed MobileNet version 2(Its updated version released by google for using convolutional neural network on mobile device)
 ### IF You wants to know more about MobileNet version 2 please visit the link https://machinethink.net/blog/mobilenet-v2/
 
 ### So after so much info on MobileNet version 2 let me tell you how i used it in my Project
 #### Just create a python file in your folder where your making your Project and name it as convert_pytorch_model.py
  ## Copy the below code
import torch
from torchvision.models import mobilenet_v2

model = mobilenet_v2(pretrained=True)

model.eval()
input_tensor = torch.rand(1,3,224,224)

script_model = torch.jit.trace(model,input_tensor)
script_model.save("mobilenet-v2.pt")

### After this run the code using your terminal: Python convert_pytorch_model.py
   - After this you will find a model is creared in your folder with name: mobilenet-v2.pt
   
 ### Great if you are able to follow till here you have created a model and now you can use this model for object classifcation this is a pretrained model
 
 ## Create a Android Project or just zip or clone my project
 ## Advise dont make it in Androidx there will be dependecy issues then you will run down in error so just zip my folder and run it
 ### - In my Project in assets folder i have kept my model mobilenet-v2.pt..
 ### If you are completely running my code no need to make a model because it is allready present in assests folder
 ## Just build the APP and you will be ready to start
 # OUTPUT
 ![app_img](https://user-images.githubusercontent.com/42214175/74078645-ff58ba00-4a52-11ea-918f-008a2715257b.jpg)
 
