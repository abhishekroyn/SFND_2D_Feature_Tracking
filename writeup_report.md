# **Kidnapped Vehicle** 
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

#### 2. MP.8 Performance Evaluation 2

Counted the number of matched keypoints for all 10 images using all possible combinations of detectors and descriptors. In the matching step, the BF approach was used with the descriptor distance ratio set to 0.8.

#### 3. MP.9 Performance Evaluation 3

Logged the time it took for keypoint detection and descriptor extraction. The results were entered into a spreadsheet and based on this data, the TOP3 detector / descriptor combinations were recommended as the best choice for the purpose of detecting keypoints on vehicles.

