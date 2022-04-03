# Dec 16 2020

<!--**SPR - 16 - E1**
<img src="images/SPR - 16 - E1/origin.jpg" width="200"> <img src="images/SPR - 16 - E1/target.png" width="200"> <img src="images/SPR - 16 - E1/pred.png" width="210"> 

**SPR - 16 - E4**
<img src="images/SPR - 16 - E4/origin.jpg" width="200"> <img src="images/SPR - 16 - E4/target.png" width="200"> <img src="images/SPR - 16 - E4/pred.png" width="200"> -->


Here are some better results achieved by using a deeper model, and the finial activation function is replaced by 
$$\mbox{min}(\mbox{max}(x, 0), 1)$$ instead of the sigmoid function (depolarisation constraints seem not work as they are likely to introduce some weird local minimum points).
**SPR - 16 - C2** (Y: in red, R: in green, BG: in blue)
<img src="images/SPR16-C2/O-SPR 16 - C2.jpg" width="210"> <img src="images/SPR16-C2/A-SPR 16 - C2.jpg" width="210"> <img src="images/SPR16-C2/P-SPR 16 - C2.jpg" width="210"> 

**SPR - 16 - D16** (Y: in red, R: in green, BG: in blue)
<img src="images/SPR16-D16/O-SPR 16 - D16.jpg" width="210"> <img src="images/SPR16-D16/A-SPR 16 - D16.jpg" width="210"> <img src="images/SPR16-D16/P-SPR 16 - D16.jpg" width="210">

