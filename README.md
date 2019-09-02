# Autonomous Car Nanodegree: Finding Lane Lines on the Road
Objective
---
The objective of this project was to detect lane lines on the road.
We were to develop and test our pipeline on a series of test image iteratively and scale it out to detect lane line on video feeds.

Pipeline
---
The approach for this lane line detection broadly consisted of following steps:
1. Color transformation of the RGB base image into Grayscale image.


		Original Image

		Grayscale Image

2. Use of Gaussian smoothing with the kernel size of 5 pixels to smooth out the image and reduce noise.


		Gaussian Smoothed Image

3. Detect edges using Canny Edge detection.

Edge Detected Image	

4. Given the lane lines would be available within the specific area of the image. Generating region of interest masks with polygonal shape and applying as a mask on the edge detected image.

		ROI Mask Applied Image

5. Generating Hough lines for the ROI mask applied image.

6. Filtering & processing lines based on Hough Lines detection further computation chain to increase the accuracy and the detected lane extrapolation:
	6.1. Finding the slope for each set of points detected by Hough transformation.
	6.2. Segregating them into the distinct right lane and left lane based on the slope calculated above, such the line with the slope between +15 to +75 degrees was deemed to be left lane lines and -15 to -75 degrees was determined to be right lane line.
	6.3. Outlier removal based for each of the lane line set based on the slope with 2 sigma bounds. This will help removal erroneous detections and also, significantly helped with the last challenge video to an extent to removal out spurious detection.
	6.4. Fitting LinearRegression model on each of the outlier removed left and right lane dataset. 
	6.5. Finding bottom and top coordinates for each left and right lane LinearRegression fitted model and drawing the lane lines.
	
Processed Hough Line Image		

7. Splicing processed hough line image and the original image to create a lane demarcated composite image.  

		Output Lane Detected Image

Potential Shortcomings with the current pipeline
---
1. Lane markings in colors other than white or yellow.
2. Bound to detect spurious lines other than lane lines.
3. If the camera angle or placement changes, the ROI masking technique would fail.
4. Rigid classification of right and left lane lines based on the slope would also be susceptible to camera placement or orientation change.
5. The detection of right and left lane, calculation of slope, outlier elimination and fit a linear regression model is very computationally intensive.

Possible Improvements to the pipeline
---
1. Handle the camera angle and placement changes
2. Ability to handle image and videos in different lighting conditions
