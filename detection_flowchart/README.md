# Crack detection flowchart

Given a raw input image, our machine learning algorithm makes two predictions

1. detect cracks 
2. for each pixel, give the probabilities that the pixel belongs to three crack type (Y, R, BG), respectively. 

For instance, feeding this image into the model:

 <img src="images/SPR 16 - B12.jpg" width="300"> 

we can get the two raw predictions (left: crack location, right: crack types):

 <img src="images/crack_pred.png" width="300">  <img src="images/crack_pred_color.png" width="300">
 
In the right image, we visualized the prediction results, where Y (Red), R (Green), BG (Blue).

Then we use some computer vision techniques to improve the prediction quality.

#### Processing details:

1. Remove weak pixels (left: input, right: week pixels removed):
<img src="images/crack_pred.png" width="300">  <img src="images/weak_pixel_rmv.png" width="300">
The process will remove weak white noise. 

2. Find all the connected components:
<img src="images/connected.png" width="300">

3. For each component, find a bounding box (in red) that has the least area
<img src="images/connected_boxed.png" width="300">

4. For each component, if the length of the diagonal of the bounding box is less than $300$, remove it. (Step 3 and 4 together remove small cracks)
<img src="images/connected_cleaned.png" width="300">

5. For each component, check the corresponding area of the crack type prediction image and get the type of majority on pixel level. Color the componenet with the major type:
<img src="images/crack_pred_color.png" width="300"> <img src="images/connected_com.png" width="300">

 
##### After process / ground truth:
 
Y (Red), R (Green), BG (Blue)
 <img src="images/connected_com.png" width="300">  <img src="images/ground_truth.jpg" width="280">
