# Lane Detection for Autonomous Cars

## Objective
The objective of this project was to design and develop a lane detection algorithm for autonomous vehicles applications. The self driving car market is growing at a very fast pace. Many companies are working in this problem trying to solve every aspect of it, so that autonomous cars can drive safely on the roads. It is a very complex problem due to the many aspects that it relies on: robotics, path planning, navigation, computer vision, mechanics, etc.

This project is focused in the computer vision aspect of it, a crucial module. If an automated car is going to drive around unpredictable environments, it has to be able to perceive and detect every small detail that surrounds it.

So for this project, a lane detection algorithm is proposed as part of the perception component for a self driving vehicle. By using a video feed input of a car driving on the highway, the algorithm will detect where the lane is so that the car can use its location to avoid getting out of the it. It will also be able to predict any turn on the road to secure a good tracking of the lane. The project was developed using Python,Numpy, OpenCV, Canny, Lane-Detection, Hough Transform.

## Algorithm

The proposed algorithm follows a straight forward pipeline with several steps as shown in the following activity diagram. 

![6](https://user-images.githubusercontent.com/73324896/145776174-e90be8c1-4cc7-4bec-96d2-642168c45ee6.png)

-	The frames of a video are captured. This image inputs are from a video of a car driving on the highway.

![1](https://user-images.githubusercontent.com/73324896/145776313-a311ff86-c7ff-40bc-a324-ca7185eef8e8.png)

- The first step will be to denoise the image by applying a filter like a Gaussian mask that smooths the image and removes any undesired pixel values that could prevent the correct detection of the lanes.
- Secondly, an edge detection algorithm is used to detect the lines that form the boundaries of the lanes. For this, the image has to be converted to grayscale, and then to binary. Once this is done, the edge detection is achieved by applying a row kernel [-1 0 1] to each pixel of the image. 

![2](https://user-images.githubusercontent.com/73324896/145776489-91e2f3b6-b0ed-4cda-8ca8-42c423751ca7.png)

- As it can be seen in the image above, there are lots of unwanted edges being detected. To fix this, the image will be masked so that it only detects edges in a region of interest. This helps because the road is always going to be in the same location on the image. The following figure shows the result of masking the edges image:

![3](https://user-images.githubusercontent.com/73324896/145776562-7f5074d2-b7fe-4658-aae4-4b9fb3fa941c.png)

-	Once the desired edges are detected and the unwanted ones have been removed, the next step is to use the Hough Lines detection algorithm, which gives the location of all the lines in the image. The parameters of the function (rho and theta) were determined by trial and error so that only the most notable lines are detected.
-	By applying basic linear algebra, all the detected Hough lines will be classified as left side lines or right side lines. The lines are classified depending on the value of their slope and where their initial and final points are approximately located with respect to the center of the image. 
-	Once everything is detected, the results are represented in the input frame, captured at the beginning of the algorithm.

![4](https://user-images.githubusercontent.com/73324896/145776872-10390d66-ae8c-45d4-8e95-0be11e3ed5e0.png)


