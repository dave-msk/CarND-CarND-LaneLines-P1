#**Finding Lane Lines on the Road** 

##Writeup for Lane Line Project

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[image1]: ./writeup_eg/figure_1.png "original image"
[image2]: ./writeup_eg/figure_2.png "color selected"
[image3]: ./writeup_eg/figure_3.png "Canny detected"
[image4]: ./writeup_eg/figure_4.png "region cropped"
[image5]: ./writeup_eg/figure_5.png "lane-lines"
[image6]: ./writeup_eg/figure_6.png "combined"
---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, color selection is performed to extract the bright pixels, with a lower blue threshold to recognize the yellow lane line as well. Then, the color-selected image is converted into grayscale and blurred before applying Canny edge detection. The resulting image from Canny is then cropped into a trapezoidal region to reduce noise and hough-transformation is applied for line segments extraction. Finally, the left and right extracted lines are joined and extended accordingly.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following procedures:
(1) Split the line segments into two sets, one with positive slope, one with negative.
(2) The end points of line segments in the same set are averaged to compute the representative line for the set
(3) A line is drawn from the bottom to the top end point whose coordinates are calculated using the representative line of each set

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![original image][image1]

![color-selected][image2]

![Canny-detected][image3]

![region-cropped][image4]

![lane-lines][image5]

![combined][image6]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the image's contrast is low, which would have a huge effect on the color selection as the thresholds are static. If the whole image is dark or dim, then it is possible for the color selection process to filter out everything. On the other hand, if the whole image is bright, the information provided may even be useless.

Another shortcoming could be when large contrasts are evenly distributed. This happens when driving under a loose canopy in a sunny day. As a result there would be a large amount of strong intensity change which would introduce a great amount of noise in the resulting edge-image.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to use a dynamic threshold for color selection, which would mitigate the low-contrast problem.

Another potential improvement could be to apply histogram equalization in the preprocessing phase.
