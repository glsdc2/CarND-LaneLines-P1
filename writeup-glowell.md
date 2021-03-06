# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Reflection

This has been an interesting project for me, as I have not previously used docker, jupyter notebooks, or the various python
libraries in addition to learning the concepts for project.  I was able to complete the project as well as process the
challenge video.  I was suprised at how much time I spent on the color filtering.

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:

* Color Filter to isolate white and yellow features in the image.  I tried both RBG and HSL color spaces. The HSL color space was slightly more effective.
* Conversion to Gray scale
* Gaussian Blur - after experimenting, I settled on a kernel size of 9
* Canny edge detection 
* Region of interesting isolation.
* Hough line fnding

The draw lines function was modified to sort the lines into left and right lane buckets based on slope.
Any lines that were near horizontal were assumed to be noise and were rejected.  After calculating slope, 
y-intercept, and length for the right and left lines, they were weighted by length and averged.  The average 
line for each lane was then on the image starting at the bottom of the image to the 60% point of the frame. 

Images captured at various stages of the pipeline are below.

#### Original Image
<img src="./pipeline-images/Challenge_1-3.6-Original.png" width="1280" alt="Original Image" />

#### OHSL White/Yellow Mask
<img src="./pipeline-images/Challenge_1-3.6-yellow-white-mask.png" width="1280" alt="OHSL White/Yellow Mask" />

#### Color Masked Image
<img src="./pipeline-images/Challenge_1-3.6-color-filtered.png" width="1280" alt="Color Masked Image" />

#### Grayscale Image
<img src="./pipeline-images/Challenge_1-3.6-grayscale.png" width="1280" alt="Grayscale Image" />

#### Gaussian Image
<img src="./pipeline-images/Challenge_1-3.6-gaussian.png" width="1280" alt="Gaussian Image" />

#### Canny Edge Detection
<img src="./pipeline-images/Challenge_1-3.6-canny-edges.png" width="1280" alt="Canny Edge Detection" />

#### Hough Line Finding
<img src="./pipeline-images/Challenge_1-3.6-hough_lines.png" width="1280" alt="Hough Line Finding" />

#### Final Image
<img src="./pipeline-images/Challenge_1-3.6-final.png" width="1280" alt="Final Image" />

### 2. Identify potential shortcomings with your current pipeline

The current pipeline can easily get confused by changes of color, or shadows.  For example the shadow
the tree accross the road in the challenge video causes the yellow line line to break up, and also causes spurious
lines to be detected in the roadway. The pipeline does not take perspective into account. If the camera moves, or if the road is sloped steeply, the pipeline might not find the lanes correctly.

Additionalissues:
*The is a certain amount of jitter from frame to frame.
*The pipeline does not deal well with missing data.
*The linear line fitting does not really account for curved roads.  The sharper the turn, the less well it does.

### 3. Suggest possible improvements to your pipeline

Some of the improvements that coud be made:

*Better isolation of features using color and statistical filtering.  For example, filter on multiple narrow bands instead of just white and yellow and identify and discard outliers.
*Handle missing data, for example when a lane marker disappears for a few frames
*Reduce jitter by smoothing data between frames
*Fit curved lane lines instead of just linear
