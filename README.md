# Perception-Challenge
This project creates a perception algorithm that can detect the boundaries of a straight path defined by cones taken by a camera attached to a vehicle.

## The answer picture
![](https://github.com/Qin-Zihan/Perception-Challenge/blob/main/answer.png)

## Methodology
The code primarily aims to detect and visualize lines formed by red-colored objects in an image. It performs this operation using the following step-by-step methodology:

Color Space Conversion:
The RGB image is converted to the HSV color space. The reason for this conversion is that the HSV color space provides better separation for color-based detection, especially for colors like red which wrap around the hue wheel.

Thresholding for Red Color Detection:
To capture the red color in the HSV space, two masks are created: one for the lower hue range and another for the upper hue range. Both masks are then combined to produce a single binary image that indicates the presence of red color.

Contour Detection:
External contours are detected in the binary mask. These contours represent the boundaries of the red objects in the image.

Separation of Contour Points:
Points from the detected contours are separated into two groups based on their horizontal (x) position in the image:

Points on the left half of the image.
Points on the right half of the image.
Additionally, a condition is implemented to ignore points from the top-right corner of the image.
Line Fitting:
Using the separated contour points from both the left and right sides, two lines are fitted. These lines represent the general direction or orientation of the red objects in the respective halves of the image.

Line Drawing:
The fitted lines from the previous step are drawn onto the original image using a red color, to visualize the orientation of the detected red objects.

## Reflection from debugging
In completing this challenge I ran into a lot of problems with the code, but in the end I managed to solve them all. One of the things I tried when I first started this project was to use the full red HSV range, but I realized that there were a lot of red interfering items in this image in addition to the cones, so I scaled back the HSV range.
In fitting the straight lines, I initially wanted to try using a Hough Transform, but that didn't work. After I learned the principle of Hough Transform, I learned that because these contour points do not form a continuous straight line, so that Hough Transform does not work. After that I tried to fit these points using the fitLine function, and because of the presence of the noise points in the upper right corner of the photo, the straight line on the right could not fit all the cones perfectly, so I manually eliminated the noise points in this area.

## Libraries used
Modules in OpenCV:
Core Functionality (opencv2/opencv.hpp)
High-level GUI (opencv2/highgui/highgui.hpp)
