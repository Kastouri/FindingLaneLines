# **Finding Lane Lines on the Road** 
The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/image0_step_0_original.jpg "Original Image"
[image2]: ./test_images_output/image0_step_1_gray.jpg "Grey Scale Image"
[image3]: ./test_images_output/image0_step_2_gray_gaussian.jpg "Gaussian Filtered"
[image4]: ./test_images_output/image0_step_3_canny.jpg "Canny Edge Detection"
[image5]: ./test_images_output/image0_step_4_canny_masked.jpg "Region of Interest"
[image6]: ./test_images_output/image0_step_5_0_Hough_segments.jpg "Raw Hough Lines"
[image7]: ./test_images_output/image0_step_5_1_Hough_lines.jpg "Average Hough Lines"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a gaussian filter to smooth the image. The next step was to use canny edge detection to detect all the edges in the image, then I applied a mask to get an image with edges only in the region of intrest. After that I applied Hough to that image and drew the found lines into an empty image. Adding that image to the original image resulted in an image where the segments of the lane lines have been annotated.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by considering the slope of each line segment detected using the Hough method. If the slope is positive, the segment considered as a part of the left lane. If the slope is negative, the segment is considered as a part of the right lane. For each lane line two arrays where defined in order to store the coordinates of every pair of points specifying a segment. Using numpy's polyfit method with all the points stored for each line, the slope and zero-intercept of the image where determined. The last step was defining the beginning and ending height (y-coordinates) of the lane lines. We know that they need to start at the bottom  and stop somewhere in the middle of the image. Knowing the y-coordinates we can use the equation of the fitted line : \\ 
$y = a*x + b$ 
to calculate x: 
$x = (y - b) / a$

The folowing images show the different steps of the pipeline.

#### Original Image
![alt text][image1]
#### Step 1: Grey Scale Image
![alt text][image2]
#### Step 2: Gaussian Filter
![alt text][image3]
#### Step 3: Canny Edges
![alt text][image4]
#### Step 4: Region of Interest
![alt text][image5]
#### Step 5: Hough Lines
##### Raw:
![alt text][image6]
##### Average:
![alt text][image7]


### 2 . Potential shortcomings with my current pipeline


One potential shortcoming would be what would happen when the curvature of the road is higher. Especially when the slope of some segments changes its sign. Those segments are then considered to be a part of the wrong lane.   

Another shortcoming could be the poor edge detection when the lightening conditions are bad.

### 3. Possible improvements to my pipeline

A possible improvement would be to add an other form of checking whether the segments are a part of the left or right lane. A possible way to achieve that would be to also check whether the segments are a part of the left or right half of the image.

Another potential improvement could be to add some filters to improve the edge detection when the lightening conditions are poor.


