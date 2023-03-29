# 3D-Develop-Basic

## Terminology

- Rendering: 3D scene to a 2D image (rendering).
3D rendering can be defined as a function that takes a 3D scene as an input and outputs a 2D image.

- Inverse graphics: 2D image to a 3D scene

- Differentiable rendering (DR):  It belongs to the methods used for solving inverse graphics problems.
The goal of **differentiable rendering** is to provide a <U>differentiable rendering function</U>, that is to say to compute the derivatives of that function with regard to different scene parameters.

![render_example](https://blog.qarnot.com/wp-content/uploads/2021/10/2.png)


![render_example2](https://blog.qarnot.com/wp-content/uploads/2021/10/3.png)

Once a renderer is differentiable, it can be integrated in optimization or neural network pipelines. These pipelines can then be used to solve inverse graphics problems such as 3D reconstruction from 2D images or light transport optimization tasks.

- Ray tracing: is a fundamental algorithm that involves tracing rays of light from the camera into the scene and calculating how they interact with objects and surfaces to determine their color and brightness

- Path tracing: on the other hand, is a more advanced form of ray tracing that simulates the random path that light takes as it bounces around a scene.

![path_tracing_formula](https://blog.qarnot.com/wp-content/uploads/2021/10/4.png)


`Lo` : light intensity (radiance) at a point

`Le` : emitted radiance at this point

`Li` : incoming radiance to this point

`f` : Bidirectional Reflectance Distribution Function (BRDF) that quantifies how light is reflected

## Camera and Primary Rays

The camera is defined by its origin and the image plane. The image plane is subdivided into a grid of pixels corresponding to the render resolution and rays are launched from the origin of the camera through the pixels of the image plane.

Now that the image plane has been transformed into a pixel grid, how is the color of each pixel collected? Propagating the boundary of a pixel through the scene highlights a large region of the scene containing multiple objects, all of which will contribute to the final color of a pixel. To compute that color, all the light passing through the pixel will have to be taken into account. 

Mathematically, this corresponds to integrating the intensity of light (radiance) over the area of the pixel. 

![pin_hole_model](https://blog.qarnot.com/wp-content/uploads/2021/10/5.png)

 A Monte Carlo estimator will be used to compute the value of this integral: N rays will be launched randomly through the pixel into the scene and evaluate their light intensity. This operation is shown in Figure 1.2. The pixel radiance value at position (i,j) in the image grid can be written:

 ![formula2](https://blog.qarnot.com/wp-content/uploads/2021/10/6.png)

`p` : the probability distribution function used to sample the pixel space with rays

`uk` : the random rays.

Those rays going from the camera into the scene are called <u>primary rays</u>. Once these rays have been intersected with the scene geometry, they are going to be propagated through space. At each intersection, light intensity at the intersection point is estimated by solving the rendering equation.
A single ray (a single sample) is launched from this intersection point into the scene. While launching a single ray per pixel won’t give precise results, launching multiple rays per pixel will give a good approximation of incoming light.

![primary_ray](https://blog.qarnot.com/wp-content/uploads/2021/10/7.png)

