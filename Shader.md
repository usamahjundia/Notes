## Shaders

When we render our models into the screen, usually we want to give them additional effects such as shadows, illumination, color and texture. In openGL this is achievable by utilizing GLSL shaders.

The shader consists of 2 parts : the Vertex Shader and the Fragment Shader. Both acts on different parts of rendering.

Firstly, the data stored in the VAO of the model goes into the Vertex shader. The vertex shader will execute for every vertices in the data.
The vertex shader has 2 main jobs : 
* To calculate the positions of the vertex on the screen.
* To calculate for each vertices a value (could be color, texture mapping, etc) which is a function of the vertex positions, hence it maps a value for each vertex.  This value will act as an input to the fragment shader.

The fragment shader takes the output of the Vertex shader as an input, and for each pixels in every planes (triangles) formed by the vertices, it calculates the final color of the pixel. The final color uses the values linearly interpolated from nearby vertices for its calculation. 

The following is an example of a simple Vertex Shader :
```GLSL
#version 400 core

in vec3 position;

out vec3 color;

void main(void){

    gl_Position = vec4(position, 1.0);
    color = vec3(position.x + 0.7, 1.0, position.y);

}
```
> Notice that besides the explicit output, we also set a variable called gl_Position.
> Remember that the vertex shader's job is to output 2 variables. The actual output which will go into the Fragment Shader input, and the location of each projected vertex location on the screen.

The following as an example of a simple Fragment Shader :
```GLSL
#version 400 core

in vec3 color;

out vec4 outputColor;

void main(void){

    outputColor = vec4(color,1.0);

}
```
> Notice that the input variable is the same name with the output of the Vertex shader.
