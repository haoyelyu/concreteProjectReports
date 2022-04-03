# Jan 22

<!--**SPR - 16 - E1**
<img src="images/SPR - 16 - E1/origin.jpg" width="200"> <img src="images/SPR - 16 - E1/target.png" width="200"> <img src="images/SPR - 16 - E1/pred.png" width="210"> 

**SPR - 16 - E4**
<img src="images/SPR - 16 - E4/origin.jpg" width="200"> <img src="images/SPR - 16 - E4/target.png" width="200"> <img src="images/SPR - 16 - E4/pred.png" width="200"> -->

# Count nodes instead of cracks

Assuming that the cracks on concretes are forest (i.e, acyclic), then

$$ \mbox{Num of cracks} = \frac{1}{2} \left[N_1 + \sum_{i=3}^{\infty} (i-2) N_i \right]$$

where $N_i$ is the number of nodes of type $i$.


Instead of counting cracks, we can count number of nodes of different types.

# Synthetic data generation

We created samples containing Nodes of type $1$, $3$, $4$ and $5$. Some noise is added to make the cracks similar to the natural one:

<img src="images/input_samples.png" width="800">

Besides, we also created the correpsonding density maps for each type of nodes.

For instance, for nodes of  type 1:
<img src="images/type1_node1.png" width="150"> <img src="images/type1_node2.png" width="150"> <img src="images/type1_node3.png" width="150"> <img src="images/type1_node4.png" width="150">

For nodes of type 1, 3, 4, 5:
<img src="images/type1_node1.png" width="150"> <img src="images/type3_node1.png" width="150"> <img src="images/type4_node1.png" width="150">  <img src="images/type5_node1.png" width="150"> 


# A UNet-based node detection model

<img src="images/unet_arch.jpeg" width="700">

This network works well to detect nodes and seperate type 2 nodes from the others. 

#### Detection of nodes of type 1

<img src="images/unet_results/node1_1.png" width="150"> <img src="images/unet_results/node1_2.png" width="150"> <img src="images/unet_results/node1_3.png" width="150"> <img src="images/unet_results/node1_4.png" width="150">

#### Detection of nodes of type 3, 4, 5
1. Density map of type 3, 4, 5 for the same input image

<img src="images/unet_results/node2_1_w.png" width="150"> <img src="images/unet_results/node3_1_w.png" width="150"> <img src="images/unet_results/node4_1.png" width="150">


# Classification of nodes of type 3, 4, 5
After detecting the nodes of types other than 1, we extract the image patch surrounding it:

<img src="images/input_samples_bd_masked.png" width="800">

Then we feed it into another network: 

<img src="images/vgg_classifier_arch.jpeg" width="800">

We used $10,000$ for training, $1,000$ for validation and $1,000$ for testing.

The model achieved $0.988$ accuracy.

**Note:** Extra analysis implies that the UNet-based network fails because the node type is not based on the pixel-wise features, which implies a need to develop a model that is a mixture of pixel-wise and regular classification models. 