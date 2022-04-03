# Nov 06 2020


## Crack detection

### The data distribution

|  Set  |  y   |  r   |  b   |  g  |   n   | Total |
|-------|------|------|------|-----|-------|-------|
| Train | 2091 | 1627 | 1342 | 302 | 21652 | 26291 |
| Valid | 706  | 417  | 591  | 129 |  1843 | 3686 |
|  Test | 830  | 766  | 775  | 177 |  2548 | 5096 |

|  Set  |  y   |  r   |  bg  |   n   | Total |
|-------|------|------|------|-------|-------| 
| Train | 2091 | 1627 | 1644 | 21652 | 26291 |
| Valid | 706  | 417  | 720  |  1843 | 3686  |
|  Test | 830  | 766  | 952  |  2548 | 5096  |


### Test results (Four cracks Y, R, B, G)


**F1 Score**

| Method | Boundary smoothed | synthetic data %  |  y   |  r   |  b   |  g   | Avg |
|--------|-------------------|---------------------------|------|------|------|------| ----|
|Single crack patch| No | 0.5 |**0.55** | 0.50 | *0.53* | *0.49* | *0.5175* |
|Single crack patch| No | exp dec |**0.55** | **0.52** | 0.52 | 0.44 | 0.5075 |
|Single crack patch| Yes | 0.5 | 0.53 | 0.50 | **0.55** | **0.50** | **0.52** |
|Single crack patch| Yes | exp dec | 0.53 | *0.51* | *0.53* | 0.48 | 0.5125 |
|Multi crack patch| Yes | 0.5 | *0.54* | *0.51* | *0.53* | 0.46 | 0.51|
|Multi crack patch| Yes | exp dec | 0.52 | 0.48 | **0.55** | **0.50** | 0.5125

**Accuracy**

| Method | Boundary smoothed | synthetic data % |  y   |  r   |  b   |  g   | Avg |
|--------|-------------------|---------------------------|------|------|------|------| ----|
|Single crack patch| No | 0.5 | 0.82 | 0.77 | *0.85* | **0.97** | 0.8525 |
|Single crack patch| No | exp dec | **0.84** | **0.80** | *0.85* | *0.96* | *0.8625*|
|Single crack patch| Yes | 0.5 | 0.82 | 0.78 | *0.85* | **0.97** | 0.855 |
|Single crack patch| Yes | exp dec | 0.79 | **0.80** | *0.85* | **0.97** | 0.8525 |
|Multi crack patch| Yes | 0.5 | *0.83* | 0.79 | *0.85* | *0.96* | 0.8575 |
|Multi crack patch| Yes | exp dec | 0.76 | 0.78 | *0.85* | *0.96* | 0.8375 |

### Test results (Three cracks Y, R, BG)

| Method | Boundary smoothed |synthetic data %  |  y   |  r   |  bg   | Avg |
|--------|-------------------|---------------------------|------|------|-------| ----|
|Single crack patch| Yes | 0.5 		| **0.53** | **0.52** | 0.56 | 0.54 |
|Single crack patch| Yes | exp dec 	| 0.51 | 0.48 | **0.62** | 0.54 |
|Single crack patch| Yes | exp inc 	| 0.52 | 0.47 | 0.59 | 0.53 |
|Multi crack patch | Yes | 0.5	 	| 0.52 | 0.50 | 0.60 | 0.54 |
|Multi crack patch (rej. int) | Yes | 0.5  | **0.52** | 0.51 | **0.62** | **0.55** |

| Method | Boundary smoothed | synthetic data %  |  y   |  r   |  bg   | Avg |
|--------|-------------------|---------------------------|------|------|-------| ----|
|Single crack patch| Yes | 0.5		| **0.83** | **0.83** | **0.84** | **0.83** |
|Single crack patch| Yes | exp dec	| 0.73 | 0.73 | 0.83 | 0.76 |
|Single crack patch| Yes | exp inc	| 0.75 | 0.72 | **0.84** | 0.77 |
|Multi crack patch | Yes | 0.5	 	| 0.79 | 0.75 | 0.83 | 0.79 |
|Multi crack patch (rej. int) | Yes | 0.5  | 0.80 | 0.74 | **0.84** | 0.79 |

## Crack counting

### The generation the binary matrix represention

*Note*: we used four-colour implementation for now.


#### Method 1
Partition the images ( of size 1792 x 1792) into 16 x 16 small patches (of size 112 x 112). Then each patch is fed into the crack detector to generate a 4 x 16 x 16 binary matrix.

* [Pros] Process image fast (1s/ image)
* [Cons] The generated binary matrix makes some anti-intuitive predictions.
* [Reason] The detector performs poorly when the crack is on the boundary of the window.

#### Method 2

Generate a heatmap using a silding window. Then we partition the images into 10 x 10 patches. For each patch, if the confidence (i.e. the brightness) is greater than a threshold, set the bit corresponding to that patch 1; otherwise, 0.

* [Pros] More accurate matrix represention.
* [Cons] Very slow processing speed (1.5 min/image)



### Results

#### Model
Four saperate regression model consisting two fully connected layers. 


##### Method 1
Training | Validation | Test | Total|
-------- | -----------| ---- | -----|
381 | 127 | 127 | 635 |


<img src="images/testMethod1.jpg" width="500">

##### Method 2

Training | Validation | Test | Total|
-------- | -----------| ---- | -----|
226 | 75 | 77 | 378 |

<img src="images/testMethod2.jpg" width="500">



## Other counting methods

### Heatmap based counting
Typical application: [Crowd Counting](https://pdf.sciencedirectassets.com/280203/1-s2.0-S1877050920X00093/1-s2.0-S187705092031053X/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjELP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJGMEQCIDcztiL8700KUGgPvkN3t0Hq6gxIUX9OSdK8VvKKPPTZAiA2yGhEWLMAIGcURm%2BraJ87ocHpPaScJD1hXdps7GDQZCq0AwgcEAMaDDA1OTAwMzU0Njg2NSIM8vfX5X3cnnw8iVovKpED00UcxpmNVxmNLKBNyNpH4lXkhnMz%2BL98I5%2FcrmERsCewItUrahHmIoxEfufcXGgltMFXjZcZe9a60p6%2Fs7%2BpZs%2FR9YYxCx7ArHGlhEZQQisJ%2FKyZ%2FDGn%2BXJ7P7g5KV0pZJpQ3gW1r%2B1%2FWDzklJwff7Sw%2BxDQsoVp8zHzP9ZaBrCYib2%2BCoGIbM9%2B9EPe%2BtcVtedkhyMCQ%2BW8eHtZAM66qYC1nLAn7UJl5zgHg5oY5BWqNszeIu14xzy%2BU1mwrRQU%2BKnDC5Xl299PEU5ue3J5lJ5litba2DMyjV4dbhhgphnXA759D3v0ayE2yfharrmpKAkCCoLHUCSBKPfejp5TAUvdCeW5su9SSmVqr8mYzSt%2Bkj3dPk5ji7t2py8vLfTLc0M8lfVdpEjOwAHBtfE%2BZ%2FS6kcoGqGJDGCX4JMZic5bAIJUFRN82DTyo6pn05TZiIqGqEB6rhYB7zhJCjH%2B1vlo0YFyYXrAo7BJVmnl%2Fsto0lepU5c1htPIo3V2pYVaKveLAI86nMFFfqcfTbFgS9RQwpLCW%2FQU67AENcv0n8eCFIgOejCp6kVkvEblcUJn1I%2B1hRN6bd3tliVBW5ChwwQjnEFI96AhfA6USltbXhlNtjDklj4l4%2BrdD5HLISI5ZdSnkXO%2FIejl6mQWQD9bH9k7vZoPFm1lBS0w033%2BrEgBMAVZ%2B2lhO1zSAeQPLG%2B2yNkMZNLJQtqaASTJcm%2Bt1%2Fm0fMNxLKKFlC%2BK55RecLuwMF8YY4qvmFWUIK0QIQEhyYlf6IW%2FKWoxMGyNLHUHR%2FmpAbBqFUX%2B%2BKvxUXRmjyJ1agU9s%2FWbwcgbqfkISDEYnmqV4d5RcuEPzgNGWUDa4AiqYlBMevA%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20201106T185803Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY5OVNWKUR%2F20201106%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=1b20f51a9b175c85e0fb17b2f58b7b9088c2f6165ea17ea19e72fc08fc87a6ef&hash=abc040ad30c7d3ab4cd4b7bb2e188f1fee8df3e1d392b1c8b124921ecb86819c&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S187705092031053X&tid=spdf-44605f02-2329-44be-9bd9-469b1fb1365e&sid=3aebc1944c29124a9f8919052b62780ce754gxrqa&type=client)


### Object Detection System
Typical algorithm: YOLO

* used to count numer of cells in an image.

The algorithm predicts: 
1. a bounding box 
2. the classification of the object in the box.


<img src="images/YOLO.png" width="500">







