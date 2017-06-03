# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./pipeline-images/Challenge_1-3.6-Original.png "Original Image"
[image2]: ./pipeline-images/Challenge_1-3.6-yellow-white-mask.png "HSL White/Yellow Mask"
[image3]: ./pipeline-images/Challenge_1-3.6-color-filtered.png "Color Masked Image"
[image4]: ./pipeline-images/Challenge_1-3.6-grayscale.png "Grayscale Image"
[image5]: ./pipeline-images/Challenge_1-3.6-gaussian.png "Gaussian Kernel Size 9"
[image6]: ./pipeline-images/Challenge_1-3.6-canny-edges.png  "Canny Edge Detection"
[image7]: ./pipeline-images/Challenge_1-3.6-hough_lines.png "Hough Line Finding"
[image8]: ./pipeline-images/Challenge_1-3.6-final.png "Final Image"
---

### Reflection

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


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
