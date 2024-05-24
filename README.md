# opengl-ray-tracing-1

> [!NOTE]
> This repository holds the completed result of my project but the source code.
> I cannot post the source code publicly here to avoid plagiarism, so I put it in another private repository. Although, I can show it upon request.



### RESULT

![](/test1.jpg)
![](/test2.jpg)
![](/table.jpg)
![](/siggraph.jpg)
![](/toy.jpg)
![](/snow.jpg)
![](/spheres.jpg)



### OVERVIEW

In this assignment, you will be building a ray tracer. Your ray tracer will be able to handle opaque surfaces with lighting and shadows. Provided for you will be starter code that will load scene data from a file.

Step 1: Uniformly send out rays from the camera location. Since the camera does not have to move, you can assume that its location is (0,0,0). You should use backwards ray tracing where rays are sent from the camera, one ray per pixel. The final images should be 640x480, but for debugging you should use smaller resolutions with faster rendering times. For example, if you halve each dimension, you would send out 1/4th of the number of rays. You can use the field of view of 60 degrees.

Step 2: Write the intersection code. The mathematical solutions for the intersection code are provided in the lecture notes.

Step 3: Implement the illumination equations (provided below).

Step 4: Create still images showing off your ray tracer.



### ILLUMINATION

At each intersection point, you need to first determine if it is in shadow, separately for each light source. You do this by launching a shadow ray to each of the lights. If the point is in shadow, its color with respect to that light should be (0,0,0), that is, black. If the point is not in shadow, use Phong shading to determine the color of the point with respect to that light:

I = lightColor * (kd * (L dot N) + ks * (R dot V) ^ sh)       (for each color channel separately; note that if L dot N < 0, you should clamp L dot N to zero; same for R dot V)

The final color of the point is the sum of the contributions from all lights, plus the global ambient color. You only add the global ambient color once, regardless of how many lights the scene has, and regardless of how many lights are visible from the point. Note that it could happen that a point is in shadow with respect to all lights. In this case, the final color will be the global ambient color. Or a point could be in shadow with respect to some lights, but not others. Or, all lights may be visible from a point. If the final color is greater than 1.0, you should of course clamp it to 1.0.

In order to compute I, you must determine the normal N at the intersection point. For triangles, you should interpolate the x,y,z coordinates of the normals given at each vertex, and then normalize the length. Use barycentric coordinates for interpolation of triangles. You should interpolate not just the normals, but also diffuse, specular and shininess coefficients. For spheres, the normal is simple to calculate based on the center of the sphere and the point location.



### THE PROJECT INCLUDES

1. Triangle intersection
2. Sphere intersection
3. Triangle Phong shading
4. Sphere Phong shading
5. Shadows rays
6. Still images



### SCENE DESCRIPTION FORMAT

The first line is the number of objects in the file. There are three types of objects supported: lights, triangles, and spheres. Color values range from 0-1. You can use our provided scenes, or create your own scenes.
Ambient Light (3 floats).
Then you can have lights, spheres or triangles.

1. sphere
- position (3 floats)
- radius (1 float)
- diffuse color (3 floats)
- specular color (3 floats)
- shininess (1 float)

2. triangle
(then the following, repeated three times (once for every vertex)
- position (3 floats)
- normal (3 floats)
- diffuse color (3 floats)
- specular color (3 floats)
- shininess (1 float)

3. light
- position (3 floats)
- color (3 floats)

Example scene files (seven examples total; see "More examples" below)
The following is an example of a scene description file. It sets a gray sphere of radius 1 at (0,0,-3). It sets a white light source at the origin.

		  2
		  amb: 0.3 0.3 0.3
		  sphere
		  pos: 0.0 0.0 -3.0
		  rad: 1
		  dif: 0.3 0.3 0.3
		  spe: 0.5 0.5 0.5
		  shi: 1
		  light
		  pos: 0 0 0
		  col: 1 1 1

Here is the file corresponding to the above example: [test1.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/test1.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/test1-solution.jpg)

### MORE EXAMPLES

Basic test scene with a triangle, ground plane and sphere: [test2.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/test2.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/test2-solution.jpg)

Five spheres: [spheres.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/spheres.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/spheres-solution.jpg)

A table and two boxes: [table.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/table.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/table-solution.jpg)

SIGGRAPH: [SIGGRAPH.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/SIGGRAPH.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/SIGGRAPH-solution.jpg)

Toys: [toys.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/toys.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/toys-solution.jpg)

Snowman: [snowman.scene](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/snowman.scene) | [Solution](https://viterbi-web.usc.edu/~jbarbic/cs420-s24/assign3/snowman-solution.jpg)
