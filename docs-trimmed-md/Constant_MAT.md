

# Constant_MAT

Constant MAT - TouchDesigner Documentation




# Constant MAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Constant MAT renders a constant color on a material.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[constantMAT\_Class](https://docs.derivative.ca/ConstantMAT_Class "ConstantMAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Constant Page](#Parameters_-_Constant_Page)
* [3 Parameters - Deform Page](#Parameters_-_Deform_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
  + [4.1 Blending](#Blending)
  + [4.2 Depth Test](#Depth_Test)
  + [4.3 Alpha Test](#Alpha_Test)
  + [4.4 Wire Frame](#Wire_Frame)
  + [4.5 Cull Face](#Cull_Face)
  + [4.6 Polygon Depth Offset](#Polygon_Depth_Offset)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common MAT Info Channels](#Common_MAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Constant Page
Apply Projection Maps `applyprojmaps` - The projection map texture color from a [Light COMP](Light_COMP.html "Light COMP") will be applied to the object as well. This allows for applying a projection map without affecting the projection map's color with any lighting.
Color `color` - ⊞ - The color of the light reflected from the material.
* Red `colorr` -
* Green `colorg` -
* Blue `colorb` -
Alpha `alpha` - The opacity of the material. This parameter is multiplied by point alpha of the object.
Apply Point Color `applypointcolor` - Multiplies the color by the geometry's point color values.
Color Map `colormap` - ⊞ - Provides a TOP texture to use as a color map.
Extend U `colormapextendu` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Extend V `colormapextendv` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Extend W `colormapextendw` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Filter `colormapfilter` - ⊞ -
* Nearest `nearest` -
* Linear `linear` -
* Mipmap Linear `mipmaplinear` -
Anisotropic Filter `colormapanisotropy` - ⊞ -
* Off `off` -
* 2x `2x` -
* 4x `4x` -
* 8x `8x` -
* 16x `16x` -
Texture Coord `colormapcoord` - ⊞ -
* Texture Layer 0 (uv[0-2]) `uv0` -
* Texture Layer 1 (uv[3-5]) `uv1` -
* Texture Layer 2 (uv[6-8]) `uv2` -
* Texture Layer 3 (uv[9-11]) `uv3` -
* Texture Layer 4 (uv[12-14]) `uv4` -
* Texture Layer 5 (uv[15-17]) `uv5` -
* Texture Layer 6 (uv[18-20]) `uv6` -
* Texture Layer 7 (uv[21-23]) `uv7` -
* Screen Space Coordinates `screenspace` -
Coord Interpolation `colormapcoordinterp` - ⊞ -
* Perspective Correct `perspectivecorrect` -
* Linear (noperspective) `linear` -
  

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
Extra Information for the Constant MAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
| MATs |
| --- |
| Constant• [Depth](Depth_MAT.html "Depth MAT") • [GLSL](GLSL_MAT.html "GLSL MAT") • [In](https://docs.derivative.ca/In_MAT "In MAT") • [Line](Line_MAT.html "Line MAT") • [MAT](MAT.html "MAT") • [Experimental:MAT](Experimental_MAT.html "Experimental:MAT") • [MAT Common Page](https://docs.derivative.ca/MAT_Common_Page "MAT Common Page") • [Null](https://docs.derivative.ca/Null_MAT "Null MAT") • [Out](https://docs.derivative.ca/Out_MAT "Out MAT") • [PBR](PBR_MAT.html "PBR MAT") • [Phong](Phong_MAT.html "Phong MAT") • [Point Sprite](Point_Sprite_MAT.html "Point Sprite MAT") • [Experimental:Point Sprite](https://docs.derivative.ca/Experimental:Point_Sprite_MAT "Experimental:Point Sprite MAT") • [Select](https://docs.derivative.ca/Select_MAT "Select MAT") • [Switch](https://docs.derivative.ca/Switch_MAT "Switch MAT") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Wireframe](https://docs.derivative.ca/Wireframe_MAT "Wireframe MAT") |
MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The OpenGL (pre-2022) or Vulkan (2022-) code that runs on the GPU and creates rendered images from polygons and textures. A shader is programmed in [Text DATs](Text_DAT.html "Text DAT") and referenced by a [GLSL Material](GLSL_MAT.html "GLSL MAT") or a [GLSL TOP](GLSL_TOP.html "GLSL TOP"). Shaders are composed of up to three parts: Vertex Shader, Pixel Shader and Compute Shader.

The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).

The connection of an output of one node to the input of another node in a network. In contrast, see [Link](Link.html "Link").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Constant_MAT&oldid=31301>"
[Category](Special_Categories.html "Special:Categories"):
* [MATs](Category_MATs.html "Category:MATs")