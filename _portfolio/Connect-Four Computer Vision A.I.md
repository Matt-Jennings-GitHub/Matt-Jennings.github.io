---
title: "Connect-Four Computer Vision A.I"
date: 2020-06-02
tags: [computer vision, minimax, artificial intelligence]
header:
  image: "/images/skyline.jpg"
  teaser: "/images/ConnectFour/ConnectFourTh.png"
excerpt: "Computer Vision, Minimax Algorithm"
mathjax: true
---

A computer vision project to detect the presence of the board game 'ConnectFour' from an image, and identify the next player's optimal move. 

## Demonstration

Below are some example outputs of the final program:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/ExampleOutput1.png" alt="Example Picture Scan">

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/ExampleOutput2.png" alt="Example Picture Scan">

We use computer vision techniques to identify the presence and state of the game-board from an image, then apply a MiniMax algorithm with Alpha-Beta pruning to determine the next best move, and display the result!

## How it works

# Step 1: Image Analysis

Various computer vision techniques, using the Python implimentation of CV2 were applied to accomplish the task of identifiying game board and counter positionsfrom a given picture.

We first apply a bilateral filter to reduce noise and smooth the image and assist edge detection:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/BilateralFilter.png" alt="Bilateral Filter">

Next, we apply the Canny Edge Detection Algorithm which is known to perform well on smoothed images:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/EdgeDetection.png" alt="Canny Edge Detection">

We can then use CV2's FindCountours to find contours within the image before aprroximating those which represent polygons with approxPolyDP, noting we expect shapes with a high number of verticies (like our circular counters) to have a low arclength / perimiter ratio.

```python
# Edges to contours
contours, hierarchy = cv2.findContours(edge_detected_image, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE) 
# Contours to polygons
approx_polygon = cv2.approxPolyDP(contour,0.01*cv2.arcLength(contour,True),True) 
```
Then we select which contours are likley to represent circular slots by applying conditions on each polygon's dimensions, area and vertices: 

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/CirclesDetected.png" alt="Circles Detected">

Great - we have successfully located the circular contours which most likley represent our board. Contour approximation to polygons proved more effective and adaptable than other approaches such as the Hough Circle Transform, which especially struggles to locate the less perfect holes in off-angle images with backgrounds. 

Next, we identify which coloured counters have been placed where in the grid using colour filtering. Coverting the image to HSV space allows us to pick-out the Red and Yellow from a range of hue values and construct a mask for each player's colour:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/ColourMasks.png" alt="Circles Detected">

Now, as there is a slim probability of reliably identifying every grid hole in any given image, we extrapolate the exact grid position based on the information we did gain. This step could be improved with more trigonometic handling to account for more extreme off-angles, but proves effective for most images.

```python
img_grid = np.zeros([img_h,img_w,3], dtype=np.uint8)
for x_i in range(0,cols):
    x = int(min_x + x_i * col_spacing)
    for y_i in range(0,rows):
        y = int(min_y + y_i * row_spacing)
        r = int((mean_h + mean_w)/5)
        img_grid_circle = np.zeros((img_h, img_w))
        cv2.circle(img_grid_circle, (x,y), r, (255,255,255),thickness=-1)
        img_res_red = cv2.bitwise_and(img_grid_circle, img_grid_circle, mask=mask_red)
        if img_res_red.any() != 0:
            grid[y_i][x_i] = id_red
```

Finally, we iterate through the grid with the above loop and apply a bitwise AND to cross-reference the grid positions with our colour masks to locate the colour of each counter in the game:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/GridOverlay.png" alt="Grid Overlay">

Success! We have picked-out the state of the game from a picture, irrespective of the background and off-angles.

# Step 2: Optimal Next Move Prediction

Having obtained the state of the grid, we must now identify which player is to move next, and where they should place their counter.

By using a scoring function to quantify the advantages of each move, we can scan the tree of possible resulting game states and arrive at the optimal next move. 

As it would be infeasable to scan the search-space for all possible resulting games, we limit our seach by applying the Minimax algorithm with alpha-beta pruning to the tree nodes. A more detailed explanation of application of Minimax to Connect-Four can be found [here](https://towardsdatascience.com/creating-the-perfect-connect-four-ai-bot-c165115557b0).

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/AlgorithmImage.png" alt="Minimax algorithm image">

We can now take the information we have extracted from the image and apply the Minimax algorithm to determine the best next move:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/Output.png" alt="Program Output">

Identifying yellow is next to move, the Minimax algorithm then sucesfully blocks red from winning!

Testing showed promising generalisation to a variety different images, and the limitations of the approach used can be seen by examining the output at each stage of the process:

<img src="{{ site.url }}{{ site.baseurl }}/images/ConnectFour/ExampleCases.jpg" alt="Example Cases">

I hope this project has given some insight into some of the techniques that can be used for computer vision, and display a fun application of the Minimax algorithm to board games! Full source code and further details can be found on my [GitHub](https://github.com/Matt-Jennings-GitHub).