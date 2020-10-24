# Oct 22 2020

## The data distribution



|  Set  |  y   |  r   |  b   |  g  |   n   | Total |
|-------|------|------|------|-----|-------|-------|
| Train | 2091 | 1627 | 1342 | 302 | 21652 | 26291 |
| Valid | 706  | 417  | 591  | 129 |  8937 | 10534 |
|  Test | 830  | 766  | 775  | 177 |  8237 | 10426 |

## Original Method
**Description:** We do not add synthetic data when training the model.


**Location:** 

	/home/fieldlv/concreteProject/project/tb_logs/20201022-215115/


**Old Results:**

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.41 | 0.33 | 0.49 | 0.30 |
|   Recall  | 0.72 | 0.86 | 0.61 | 0.44 |
|  F1 Score | 0.52 | 0.48 | 0.55 | 0.35 |
|  Accuracy | 0.75 | 0.67 | 0.82 | 0.93 |



We can gain some improvements by adjusting the gradient descent configuration and the choosing a larger patience in the early stopping method. 

**New Results:**

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.60 | 0.52 | 0.66 | 0.61 |
|   Recall  | 0.50 | 0.40 | 0.38 | 0.38 |
|  F1 Score | 0.54 | 0.45 | 0.48 | 0.47 |
|  Accuracy | 0.84 | 0.83 | 0.86 | 0.97 |



## Single-crack artificial sample
**Description:** An artitifical sample formed by a patch contatining crack combined with a randomly picked crack-free patch as the background


The background brightness follows a Beta distribution $\mathcal{B}(2,10)$.




##### Version 1.1

**Location:** 

	/home/fieldlv/concreteProject/project/tb_logs/20201023-013443

*Portion of artificial data is $0.5$.*


|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.53 | 0.41 | 0.59 | 0.63 |
|   Recall  | 0.58 | 0.66 | 0.48 | 0.41 |
|  F1 Score | 0.55 | 0.50 | 0.53 | 0.49 |
|  Accuracy | 0.82 | 0.77 | 0.85 | 0.97 |


##### Version 1.2

**Location:** 

	/home/fieldlv/concreteProject/project/tb_logs/20201023-051240
	
	
*Portion of artificial decreases exponentially and follows*

~~~ python
0.5 * (0.95**current_epoch)
~~~


|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.58 | 0.45 | 0.59 | 0.61 |
|   Recall  | 0.52 | 0.61 | 0.47 | 0.34 |
|  F1 Score | 0.55 | 0.52 | 0.52 | 0.44 |
|  Accuracy | 0.84 | 0.80 | 0.85 | 0.96 |


#### Version 2

**Location:** 

	/home/fieldlv/concreteProject/project/tb_logs/20201022-222638/

The boundary is moothed by a gaussian filter:

~~~ python
cv2.GaussianBlur(mask, (41, 41), 20)
~~~

##### Version 2.1
*Portion of artificial data is $0.5$.*

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.51 | 0.42 | 0.58 | 0.60 |
|   Recall  | 0.56 | 0.61 | 0.51 | 0.42 |
|  F1 Score | 0.53 | 0.50 | 0.55 | 0.50 |
|  Accuracy | 0.82 | 0.78 | 0.85 | 0.97 |


##### Version 2.2
**Location:** 
	
	/home/fieldlv/concreteProject/project/tb_logs/20201022-222638/

*Portion of artificial decreases exponentially and follows*

~~~ python
0.5 * (0.95**current_epoch)
~~~



|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.46 | 0.45 | 0.61 | 0.65 |
|   Recall  | 0.61 | 0.58 | 0.47 | 0.38 |
|  F1 Score | 0.53 | 0.51 | 0.53 | 0.48 |
|  Accuracy | 0.79 | 0.80 | 0.85 | 0.97 |





## Multi-crack artificial sample

**Description:** Multiple cracks from different samples are merged together with a background from a randomly picked crack-free patch.

Number of samples containing cracks follow distribution:

| # samples | 1 | 2 | 3 |
|-----------|---|---|---|
| Probability | 0.7 | 0.2 | 0.1 |

The boundary is moothed by a gaussian filter:

~~~ python
cv2.GaussianBlur(mask, (41, 41), 20)
~~~

The background brightness follows a Beta distribution $\mathcal{B}(2,10)$.

#### Version 1 
*Portion of artificial data is $0.5$.*

**Location:**

	/home/fieldlv/concreteProject/project/tb_logs/20201022-155807/

**Results:**

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.55 | 0.43 | 0.59 | 0.57 |
|   Recall  | 0.53 | 0.62 | 0.48 | 0.39 |
|  F1 Score | 0.54 | 0.51 | 0.53 | 0.46 |
|  Accuracy | 0.83 | 0.79 | 0.85 | 0.96 |


#### Version 2 
*Portion of artificial decreases exponentially and follows*

~~~ python
0.5 * (0.95**current_epoch)
~~~
**Location:**

	/home/fieldlv/concreteProject/project/tb_logs/20201022-174950/

**Results:**

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.42 | 0.41 | 0.59 | 0.55 |
|   Recall  | 0.68 | 0.57 | 0.51 | 0.46 |
|  F1 Score | 0.52 | 0.48 | 0.55 | 0.50 |
|  Accuracy | 0.76 | 0.78 | 0.85 | 0.96 |



## Summary

**F1 Score**

| Method | Boundary smoothed | Portion of synthetic data |  y   |  r   |  b   |  g   | Avg |
|--------|-------------------|---------------------------|------|------|------|------| ----|
|Original (old)| N.A | N.A | 0.52 | 0.48 | **0.55** | 0.35 | 0.475|
|Original (new)| N.A | N.A | *0.54* | 0.45 | 0.48 | 0.47 | 0.485|
|Single crack patch| No | 0.5 |**0.55** | 0.50 | *0.53* | *0.49* | *0.5175* |
|Single crack patch| No | exponentially decrese |**0.55** | **0.52** | 0.52 | 0.44 | 0.5075 |
|Single crack patch| Yes | 0.5 | 0.53 | 0.50 | **0.55** | **0.50** | **0.52** |
|Single crack patch| Yes | exponentially decrese | 0.53 | *0.51* | *0.53* | 0.48 | 0.5125 |
|Multi crack patch| Yes | 0.5 | *0.54* | *0.51* | *0.53* | 0.46 | 0.51|
|Multi crack patch| Yes | exponentially decrese | 0.52 | 0.48 | **0.55** | **0.50** | 0.5125



**Accuracy**

| Method | Boundary smoothed | Portion of synthetic data |  y   |  r   |  b   |  g   | Avg |
|--------|-------------------|---------------------------|------|------|------|------| ----|
|Original (old)| N.A				  | N.A | 0.75 | 0.67 | 0.82 | 0.93 | 0.7925 |
|Original (new)| N.A				  | N.A | **0.84** | **0.83** | **0.86** | **0.97** | **0.875** |
|Single crack patch| No | 0.5 | 0.82 | 0.77 | *0.85* | **0.97** | 0.8525 |
|Single crack patch| No | exponentially decrese | **0.84** | *0.80* | *0.85* | *0.96* | *0.8625*|
|Single crack patch| Yes | 0.5 | 0.82 | 0.78 | *0.85* | **0.97** | 0.855 |
|Single crack patch| Yes | exponentially decrese | 0.79 | *0.80* | *0.85* | **0.97** | 0.8525 |
|Multi crack patch| Yes | 0.5 | *0.83* | 0.79 | *0.85* | *0.96* | 0.8575 |
|Multi crack patch| Yes | exponentially decrese | 0.76 | 0.78 | *0.85* | *0.96* | 0.8375 |




