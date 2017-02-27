#**Finding Lane Lines on the Road** 




---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[gray]: ./examples/gray.jpg 
[edges]: ./examples/edges.jpg 
[interest_edges]: ./examples/interest_edges.jpg 
[result]: ./examples/result.jpg 
---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps: 
1. converted the images to grayscale
![][gray]
2. gaussian blur the gray image
3. canny image to get edges 
![][edges]
4. fill the canny result by region of interest
![][interest_edges]
5. through hough lines get one extended left and right line
6. merge original image and the hough output
![][result]

In order to draw a single line from the line segments, I modified the draw_lines() function.First,I use -0.5 and 0.5 as the slope boundray to seperate left line and right line,after this all lines seperated into two line group.Then i select the longest line from line group respectively,i extend these two lines as the final averaged, extended line


###2. The potential shortcomings with my current pipeline

One shortcommings  : If the camera position changed,the position of lane line in the picture can be different . Thus after my region filtering,i may get other  lines exceipt lane lines.This can lead to  the wrong final extended line 

Another shortcommings: because i use the longest line as base line to extend,if the road is old,and the lane lines are all short  obsecure, the draw_line() may select the wrong lane line to extend 

###3. Suggest possible improvements to your pipeline

Maybe i should use select the frequently appeared slope in both selected line groups,and use it to verify the selected longest line. If the slope of longest line is two different from it(maybe 20%) ,i will  drop it and select another line