# March 05

<!--**SPR - 16 - E1**
<img src="images/SPR - 16 - E1/origin.jpg" width="200"> <img src="images/SPR - 16 - E1/target.png" width="200"> <img src="images/SPR - 16 - E1/pred.png" width="210"> 

**SPR - 16 - E4**
<img src="images/SPR - 16 - E4/origin.jpg" width="200"> <img src="images/SPR - 16 - E4/target.png" width="200"> <img src="images/SPR - 16 - E4/pred.png" width="200"> -->



## Task 1

Given:
1. a small dataset containing (image, perfect mask, noisy mask)
2. a large dataset containing (image, noisy mask)


|                 Exp Name                |      dice_loss      |
|-----------------------------------------|---------------------|
|  use denoised mask      | 0.45287594199180603 |
| 	use perfect masks only  |  0.4660969376564026 |
|  pseudo labeling          |  0.6596523523330688 |
|  if all lebels are perfect |  0.3286687731742859 |


## Task 2

Given:
1. A large dataset containing (image, noisy mask)


Cropped
<img src="image/999_mask_cropped.png" width="1000"> 

Original
<img src="image/999_org.png" width="1000"> 

Recovered
<img src="image/999_recoverd.png" width="1000"> 


|                 Exp Name                |      dice_loss      |
|-----------------------------------------|---------------------|
|  directly use noisy masks    | 0.3015390932559967 |
| 	use denoised mask			 |  0.3351624608039856 |