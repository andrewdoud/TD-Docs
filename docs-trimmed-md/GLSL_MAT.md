

GLSL MAT - TouchDesigner Documentation





























# GLSL MAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The GLSL MAT allows you to write or import custom materials into TouchDesigner. When there are compile errors in a GLSL [shader](Shader.html "Shader"), a blue/red checkerboard *error* shader will be displayed.

For more information on writing a shader, see [Write a GLSL Material](Write_a_GLSL_Material.html "Write a GLSL Material"), and the [GLSL Category](Category_GLSL.html "Category:GLSL").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[glslMAT\_Class](https://docs.derivative.ca/GlslMAT_Class "GlslMAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Load Page](#Parameters_-_Load_Page)
* [3 Parameters - Attributes Page](#Parameters_-_Attributes_Page)
* [4 Parameters - Samplers Page](#Parameters_-_Samplers_Page)
* [5 Parameters - Vectors Page](#Parameters_-_Vectors_Page)
* [6 Parameters - Arrays Page](#Parameters_-_Arrays_Page)
* [7 Parameters - Matrices Page](#Parameters_-_Matrices_Page)
* [8 Parameters - Constants Page](#Parameters_-_Constants_Page)
* [9 Parameters - Deform Page](#Parameters_-_Deform_Page)
* [10 Parameters - Common Page](#Parameters_-_Common_Page)
  + [10.1 Blending](#Blending)
  + [10.2 Depth Test](#Depth_Test)
  + [10.3 Alpha Test](#Alpha_Test)
  + [10.4 Wire Frame](#Wire_Frame)
  + [10.5 Cull Face](#Cull_Face)
  + [10.6 Polygon Depth Offset](#Polygon_Depth_Offset)
* [11 Info CHOP Channels](#Info_CHOP_Channels)
  + [11.1 Common MAT Info Channels](#Common_MAT_Info_Channels)
  + [11.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Load Page

GLSL Version `glslversion` - ⊞ - Pick what version of GLSL to compile the shader with.

* 1.20 `glsl120` -

* 3.30 `glsl330` -

* 4.00 `glsl400` -

* 4.10 `glsl410` -

* 4.20 `glsl420` -

* 4.30 `glsl430` -

* 4.40 `glsl440` -

* 4.50 `glsl450` -

* 4.60 `glsl460` -

Preprocess Directives `predat` - Use this DAT to place preprocessor directives at the start of your shader, such as #extension. This is required since these need to be the first lines in the shader, and TouchDesigner will be adding code to the start of your shader to declare uniforms/functions which would appear before #extension directives located in the main shader.
Vertex Shader `vdat` - Path to the DAT that holds the vertex shader code.
Pixel Shader `pdat` - Path to the DAT that holds the pixel shader code.
Load Uniform Names `loaduniformnames` - This will read all the declared (and used) uniforms in the compiled GLSL shader, and fill in the various name fields for the uniform parameters.
Clear Uniform Names `clearuniformnames` - This will clear all of the name fields for the uniform parameters.
Geometry Shader `gdat` - Path to the DAT that holds the geometry shader code.
Inherit Uniforms/Samplers from `inherit` - This Material will inherit all of the Textures and Uniforms from the GLSL Material referenced in this parameter.
Lighting Space `lightingspace` - ⊞ - Allows lighting space switch from the current default World Space to legacy Camera Space which was used for TouchDesigner 088.

* World Space `worldspace` -

* Camera Space (Legacy 088 shaders) `cameraspace` -

Input Primitive Type `inprim` - ⊞ - The type of geometry that will be inputed into the Geometry Shader.

* Points `points` -

* Lines `lines` -

* Triangles `triangles` -

Output Primitive Type `outprim` - ⊞ - The type of geometry that the Geometry Shader will output.

* Points `points` -

* Line Strip `linestrip` -

* Triangle Strip `tristrip` -

Num Output Vertices `numout` - The maximum number of vertices the Geometry Shader will output.
Two Sided Coloring `twocolor` - Enables support for two-sided coloring. When this is enabled the Vertex and/or Geometry shader can write to gl\_FrontColor, gl\_BackColor, gl\_FrontSecondaryColor and gl\_BackSecondaryColor and the correct color will be placed into gl\_Color and gl\_SecondaryColor in the Pixel shader depending on if the primitive's front face or back face is facing the camera. When this is disabled the values placed into gl\_FrontColor and gl\_FrontSecondaryColor are passed to gl\_Color and gl\_SecondaryColor regardless of which side of the primitive is facing the camera.

  


## Parameters - Attributes Page

Attribute `attr` - A sequence of attributes that should be made accesible in the shader. In the past these would be manually declared inside the shader, but to add support for POP based workflows, they need to be setup via these parameters instead. You can access the shaders using `TDAttrib_<attribName>()`.
Name `attr0name` - The name to give the attribute.
Type `attr0type` - ⊞ - The type, both vector size as well as if it's a float, double (d), integer (i), or unsigned integer (u).

* float `float` -

* vec2 `vec2` -

* vec3 `vec3` -

* vec4 `vec4` -

* double `double` -

* dvec2 `dvec2` -

* dvec3 `dvec3` -

* dvec4 `dvec4` -

* int `int` -

* ivec2 `ivec2` -

* ivec3 `ivec3` -

* ivec4 `ivec4` -

* uint `uint` -

* uvec2 `uvec2` -

* uvec3 `uvec3` -

* uvec4 `uvec4` -

Array Size `attr0size` - The size of the array. Currently a Size == 1 means it's not an array.

  


## Parameters - Samplers Page

Sampler `sampler` - Sequence of samplers for use in the shader
Name `sampler0name` - This is the sampler name that the GLSL program will use to sample from this TOP. The samplers need to be declared at the same dimentions as the TOP (sampler2D for a 2D TOP, sampler3D for 3D TOP).
TOP `sampler0top` - ⊞ - This is the TOP that will be referenced by the above sampler name above it.

**Exposed by the + Button, texture sampling parameters**:

Refer to the [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") article for more information on the parameters exposed by pressing the + button. The *parameter* prefix for each of the parameters is *top[digit]*.

Extend U `sampler0extendu` - ⊞ -

* Hold `hold` -

* Zero `zero` -

* Repeat `repeat` -

* Mirror `mirror` -

Extend V `sampler0extendv` - ⊞ -

* Hold `hold` -

* Zero `zero` -

* Repeat `repeat` -

* Mirror `mirror` -

Extend W `sampler0extendw` - ⊞ -

* Hold `hold` -

* Zero `zero` -

* Repeat `repeat` -

* Mirror `mirror` -

Filter `sampler0filter` - ⊞ -

* Nearest `nearest` -

* Linear `linear` -

* Mipmap Linear `mipmaplinear` -

Anisotropic Filter `sampler0anisotropy` - ⊞ -

* Off `off` -

* 2x `2x` -

* 4x `4x` -

* 8x `8x` -

* 16x `16x` -



  


## Parameters - Vectors Page

Vector `vec` - Sequence of vectors to be used as uniforms
Name `vec0name` - The name of the vector.
Value `vec0value` - ⊞ - The value to assign to the uniform. If the uniform is a float the first entry of the four is used, if the uniform is a vec2 the first two entries are used, etc.

* Value `vec0valuex` -

* Value `vec0valuey` -

* Value `vec0valuez` -

* Value `vec0valuew` -


  


## Parameters - Arrays Page

CHOP Uniforms allow you to send CHOP channel data into a GLSL shader as an array. Depending on the array type used, the number of values you can send into the shader may be limited. If you are using Uniform Arrays, you can use the Built-In variable $SYS\_GFX\_GLSL\_MAX\_UNIFORMS to get an idea of how many values you can pass to the shader. Current GPUs are vec4 based for uniform arrays, so the maximum array size is $SYS\_GFX\_GLSL\_MAX\_UNIFORMS / 4. Other uniforms will take away from this maximum.
If you are using Texture Buffers the maximum array size is far bigger, $SYS\_GFX\_MAX\_TEXTURE\_BUFFER\_SIZE will tell you the max for this. The max for texture buffer is per texture buffer, and having multiple texture buffers does not take away from the max for each array.

Name `array` - Sequence of arrays to be used as uniforms
Array `array` - Sequence of arrays to be used as uniforms

  


## Parameters - Matrices Page

Relative Xforms are matrices that will transform points and vectors from one space to another space.

Matrix `matrix` - Sequence of matrices to be used as uniforms
Name `matrix0name` - The name of the uniform. The uniform should be declared as a mat4.
Matrix `matrix0value` - The value to assign the matrix. For valid ways to specify this, see the [Matrix Parameters](Matrix_Parameters.html "Matrix Parameters") article.


Relative `rel` - A sequence of relative transforms. The transform is the relative transform one Object COMP to another.
Name `rel0name` - The name of the uniform. The uniform should be declared as a mat4.
Xform from `rel0from` - Transform from this COMPs world transform.
To `rel0to` - Transform to this COMPs world transform.

  


## Parameters - Constants Page

[Specialization Constants](Write_a_GLSL_Material.html#Specialization_Constants "Write a GLSL Material") can optionally have their values assigned here.

Constant `const` - Sequence of constant uniforms.
Name `const0name` - The constant name, as declared in the shader.
Value `const0value` - The value to give the constant.

  


## Parameters - Deform Page

Refer to the  [Deform Article](Deforming_Geometry_(Skinning).html "Deforming Geometry (Skinning)") for more information on doing deforms in TouchDesigner.

Deform `dodeform` - Enables deforms on this material.
Get Bone Data: `deformdata` - ⊞ - Specifies where the deform bone data will be obtained.

* From a SOP `sop` -

* From another MAT `mat` -

* From a DeformIn MAT `deformin` -

SOP with Capture Data `targetsop` - Specifies the SOP that contains the deform capture attributes.
pCaptPath Attrib `pcaptpath` - Specifies the name of the pCaptPath attribute to use. When your geometry has been put through a [Bone Group SOP](Bone_Group_SOP.html "Bone Group SOP"), the attributes will be split into names like pCaptPath0, pCaptPath1. You can only render 1 bone group at a time, so this should match the group you are rendering with this material.
pCaptData Attrib `pcaptdata` - Much like pCaptPath Attrib.
Skeleton Root Path `skelrootpath` - Specifies the path to the COMP where the root of the skeleton is located.
MAT `mat` - When obtaining deform data from a MAT or a Deform In MAT, this is where that MAT is specified.

  


## Parameters - Common Page

### Blending

[Blending](Blending.html "Blending") is summing the color value of the pixel being drawn and the pixel currently present in the Color-Buffer. Blending is typically used to simulate [Transparency](Transparency.html "Transparency").
The blending equation is:
`Final Pixel Value = (Source Blend * Source Color) + (Dest Blend * Destination Color)`

  


Blending (Transparency) `blending` - This toggle enables and disables blending. However see the wiki article [Transparency](Transparency.html "Transparency").
Blend Operation `blendop` - ⊞ -

* Add `add` -

* Subtract `subtract` -

* Reverse Subtract `revsubtract` -

* Minimum `minimum` -

* Maximum `maximum` -

Source Color \* `srcblend` - ⊞ - This value is multiplied by the color value of the pixel that is being written to the Color-Buffer (also know as the Source Color).

* Zero `zero` -

* Dest Color `dcol` -

* One Minus Dest Color `omdcol` -

* Source Alpha `sa` -

* One Minus Source Alpha `omsa` -

* Dest Alpha `da` -

* One Minus Dest Alpha `omda` -

* Source Alpha Saturate `sas` -

* One `one` -

* Constant Color `constantcol` -

* One Minus Constant Color `omconstantcol` -

* Constant Alpha `constanta` -

* One Minus Constant Alpha `omconstanta` -

Destination Color \* `destblend` - ⊞ - This value is multiplied by the color value of the pixel currently in the Color-Buffer (also known as the Destination Color).

* One `one` -

* Src Color `scol` -

* One Minus Src Color `omscol` -

* Source Alpha `sa` -

* One Minus Source Alpha `omsa` -

* Dest Alpha `da` -

* One Minus Dest Alpha `omda` -

* Zero `zero` -

* Dest Color `dcol` -

* One Minus Dest Color `omdcol` -

* Source Alpha Saturate `sas` -

* Constant Color `constantcol` -

* One Minus Constant Color `omconstantcol` -

* Constant Alpha `constanta` -

* One Minus Constant Alpha `omconstanta` -

Separate Alpha Function `separatealphafunc` - This toggle enables and disables separate blending options for the alpha values.
Alpha Blend Operation `blendopa` - ⊞ -

* Add `add` -

* Subtract `subtract` -

* Reverse Subtract `revsubtract` -

* Minimum `minimum` -

* Maximum `maximum` -

Source Alpha \* `srcblenda` - ⊞ - This value is multiplied by the alpha value of the pixel that is being written to the Color-Buffer (also know as the Source Alpha).

* Zero `zero` -

* Dest Color `dcol` -

* One Minus Dest Color `omdcol` -

* Source Alpha `sa` -

* One Minus Source Alpha `omsa` -

* Dest Alpha `da` -

* One Minus Dest Alpha `omda` -

* Source Alpha Saturate `sas` -

* One `one` -

* Constant Color `constantcol` -

* One Minus Constant Color `omconstantcol` -

* Constant Alpha `constanta` -

* One Minus Constant Alpha `omconstanta` -

Destination Alpha \* `destblenda` - ⊞ - This value is multiplied by the alpha value of the pixel currently in the Color-Buffer (also known as the Destination Alpha).

* One `one` -

* Src Color `scol` -

* One Minus Src Color `omscol` -

* Source Alpha `sa` -

* One Minus Source Alpha `omsa` -

* Dest Alpha `da` -

* One Minus Dest Alpha `omda` -

* Zero `zero` -

* Dest Color `dcol` -

* One Minus Dest Color `omdcol` -

* Source Alpha Saturate `sas` -

* Constant Color `constantcol` -

* One Minus Constant Color `omconstantcol` -

* Constant Alpha `constanta` -

* One Minus Constant Alpha `omconstanta` -

Blend Constant Color `blendconstant` - ⊞ -

* Blend Constant Color `blendconstantr` -

* Blend Constant Color `blendconstantg` -

* Blend Constant Color `blendconstantb` -

Blend Constant Alpha `blendconstanta` -
Legacy Alpha Behavior `legacyalphabehavior` -
Post-Mult Color by Alpha `postmultalpha` - Multiplies the color by alpha after all other operations have taken place.
Point Color Pre-Multiply `pointcolorpremult` - ⊞ -

* Already Pre-Multiplied By Alpha `alreadypremult` -

* Pre-Multiply By Alpha in Shader `premultinshader` -

Depth Test `depthtest` - Enables and disables the Depth-Test. If the depth-test is disabled, depths values aren't written to the Depth-Buffer.
Depth Test Function `depthfunc` - ⊞ - The depth value of the pixel being drawn is compared to the depth value currently in the depth-buffer using this function. If the test passes then the pixel is drawn to the Frame-Buffer. If the test fails the pixel is discarded and no changes are made to the Frame-Buffer.

* Less Than `less` -

* Less Than or Equal `lessorequal` -

* Equal `equal` -

* Greater Than `greater` -

* Greater Than or Equal `greaterorequal` -

* Not Equal `notequal` -

* Always `always` -
### Depth Test

Depth-Testing is comparing the depth value of the pixel being drawn with the pixel currently in the [Frame-Buffer](https://docs.derivative.ca/index.php?title=Frame-Buffer&action=edit&redlink=1 "Frame-Buffer (page does not exist)"). A pixel that is determined to be in-front of the pixel currently in the Frame-Buffer will be drawn over it. Pixels that are determined to be behind the pixel currently in the Frame-Buffer will not be drawn. Depth-Testing allows geometry in a 3D scene to occlude geometry behind it, and be occluded by geometry in-front of it regardless of the order the geometry was drawn.

For a more detailed description of Depth-Testing, refer to the [Depth-Test](https://docs.derivative.ca/Depth-Test "Depth-Test") article.

  


Write Depth Values `depthwriting` - If Write Depth Values is on, pixels that pass the depth-test will write their depth value to the Depth-Buffer. If this isn't on then no changes will be made to the Depth-Buffer, regardless of if the pixels drawn pass or fail the depth-test.
Discard Pixels Based on Alpha `alphatest` - This enables or disables the pixel alpha test.
Keep Pixels with Alpha `alphafunc` - ⊞ - This menu works in conjunction with the Alpha Threshold parameter below in determining which pixels to keep based on their alpha value.

* Less Than `less` -

* Less Than or Equal `lessorequal` -

* Greater Than `greater` -

* Greater Than or Equal `greaterorequal` -

Alpha Threshold `alphathreshold` - This value is what the pixel's alpha is compared to to determine if the pixel should be drawn. Pixels with alpha greater than the Alpha Threshold will be drawn. Pixels with alpha less than or equal to the Alpha Threshold will not be drawn.
Wire Frame `wireframe` - ⊞ - Enables and disables wire-frame rendering with the option of OpenGL Tesselated or Topology based wireframes.

* Off `off` -

* OpenGL Tesselated Wire Frame `tesselated` -

* Topology Wire Frame `topology` -
### Alpha Test

Alpha-testing allows you to choose to draw or not draw a pixel based on its alpha value.

  


Line Width `wirewidth` - This value is the width that the wires will be. This value is in pixels.
Cull Face `cullface` - ⊞ - Selects which faces to render.

* Use Render Setting `userender` - Use the render settings found in the Render or Render Pass TOP.

* Neither `neither` - Do not cull any faces, render everything.

* Back Faces `backfaces` - Cull back faces, render front faces.

* Front Faces `frontfaces` - Cull front faces, render back faces.

* Both Faces `bothfaces` - Cull both faces, render nothing.

Polygon Depth Offset `polygonoffset` - Turns on the polygon offset feature.
Offset Factor `polygonoffsetfactor` -
Offset Units `polygonoffsetunits` -
### Wire Frame

The wire-frame feature will render the geometry as wire-frame, using the actual primitive type used in the render. What this means is surfaces like Metaballs, NURBs and Beziers will become a wire-frame of the triangles/triangle-strips used to render them (since these types of primitives can't be natively rendered in OpenGL).

  


### Cull Face

The cull face parameter will cull faces from the render output. This can be used as an optimization or sometimes to remove artifacts. See [Back-Face Culling](https://docs.derivative.ca/Back-Face_Culling "Back-Face Culling") for more infomation.

  


### Polygon Depth Offset

This feature pushes the polygons back into space a tiny fraction. This is useful when you are rendering two polygons directly on-top of each other and are experiencing [Z-Fighting](Z-Fighting.html "Z-Fighting"). Refer to [Polygon Depth Offset](Polygon_Depth_Offset.html "Polygon Depth Offset") for more information. This is also an important feature when doing [shadows](Shadows.html "Shadows").

  


## Info CHOP Channels

Extra Information for the GLSL MAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


### Common MAT Info Channels

### Common Operator Info Channels

* total\_cooks - Number of times the operator has cooked since the process started.

* cook\_time - Duration of the last cook in milliseconds.

* cook\_frame - Frame number when this operator was last cooked relative to the component timeline.

* cook\_abs\_frame - Frame number when this operator was last cooked relative to the absolute time.

* cook\_start\_time - Time in milliseconds at which the operator started cooking in the frame it was cooked.

* cook\_end\_time - Time in milliseconds at which the operator finished cooking in the frame it was cooked.

* cooked\_this\_frame - 1 if operator was cooked this frame.

* warnings - Number of warnings in this operator if any.

* errors - Number of errors in this operator if any.

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002020.200002018.28070before 2018.28070

| MATs |
| --- |
| [Constant](Constant_MAT.html "Constant MAT") • [Depth](Depth_MAT.html "Depth MAT") • GLSL• [In](https://docs.derivative.ca/In_MAT "In MAT") • [Line](Line_MAT.html "Line MAT") • [MAT](MAT.html "MAT") • [Experimental:MAT](Experimental_MAT.html "Experimental:MAT") • [MAT Common Page](https://docs.derivative.ca/MAT_Common_Page "MAT Common Page") • [Null](https://docs.derivative.ca/Null_MAT "Null MAT") • [Out](https://docs.derivative.ca/Out_MAT "Out MAT") • [PBR](PBR_MAT.html "PBR MAT") • [Phong](Phong_MAT.html "Phong MAT") • [Point Sprite](Point_Sprite_MAT.html "Point Sprite MAT") • [Experimental:Point Sprite](https://docs.derivative.ca/Experimental:Point_Sprite_MAT "Experimental:Point Sprite MAT") • [Select](https://docs.derivative.ca/Select_MAT "Select MAT") • [Switch](https://docs.derivative.ca/Switch_MAT "Switch MAT") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Wireframe](https://docs.derivative.ca/Wireframe_MAT "Wireframe MAT") |

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.


The OpenGL (pre-2022) or Vulkan (2022-) code that runs on the GPU and creates rendered images from polygons and textures. A shader is programmed in [Text DATs](Text_DAT.html "Text DAT") and referenced by a GLSL Material or a [GLSL TOP](GLSL_TOP.html "GLSL TOP"). Shaders are composed of up to three parts: Vertex Shader, Pixel Shader and Compute Shader.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.


A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").


A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.


Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).


The connection of an output of one node to the input of another node in a network. In contrast, see [Link](Link.html "Link").


A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.







Retrieved from "<https://docs.derivative.ca/index.php?title=GLSL_MAT&oldid=32285>"
[Category](Special_Categories.html "Special:Categories"):

* [MATs](Category_MATs.html "Category:MATs")