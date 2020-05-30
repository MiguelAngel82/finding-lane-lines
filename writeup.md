# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/grayscale.png "Grayscale"
[image2]: ./test_images_output/gaussian_blur.PNG "Gaussian Blur"
[image3]: ./test_images_output/canny_edge.PNG "Canny edge"
[image4]: ./test_images_output/region_of_interest.PNG "Region of interest"
[image5]: ./test_images_output/region_of_interest_grayscale.PNG "Region of interest over gray image"
[image6]: ./test_images_output/hough_transform.PNG "Hough transform"
[image7]: ./test_images_output/weighted_image.PNG "Weighted image"
[image8]: ./test_images_output/processed_images.png "Weighted image"

---

### Reflection

### 1. Pipeline. 

My pipeline consisted of 6 steps. First, all needed parameters are defined. So that is easy to find a parameter, change it and do a quick check of how the change is affecting. An important parameter is `vertices` that builds a trapezium to focus only on the road. As the first step, the image is converted to grayscale, then a Gaussian blur is applied, followed by Canny edge detection. Once the edge has been detected the region of interest is obtained and finally Hough transform is done in order to find lane lines. The last step is to draw the detected lines onto the original image.

A quick summarize of the steps throughout images:

#### Grayscale image

![alt text][image1]

#### Gaussian blur

![alt text][image2]

#### Canny edge detection

![alt text][image3]

#### Region of interest

![alt text][image4]
![alt text][image5]

#### Hough transform

![alt text][image6]

#### Weighted image

![alt text][image7]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by checking the slope for every line detected by Hough transform. Firstly, if the slope is less than 0.5 (in absolute value), this line is discarded. If not, the slope is checked again to know whether is from the left side (negative slope) or right side (positive). Left and right points of the line are stored in its corresponding array. Minimum `y` and maximum `y` from the original image are stored. For minimum `y` the horizon (3/5) is taken into consideration. A new polygon is built taking points for the left side. New left line is calculated based on this polygon, taken the point nearest to maximum `y` and minimum `y` as a start and endpoint of this new line. The same approach is done for the right line. Once the new left and right lines are obtained, they are drawn in the original image.

##### Full example (find lane lines in every sample image)

![alt text][image8]

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when there are no lines in one side, or even on both sides.  

Another shortcoming could be, related to the former one, when lines are not clear, i.e., when are not well painted because are deteriorated by the time. Or maybe are not fully visible because of the snow or other weather conditions. 

### 3. Suggest possible improvements to your pipeline

Related to the shortcomings mentioned before, a possible improvement would be to detect also the delimited end sides of the road, i.e., where the road ends. 

Another potential improvement could be to detect automatically the best parameters depending on weather conditions, for example. In this way, possible errors are minimized because of external factors.
