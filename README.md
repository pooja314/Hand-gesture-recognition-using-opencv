# Hand-gesture-recognition-using-opencv
 using Convex Hull
 
>A Convex object is one with no interior angles greater than 180 degrees. Hull means exterior of the object. Convex hull of a shape or a group of points is a tight fitting >convex boundry around the points or shape. 
 
 I am using convex hull to recognize number of fingers in a live video
 
 # How it works:
 A Person has to place hand inside the ractangular box which is visible in video frame. From this rectangular ROI we have the image of hand. A HSV color space image of this rectangular image is now used to create mask of hand image. This mask image will be used in extracting hand image
After that, some morphological operations are performed on this mask to remove noises. Next step is to find out the contours in this mask image. 

>Contour is a curve joining all the points along the boundary of a certain shape. As they define the boundary of the shape, an analysis of these
>points can reveal key information for shape analysis and object detection and recognition. 

In our case, 'hand' is the contour which we want to extract.  Next step is to draw convexity hull around this hand contour.  Calling cv2.convexHull() function returns a 2-D points set. This points are used to calculate convexity defects. 


for understanding what Convexity Defect is :
https://dsp.stackexchange.com/questions/26996/what-is-the-deffinition-of-convexity-defect-in-imageprocessing#:~:text=In%20simple%20words%2C%20convexity%20defect,%3A%3AconvexHull%20function%20for%20details).


cv2.convexityDefects() function returns an array where each row contains these values - [ start point, end point, farthest point, approximate distance to farthest point ].

![Convexity defects in hands](https://miro.medium.com/max/682/1*ICriWpg3imhLUJQI-o8INA.png)

Usign this set of values, angle between starting point, far point and end point  is calculated. If this angle is less than 180 than it is desired defect i.e. the convexity defect point between fingers. Otherwise we will discard this convexity defect point. 

Number of fingers is calculated based on convexity defect points.
