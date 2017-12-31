# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

## My pipeline consisted of 7 stages:
1. Greyscale the input image
2. Apply the `cv2.inRange` to transfer it to a binary image
3. Apply a Gaussian Blur with a kernel size of 3
4. Apply Canny filter to detect edges
5. Apply the `region_of_interest` helper to get the desired region
6. Apply Hough transform
7. Draw lines on image

## How I modified the draw_lines():
My goal was to draw only two lines, one line on each lane.
Basically, I initialized 4 arrays: `  left_line_x,  left_line_y = [], []right_line_x, right_line_y = [], []` to store the x and y points in every iteration based on where it belongs. If the slope of the points is negative then it belongs to the left lane. Otherwise, it belongs to the right lane. After finishing this I ended up with 4 arrays with the data of all the x and y values for each of the two lane lines. My goal at this step was to average the points on each lane to make out only 2 coordinates that can be used to draw a line. I used `np.polyfit()` to do this job for me. I just entered by x and y arrays for each line and a degree of 1 and I got an output as a slope and a y-intercept (c). At the end, I used these data to draw my lines.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when something changes with the light source as this might change the color of the lane lines and would make them invisible.

Another shortcoming could be that my pipeline may not work with all camera inputs as I have defined the region of interest as a percentage of the input image from each side. So of the input image is not with the same ratios it may not give out a correct output.

Another shortcoming could be that when there is a problem with the input to the draw lines function, no lines are drawn at this exact frame.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use several color filters and combine images to make sure we get the lanelines with all colors. (Could be the solution for the challenge)

Another potential improvement could be to refine the Hough Transform and the Canny parameters to obtain more stable lines.
