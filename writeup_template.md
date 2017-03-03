#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/solidWhiteRight.jpg "solidWhiteRight.jpg"
[image2]: ./test_images_output/solidWhiteRight.jpg "solidWhiteRight.jpg"

[image3]: ./examples/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch.jpg"
[image4]: ./test_images_output/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch.jpg"

[image5]: ./examples/solidYellowLeft.jpg "solidYellowLeft.jpg"
[image6]: ./test_images_output/solidYellowLeft.jpg "solidYellowLeft.jpg"

[image7]: ./examples/solidWhiteCurve.jpg "solidWhiteCurve.jpg"
[image8]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve.jpg"

[image9]: ./examples/solidYellowCurve.jpg "solidYellowCurve.jpg"
[image10]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurve.jpg"

[image11]: ./examples/solidYellowCurve2.jpg "solidYellowCurve2.jpg"
[image12]: ./test_images_output/solidYellowCurve2.jpg "solidYellowCurve2.jpg"


---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

In order to find lane line I prepared a line_finder() class and process_image() function. 
line_finder() class is consisted with all required functions. I also added comments to the code.

In order start a class I defined a variable with line_finder() and used this variable in process_image() function. In the class first I called process() function. process() function call pp_image() function to convert image hsv color space and get v layer. I used threshold for v layer with 226 to take only bright colors. I need a single channel image for hough lines so I sent this one channel. After finding bright area in image I used get_lines() function to detect lines with hough lines(cv2.HoughLinesP).
In order calculate slope (m) and fixed (b) values with line_fit() function I checked number of the lines. If number of the lines smaller then 10, get_lines() function returns false and uses previous values. Otherwise using line_fit() function I calculate new m and b values. 

I used get_borders() function to detect negative and positive slopes and purify them with purify() function. I checked differences new and old value of m and b (abs((m-old_m)/old_m), abs((b-old_b)/old_b)). If differences higher then threshold (self.th) then use old b, m values as new values in order to prevent line ramble.

Using get_points() function I calculated x values from m and b values for y size of image and limit line lenght with a constant value (for calculating y2 value multiply with 0.63) 

Last step using draw_border() function I draw left and right lane lines and combine with the original image.

Pipeline draw lane lines on the test_images: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]
![alt text][image8]
![alt text][image9]
![alt text][image10]
![alt text][image11]
![alt text][image12]

###Video
#Solid white lane on the right
[![solidWhiteRight.mp4](https://img.youtube.com/vi/cJWOE5xjksg/0.jpg)](https://www.youtube.com/watch?v=cJWOE5xjksg)

###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
