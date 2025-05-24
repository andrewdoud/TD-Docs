

# MAT

MAT - Derivative




# MAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
[![OP MAT.png](images/b/bc/OP_MAT.png)](File_OP_MAT.html)
MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.
See also [Category:MATs](Category_MATs.html "Category:MATs") for a full list of articles related to MATs.
**Material Operators**, or **MATs**, are used to create materials for geometry. They can be applied to geometry using the **Material** parameter on the Display page or any [Object Components](Object_Component.html "Object Component").
The [Phong MAT](Phong_MAT.html "Phong MAT") and [GLSL MAT](GLSL_MAT.html "GLSL MAT") are designed to use [TOPs](TOP.html "TOP") and [GLSL](GLSL.html "GLSL") programs (pixel and vertex shaders) as inputs to create more advanced shaders.
The most commonly used MAT is the Phong MAT. The Phong MAT contains a large number of lighting options that allow the users to create some very unique effects.
[Phong MAT](Phong_MAT.html "Phong MAT") - applies a phong shader to the geometry. Geometry must have [normals](Normals.html "Normals") for specular shading to work. Geometry must have [Texture Coordinates](https://docs.derivative.ca/index.php?title=Point_Attributes&action=edit&redlink=1 "Point Attributes (page does not exist)") for any applied maps to work (ie Color Map, Bump Map, Specular Map, etc). Geometry can be deformed using the Deform parameter page. The Phong MAT offers other advanced features for [Transparency](Transparency.html "Transparency"), [Rim Lights](Rim_Light.html "Rim Light"), and [Shadows](Shadows.html "Shadows").
[PBR MAT](PBR_MAT.html "PBR MAT") - applies a PBR shader to the geometry. Use in conjunction with an [Environment Light COMP](Environment_Light_COMP.html "Environment Light COMP"). [Substance Designer](http://www.allegorithmic.com/products/substance-designer) PBR materials can also be used via .sbsar files loaded into the [Substance TOP](Substance_TOP.html "Substance TOP").
[Line MAT](Line_MAT.html "Line MAT") - renders the geometry edges as lines and points with different geometry.
[Constant MAT](Constant_MAT.html "Constant MAT") - this material applies a constant flat color to the geometry. There is no specular shading, ie shading is not affected by the camera or light positions.
[PBR MAT](PBR_MAT.html "PBR MAT") - applies a PBR shader to the geometry. Use in conjunction with an [Environment Light COMP](Environment_Light_COMP.html "Environment Light COMP"). [Substance Designer](http://www.allegorithmic.com/products/substance-designer) PBR materials can also be used via `.sbsar` files loaded into the [Substance TOP](Substance_TOP.html "Substance TOP").
[Depth MAT](Depth_MAT.html "Depth MAT") - can be used to get depth information from the geometry for a depth-pass render. It will not render any color.
[GLSL MAT](GLSL_MAT.html "GLSL MAT") - a powerful material operator which applies Pixel and Vertex GLSL shaders to the geometry. Geometry can be deformed on the GPU using vertex shaders. Geometry must have [Texture Coordinates](https://docs.derivative.ca/index.php?title=Point_Attributes&action=edit&redlink=1 "Point Attributes (page does not exist)") and [normals](Normals.html "Normals").
[Point Sprite MAT](Point_Sprite_MAT.html "Point Sprite MAT") - special material for use with Point Sprite geometry type. The [Particle SOP](Particle_SOP.html "Particle SOP") can create point sprites.
## Using MATs[[edit](https://docs.derivative.ca/index.php?title=MAT&action=edit&section=1 "Edit section: Using MATs")]
* for Materials to texture geometry with, Phong MAT, GLSL MAT
* setup for materials (normals, uvs, where to apply, lighting and rendering)
* examples of applying a material, example of Rim Lighting, example of shadows
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Retrieved from "<https://docs.derivative.ca/index.php?title=MAT&oldid=27079>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [MATs](Category_MATs.html "Category:MATs")