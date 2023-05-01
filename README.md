# Image-Feature-Detection-and-Recreation

My individual module in our senior design project, the concept was to taken an image string, locate the png file related to that string in some shared folder, and produce a path of coordinates based on that image, to later be processed by 2 stepper motor controllers, and then recreated with a marker onto a whiteboard. 

<h2>Gray Scaling</h2>
In order to simplify the image, the image is first filtered to remove color. This feature does make working with highly saturated images difficult.

![heart1](https://user-images.githubusercontent.com/77860961/235528192-b07e892b-9157-4fc1-a2d3-01606ce403e4.png)
Note that although the image does not appear in grayscale, this is an issue between matplotlib and OpenCV.

<h2>Convolution</h2>
The images are then pu through a convolution algorithm to get the relevant features

![heart2](https://user-images.githubusercontent.com/77860961/235528406-ef3acaf1-1f53-49aa-970c-4370053286aa.png)

<h2>Corner Detection</h2>
Using the OpenCV library, conditions can be specified to locate corners on the convoled image.

![heart3](https://user-images.githubusercontent.com/77860961/235528693-1b0d585a-9855-40a6-83bf-ab06d742b2ec.png)

<h2>Edge Detection</h2>
By checking a designated number of checkpoints spaced evenly along any distance, it can be determined if an edge is located between any two corners by cross referencing the pixel value of the convolved image at those locations. By running this test between every combination of corners, all edges can be located, informing the rest of the algorithm what is a valid path to travel

<h2>Implementation Constraints</h2>
Currently these functions only work as intended on 2D simple geometric figures. It does not account for skipping between points that are not connected by edges due to the hardware limitations of this project. There is proof of concept in the HeartTest file, for this to work for more complicated images. Reproducing a proper arc was challenging, and required different specifications in tolerance for the quality of the corners, and the spacing of the mid point on the arcs from where it would be on a straight edge. In order to solve this I reran very similar algorithms any time the numbder of located coners did not equal the value of the number of located edges. It should be possible to determine some iterative value to increase these corner and edge tolerance starting from a very low value, until the conditions of edges=corners is validate, otherwise it is a complex image, and which would need to be its own seperate algorithm.

<h2>Successful Images in Testing</h2>

<img width="852" alt="Success" src="https://user-images.githubusercontent.com/77860961/235530573-cbeb4dd2-d08e-4b58-84db-1c8f2262b892.PNG">

