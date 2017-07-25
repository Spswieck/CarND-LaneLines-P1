**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My Pipeline first began by converting a still image from the video feed to grayscale and then I used the Canny function to find the gradient edges in the image. Following the Canny function the Gaussian_Blur() function was used to smooth the image into better lines. This Gaussian_Blur() function is only necessary so that we can manually configure the kernel size where as the Gaussian smoothing natively present in the Canny() function is not easily manipulated. After applying the Gaussian_Blur() the next step is to pass the data through a region mask created primarily using the fill_poly() function. The region mask allowed the extra data that we do not care about to be filtered out, limiting data examined and inherent system noise. With the lanes extracted the hough_lines() function was used to extract line segments from the canny edge contrast lines. After the hough_lines were extracted I created a moving average of the slopes and y-intercepts then recalculated two lines constrained by their vertical limits they were combined with the original image which achieved the overall goal of this project.

In order to extract single lines I made a few successful observations. The left and right lane lines have a roughly equal but opposite slopes.. i.e one is a positive slope and one is a negative slope. I used this to my advantage to constrain the data and take two moving average data sets of the slope and y-intercepts, one for each lane line. Then using the standard line equation y=mx+b I recalculated both lines by providing the average slope and average y intercept and because I know the vertical limits of the line I reorganized the equation too: x=(y-b)/m whixh allows me to calculate the x co-ordinate when I can chose where the y position starts and stops. 

### 2. Identify potential shortcomings with your current pipeline


The moving average filter adds a large system delay and does not perform well in scenarios of fast variation.


### 3. Suggest possible improvements to your pipeline

Many of the threshold values could be improved but that would just take a large amount of time for trial and error based on my current understanding.
