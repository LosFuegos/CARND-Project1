#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image1]: ./Weighted_solidWhiteCurve.jpg "Image_1"
[image2]: ./Weighted_solidYellowLeft.jpg "Image_2"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a gaussian noise kernel. On the output from 

gaussianblur I applied a canny trasnform with low and high threshold of 50 and 200 respectivly. Using the canny output as input getting the 

houghLines. After the lines where drawn I masked the image using a polygon, then used addWeight to to lay the mask on top of the original

image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by using a nested for loop to

access the coordinates to find the slope of each line and median point. Used the fact that left and right lines would have opposite signs.

From there I narrowed down the range to reduce the jitteryness of my lines and also split the img vertically along x = 480. Once lines were

organized I stored median and slope values for both sides into there respective arrays. Then took the average of the slopes and median, 

which I used in y - y' = M(x -x') to find x at y = 960,320 for both sides.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

[image1]

[image2]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when I would narrow the field of acceptable slopes I get errors. That seemed to fix 

this but lines might disappear in some frames.

Another shortcoming could be can't seem to get past the shadows in the challenge video.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to find the thresholds for the cv2.inRange function.

Work on a way to better filter outliers in the drawlines function.
