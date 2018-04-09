# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I blurred the image by calling the `gaussian_blur` function, then I used the `canny` fuction to find the edges using the canny transform, then I used a poligonal mask to only focus on the lane lines and mask out everything else in the image, then I used `hough_lines` function to find lines by using the Hough transform, and finally I used the `weighted_img` function to overlap the image obtained after the hough transform and the original image.

In order to draw a single line on the left and right lanes, I modified the `draw_lines` function by calculating the slope and center of each detected line and separating them by positive and negative slope to determine if the line belonged to the right side or to the left side, after doing this I calculated the y-intercepts of the lines and created a loop to make the line start at y=540 (the bottom of the image) so that if the detected line did not already start at y=540 it would change this and calculate the x coordinate by using the y-intercept. For the second point the y coordinate would be a set point about a third of the way towards the middle of the image and the new x coordinate would be calculated by using the previously calculated x, the slope, and the calculate y, using a modified version or the slope formula. Finally the `cv2.line` function is called to draw the lines using the beginning and end points that were calculated for each lane line.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming is that the code is written for a set image size. Also the vertices for the poligonal mask are set values and not calculated values depending on the image shape. So this code would not work on an image with bigger dimensions or smaller dimensions.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to edit the code to calculate certain values based on values derived from the `.shape` function. So that it would be more universal and work with most cases.

Another potential improvement could be to rethink the way `draw_lines` works and perhaps use a different criteria to separate the lines and therefore prevent the shaking and have the lines more stabilized.