# **Finding Lane Lines on the Road: Writeup**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
1. I converted the images to grayscale
2. I performed a gaussian blur
3. I performed edge detection on the image
4. I discarded edges outside a bounding polygon
5. I converted the image to Hough space so I could find which edges were lines
6. For each side of the screen: I discarded edges that didn't fit my expectations for a lane line. Ex: lines on the right hand side of the screen would be discarded if their angle wasn't within a specific bounds.
7. For each side of the screen: I invoked the existing draw_line() function to convert the set of lines into a set of highlighted coordinates.
8. For each side of the screen: I performed linear regression to fit a line between the highlighted coordinates

Step 8 is an addition/modification to the way that draw_line was proposed in the starter notebook.

### 2. Identify potential shortcomings with your current pipeline

My approach has multiple shortcomings:
1. Linear regression can't handle curves
2. My linear regression didn't elminate outliers. So a single unexpected edge-line outside the usual area could cause the entire line to be misplaced
3. My algorithm assumes that there is only one line on each side of the screen. If this is not true, the line will be drastically misfit.

### 3. Suggest possible improvements to your pipeline

Each shortcoming has multiple possible mitigations. Let's discuss one each:
1. Use polynomial regression
2. Eliminate outliers
3. Prior to running regression, group the edges into different groupings depending on their adjacency and angles. Run regression on each of these groups independently.
