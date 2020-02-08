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

My pipeline consisted of the following high-level steps. 

1. The image is first converted into an hsv colorspace. 

2. Using the Gaussian bur, the "white noise" in the hsv_image is reduced so that only the significant features are highlighted. 

3. The Canny() method is then applied this smoothen image to generate edges of those features. 

4. The region containing the lanes is then defined on the Canny output image. An offset value from the image's horizontal and vertical center is created. The lanes are not assumed to be symmetrical about the driver's centerline. 

5. Hough transform is applied within the binary region of interest. This function invokes drawlines(), which will take the lines from the Hough output image and classfiy them as right or left lanes based on their slopes.  Assuming a line will be extended to the bottom of the image, the line will be drawn relative to the y-min of the lines. This value is slightly offset to avoid crossing at the top. Averages of the slopes and intercepts are calculated and used to calcuate the line coordinate pairs by rearranging the slope-intercept equation. 

6. This binary line image is then imposed on the original image using weighted_img() to give the final output image as shown below. 

![output image1](/test_images/solidWhiteRight.jpg)

### 2. Identify potential shortcomings with your current pipeline


1. If the lanes are curving too drastically, we can no longer assume the right lane is sloping negatively. 
2. If the lanes are curving to the left, we encounter the same invalid assumption. 
3. An obstacle along target lane will be included in the region of interest and may skew the averages. 



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

1. Label the lines as positive or negative slopes first and then pass it through a nested conditional to determine if this is in fact a right or left lane. If there exists a line to the right of an initially classified right line within the region of interest, it will need to be appended to the "left" list. 
2. Distinguish geometry of lanes from an obstacle. Alternatively, maybe the program can assume an object is 
3. Votes are determined by 
