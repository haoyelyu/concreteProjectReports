### Data distribution (small patches)

|  Set  |  y   |  r   |  b   |  g  | no crack | Total |
|-------|------|------|------|-----|-------|-------|
| Train | 2091 | 1627 | 1342 | 302 | 21652 | 26291 |
| Valid | 706  | 417  | 591  | 129 |  8937 | 10534 |
|  Test | 830  | 766  | 775  | 177 |  8237 | 10426 |



**Note**: Since I am comparing the performances of a list of the models, I have NOT added the images updated by Agnes on *October 15*. 


### Test results

|  Measures |  y   |  r   |  b   |  g   |
|-----------|------|------|------|------|
| Precision | 0.45 | 0.37 | 0.54 | 0.51 |
|   Recall  | 0.61 | 0.74 | 0.58 | 0.42 |
|  F1 Score | 0.52 | 0.49 | 0.56 | 0.46 |
|  Accuracy | 0.79 | 0.73 | 0.84 | 0.96 |


*Precision* is the ratio of the positive samples among the samples that are classified as positive. A high precision means the algorithm will hardly produce false positive results.

*Recall* is the true positive rate. It answers how many positive samples are labelled positive. A high recall means the algorithm is unlikely to miss a patch containing cracks. (see [Precision and recall](https://en.wikipedia.org/wiki/Precision_and_recall) for detailed explantions)

*F1 Score* is a ``mixture'' of precision and recall, which equals 2/(Recall^(-1) + Precision^(-1)). (see [F1 Score](https://en.wikipedia.org/wiki/F1_score) for detailed explantions)[]()

### Some visualizations

I list some typical cases that the algorithm works and fails. You may notice that the algorithm works well when the crack types are obvious. However, the misclassifaction happens when the crack type alters due to the variations of some unobvious features.  

*You can also find the original images in the folders.*

**J+C25 -37 - D3** (Blue, Green, Red , Yellow in order)

<img src='J+C25 -37 - D3/b.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - D3/g.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - D3/r.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - D3/y.jpg' alt="drawing" width="600"/>

**J+C25-37-B17** (Blue, Green, Red , Yellow in order)

<img src='J+C25 -37 - B17/b.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - B17/g.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - B17/r.jpg' alt="drawing" width="600"/>
<img src='J+C25 -37 - B17/y.jpg' alt="drawing" width="600"/>

**NM+UL45 - 68 - D11** (Blue, Green, Red , Yellow in order)

<img src='NM+UL45 - 68 - D11/b.jpg' alt="drawing" width="600"/>
<img src='NM+UL45 - 68 - D11/g.jpg' alt="drawing" width="600"/>
<img src='NM+UL45 - 68 - D11/r.jpg' alt="drawing" width="600"/>
<img src='NM+UL45 - 68 - D11/y.jpg' alt="drawing" width="600"/>















