# Jan 22

<!--**SPR - 16 - E1**
<img src="images/SPR - 16 - E1/origin.jpg" width="200"> <img src="images/SPR - 16 - E1/target.png" width="200"> <img src="images/SPR - 16 - E1/pred.png" width="210"> 

**SPR - 16 - E4**
<img src="images/SPR - 16 - E4/origin.jpg" width="200"> <img src="images/SPR - 16 - E4/target.png" width="200"> <img src="images/SPR - 16 - E4/pred.png" width="200"> -->

# Improvements on the crack detection models

Our previous model [UNet]:

<img src="images/unet_arch.jpeg" width="500"> 

The upsampling process could introduce noise and blurs:

<img src="images/unet_upsample.jpeg" width="400">

To fix the problem, we introduce a gated mechanism:

<img src="images/upsample_attn.jpeg" width="400">

Methods | Dice coeffients 
------- | ---------------
UNet	  | 0.3480
Gated-Unet | 0.3602

Dice coeffients (F1 score on pixel level): for detecting each type of cracks Y, R, BG (i = 1, 2, 3) and detecting all cracks (i = 4),

$$D(p_i,g_i) = \frac{2 p_i \cdot g_i}{||p_i||_2^2 + ||g_i||_2^2}$$

and 

$$\mbox{Dice coefficient}= \frac{1}{4}\sum_{i=1}^4 D(p_i,g_i)$$



# Process the generated crack detection results

##### Raw prediction results:

 <img src="images/crack_pred.png" width="300">  <img src="images/crack_pred_color.png" width="300">
 
##### After process / ground truth:
 
Y (Red), R (Green), BG (Blue)
 <img src="images/connected_com.png" width="300">  <img src="images/ground_truth.jpg" width="280">
 

#### Processing details:

1. Remove weak pixels:
<img src="images/crack_pred.png" width="300">  <img src="images/weak_pixel_rmv.png" width="300">

2. Find all the connected components:
<img src="images/connected.png" width="300">

3. For each component, find a bounding box that has the least area
<img src="images/connected_boxed.png" width="300">

4. For each component, if the length of the diagonal of the bounding box is less than $300$, remove it.
<img src="images/connected_cleaned.png" width="300">

5. For each component, check the corresponding area of the crack type prediction image and get the type of majority on pixel level. Color the componenet with the major type:
<img src="images/crack_pred_color.png" width="300"> <img src="images/connected_com.png" width="300">


#The failure of VAE-based compression:

In general, VAE-based mothods work poorly if the input images do not contain rich patterns:

For instance: 

Input: 
<img src="images/vae_input.png" width="200">

Output (sampled from the distribution):

<img src="images/vae_output.png" width="600">

# A graph theory based method

Assume that the cracks on concretes are forest (i.e, acyclic).

We say a node is of type $i$ if it has $i$ edges. For example:

<img src="images/node_type.jpeg" width="500">

**Notes:** we do not consider the nodes of type $2$, as it is just an edge.

Then we can prove that:

$$ \mbox{Num of cracks} = \frac{1}{2} \left[N_1 + \sum_{i=3}^{\infty} (i-2) N_i \right]$$

where $N_i$ is the number of nodes of type $i$.

Examples:

<img src="images/example_crack_count.jpeg" width="500">


Instead of counting cracks, we can count number of nodes of different types.


