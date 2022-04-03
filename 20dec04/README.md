# Nov 20 2020

## Review

Last time, we discussed a Unet-like design:

<img src="images/unet.jpeg" width="800"> 

- I reported that the model fails to learn the right features if I directly train the model to implement both crack detection and type classification. 

As a result, we started from implementing the crack detection first:

<img src="images/unet_crack_only.jpeg" width="800">

#### Result
<img src="images/crack_org.jpg" width="300"> <img src="images/old_result/crack_pred.jpeg" width="300">


## Upgraded model

<img src="images/unet_crack_aux.png" width="800">
Regularizers: for each pixel, add the following terms to the loss function
$$\lambda_1 (Y + R + GB - Crack)^2$$
$$\lambda_2 (|Y| + |R| + |GB|)$$

#####Results
<img src="images/crack_org.jpg" width="300"> <img src="images/unet_mul/pred.jpg" width="300"> 
<img src="images/crack_org.jpg" width="300"> <img src="images/unet_mul/pred_crack.jpg" width="300">
<img src="images/crack_org.jpg" width="300"> <img src="images/unet_mul/pred_proccessed.jpg" width="300">

#### 'XOR'-problem
The model has a strong intention to classify yellow cracks as green. The logic seems like:

| cracks type | Feature G | Feature Y |
| ----------- | --------- | --------- |
| Y | Yes | Yes |
| G | Yes | No |

So the feature G detector is not diabled when feature Y detector is activated. 

#### Extra Results
Instead of applying regularizers, for each pixel, there are four possible types:
 
 - Y, R, GB, crack-free

I added a softmax layer to produce one-hot labels.

##### Results

<img src="images/crack_org.jpg" width="300"> <img src="images/unet_softmax/pred.jpg" width="300"> 
<img src="images/crack_org.jpg" width="300"> <img src="images/unet_softmax/pred_crack.jpg" width="300">



