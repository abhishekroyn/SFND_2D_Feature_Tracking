# **2D Feature Tracking** 
---

**Camera-Based-2D-Feature-Tracking**

The goals / steps of this project are the following:
* Implement a vector for dataBuffer objects
* Implement detectors HARRIS, FAST, BRISK, ORB, AKAZE, and SIFT
* Remove all keypoints outside of a pre-defined rectangle
* Implement descriptors BRIEF, ORB, FREAK, AKAZE and SIFT
* Implement FLANN matching as well as k-nearest neighbor selection
* Use the K-Nearest-Neighbor matching to implement the descriptor distance ratio test
* Count the number of keypoints on the preceding vehicle for all 10 images
* Count the number of matched keypoints for all 10 images using all possible combinations of detectors and descriptors.
* Log the time it takes for keypoint detection and descriptor extraction, and based on this data, recommend the TOP3 detector / descriptor combinations as the best choice for the purpose of detecting keypoints on vehicles.

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/2549/view) individually and describe how I addressed each point in my implementation.  

---
### Mid-Term Report

#### 1. MP.0 Mid-Term Report

Provided a Writeup (writeup_report.md) that included all the rubric points and how I addressed each one. Submitted writeup as markdown.

### Data Buffer

#### 1. MP.1 Data Buffer Optimization

Implemented a vector for dataBuffer objects whose size did not exceed a limit (e.g. 2 elements). It was achieved by pushing in new elements on one end and removing elements on the other end.

### Keypoints

#### 1. MP.2 Keypoint Detection

Implemented detectors HARRIS, FAST, BRISK, ORB, AKAZE, and SIFT and made them selectable by setting a string accordingly.

#### 2. MP.3 Keypoint Removal

Removed all keypoints outside of a pre-defined rectangle and only used the keypoints within the rectangle for further processing.

### Descriptors

#### 1. MP.4 Keypoint Descriptors

Implemented descriptors BRIEF, ORB, FREAK, AKAZE and SIFT and made them selectable by setting a string accordingly.

#### 2. MP.5 Descriptor Matching

Implemented FLANN matching as well as k-nearest neighbor selection. Both methods were selectable using the respective strings in the main function.

#### 3. MP.6 Descriptor Distance Ratio

Used the K-Nearest-Neighbor matching to implement the descriptor distance ratio test, which looked at the ratio of best vs. second-best match to decide whether to keep an associated pair of keypoints.

### Performance

#### 1. MP.7 Performance Evaluation 1

Counted the number of keypoints on the preceding vehicle for all 10 images and took note of the distribution of their neighborhood size. Did this for all the detectors I had implemented.

[Summary results for - Number of keypoints on the preceding vehicle for all 10 images](#benchmark)

#### 2. MP.8 Performance Evaluation 2

Counted the number of matched keypoints for all 10 images using all possible combinations of detectors and descriptors. In the matching step, the BF approach was used with the descriptor distance ratio set to 0.8.

[Summary results for - Number of matched keypoints on the preceding vehicle for all 10 images](#benchmark)

#### 3. MP.9 Performance Evaluation 3

Logged the time it took for keypoint detection and descriptor extraction. The results were entered into a spreadsheet and based on this data, the TOP3 detector / descriptor combinations were recommended as the best choice for the purpose of detecting keypoints on vehicles.

[Summary results for - Time taken for keypoint detection and descriptor extraction(in ms)](#Performance-Benchmarking)

[Summary results for - Efficiency (total number of matched keypoints/ms)](#benchmark)



## Performance-Benchmarking

#### Number of keypoints on the preceding vehicle for all 10 images

| Detectors | Number of Key-points |
| :-------: | :------------------: |
| SHITOMASI |        1179          |
|  HARRIS   |         248          |
|   FAST    |        1491          |
|   BRISK   |        2763          |
|    ORB    |        1161          |
|   AKAZE   |        1670          |
|   SIFT    |        1387          |



#### Number of matched keypoints on the preceding vehicle for all 10 images

| Detectors\Descriptors | BRISK |  BRIEF  |      ORB      | FREAK | AKAZE | SIFT |
| :-------------------: | :---: | :-----: | :-----------: | :---: | :---: | :--: |
|       SHITOMASI       |  767  |   944   |      908      |  768  |  N/A  |  927 |
|        HARRIS         |  142  |   173   |      162      |  144  |  N/A  |  163 |
|         FAST          |  899  |  1099   |     1071      |  878  |  N/A  | 1046 |
|         BRISK         | 1570  |**1704** |     1516      | 1524  |  N/A  | 1648 |
|          ORB          |  751  |   545   |      763      |  420  |  N/A  |  763 |
|         AKAZE         | 1215  |  1266   |     1182      | 1187  | 1259  | 1270 |
|         SIFT          |  594  |   704   | Out of Memory |  595  |  N/A  |  802 |


* AKAZE descriptors found to be working only with AKAZE keypoints.
* SHITOMASI is configured to have blockSize = 4, whereas, HARRIS is configured to have blockSize = 2
* In the matching step, the BF approach is used with the descriptor distance ratio set to 0.8.
* In the matching step, the BF approach used HAMMING distance as descriptor type for all combinations, but L2 distance as descriptor type for SIFT, because SIFT is not a binary descriptor, and thus results would be N/A if SIFT is used with HAMMING distance as well like others.
[https://stackoverflow.com/questions/37810588/in-opencv-what-does-descriptortype-of-descriptorextractor-class-return]



#### Time taken for keypoint detection and descriptor extraction(in ms)

| Detectors\Descriptors |  BRISK  |    BRIEF    |      ORB      |  FREAK  |  AKAZE  |    SIFT    |
| :-------------------: | :-----: | :---------: | :-----------: | :-----: | :-----: | :--------: |
|       SHITOMASI       | 123.274 |   102.489   |    132.001    | 369.048 |   N/A   |  246.943   |
|        HARRIS         | 129.673 |   151.323   |    152.601    | 399.138 |   N/A   |  250.273   |
|         FAST          |  24.4351|    17.9567  |   **18.7776** | 301.897 |   N/A   |  167.255   |
|         BRISK         | 384.75  |   362.716   |    408.256    | 645.429 |   N/A   |  545.455   |
|          ORB          | 177.769 |   165.538   |    201.364    | 437.482 |   N/A   |  383.248   |
|         AKAZE         | 519.956 |   547.446   |    566.709    | 774.204 | 967.487 |  655.694   |
|         SIFT          | 711.46  |   710.653   | Out of Memory | 915.524 |   N/A   | 1018.62    |



#### Efficiency (matched-keypoints/ms)

| Detectors\Descriptors |  BRISK   |    BRIEF    |      ORB      |  FREAK   |  AKAZE   |   SIFT   |
| :-------------------: | :------: | :---------: | :-----------: | :------: | :------: | :------: |
|       SHITOMASI       | 6.22189  |   9.21075   |    6.87874    | 2.08103  |   N/A    |  3.7539  |
|        HARRIS         | 1.09506  |   1.14325   |    1.06159    | 0.360778 |   N/A    |  0.65128 |
|         FAST          |36.7913   |**61.2029**  |   57.0359     | 2.90827  |   N/A    |  6.25392 |
|         BRISK         | 4.08057  |   4.69789   |    3.71336    | 2.36122  |   N/A    |  3.02133 |
|          ORB          | 4.22458  |   3.2923    |    3.78915    | 0.960039 |   N/A    |  1.99088 |
|         AKAZE         | 2.33673  |   2.31256   |    2.08573    | 1.53319  | 1.30131  |  1.93688 |
|         SIFT          | 0.834902 |   0.990639  | Out of Memory | 0.649901 |   N/A    |  0.78734 |




## TOP3 detector / descriptor combinations

1. FAST + BRIEF
2. FAST + ORB
3. FAST + BRISK

