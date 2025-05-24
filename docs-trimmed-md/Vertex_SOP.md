

Vertex SOP - TouchDesigner Documentation




# Vertex SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Vertex SOP allows you to edit/create attributes on a per-vertex (rather than per-point) basis. It is similar to the [Point SOP](Point_SOP.html "Point SOP") in this respect. It supports two inputs, and will inherit the first input source by default. If the second input have less primitives than the first input, it will cycle through the primitives and match the vertices. If the primitive in the first input has more vertices than the matching primitive in the second input, the extra vertices are ignored.
There are currently three vertex attributes supported:
* Diffuse Color
* Alpha
* Texture Coordinates
When the attribute is defined, it can only occur on either points or vertices, but not both. Thus, if the input geometry has a point attribute for diffuse color, the attribute will automatically be "elevated" to be a vertex attribute (if diffuse colors are added in the Vertex SOP).
The SOP processes every vertex of every primitive. For each vertex processed, there are variables which allow you to know the:
* Vertex number of the primitive being processed
* The number of vertices in the primitive being processed
* The point which is referenced by the vertex
* The primitive which contains the vertex
* The total number of points
* The total number of primitives
There are also local variables to find out the values of some point attributes (i.e. position, normal - if they exist), in addition to vertex attributes. To access the attributes of the second input source, append a 2 to the variable.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[vertexSOP\_Class](https://docs.derivative.ca/VertexSOP_Class "VertexSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Vertex Page](#Parameters_-_Vertex_Page)
* [3 Parameters - Attributes Page](#Parameters_-_Attributes_Page)
* [4 Examples](#Examples)
  + [4.1 Texture Offsets](#Texture_Offsets)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Vertex Page
Group `group` - If there are input groups, specifying a group name in this field will cause this `SOP` to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Color `doclr` - ⊞ - Select between keeping the color, adding new color, or using no color for vertex color attributes from incoming geometry.
* Keep Color `off` -
* Add Color `on` -
* No Color `remove` -
Color `diff` - ⊞ - If you select 'Add Color' from the menu above, Cd color vertex attributes will be added/modified in the SOP. Enter expressions below to control the values of the point colors. The attributes to modify are: `me.inputColor[0]` for red, `me.inputColor[1]` for green, `me.inputColor[2]` for blue, and `me.inputColor[3]` for alpha. If you select 'No Color' from the menu above, the Cd color vertex attribute will be removed from the SOP.
* Color `diffr` -
* Color `diffg` -
* Color `diffb` -
Alpha `alpha` - Control the alpha attribute in the same manner as the rgb colors above. Alpha is Cd[3] and comes from input via `me.inputColor[3]`
Texture `douvw` - ⊞ - Select between keeping the texture coordinates, adding new texture coordinates, or using no texture coordinates for the vertex texture attributes from incoming geometry.
* Keep Texture `off` -
* Add Texture `on` -
* No Texture `remove` -
Texture `map` - ⊞ - If you select 'Add Texture' from the menu above, uv texture coordinate vertex attributes will be added/modified in the SOP. Enter expressions here to control the values of the vertex texture coordinates here. The attributes to modify are: `me.inputTexture[0]`, `me.inputTexture[1]` and `me.inputTexture[2]`. If you select 'No Texture' from the menu above, the uv texture coordinates vertex attribute will be removed from the SOP.
* Texture `mapu` -
* Texture `mapv` -
* Texture `mapw` -
Crease `docrease` - ⊞ - Select between keeping the crease, adding new crease, or using no crease for creaseweight attribute from incoming geometry.
The `Crease Weight` attribute can be used to set individual edge crease weights for sub-division surfaces (see [Subdivide SOP](Subdivide_SOP.html "Subdivide SOP") ). This vertex attribute defines the weight for the edge which goes from that vertex to the next vertex in the polygon. For example, with a triangle (which has vertices 0, 1, 2), the attribute for vertex 1 defines the crease weight for the edge (1, 2). The attribute for vertex 2 defines the crease weight for edge (2, 0). The crease weight should be greater than 0. The larger the value for crease weights, the sharper the edge will be when sub-divided.
Crease attributes can be visualized by passing them into a [Subdivide SOP](Subdivide_SOP.html "Subdivide SOP").
* Keep Crease `off` -
* Add Crease `on` -
* No Crease `remove` -
Crease `crease` - If you select 'Add Crease' from the menu above, enter expressions here to control the values of the creaseweights here. The attribute to modify is: me.inputVertex.creaseWeight[0]. Values for the weight of the vertex can range from 0.0001 to infinity.
  

## Parameters - Attributes Page
Custom Attribute `attr` - Sequence of custom attributes to be added to the geometry created.
Name `attr0name` - Creates a custom attribute with this name.
Type `attr0type` - ⊞ - The type of attribute created can be selected from this menu.
* float `float` -
* vec2 `vec2` -
* vec3 `vec3` -
* vec4 `vec4` -
* int `int` -
* ivec2 `ivec2` -
* ivec3 `ivec3` -
* ivec4 `ivec4` -
Value `attr0value` - ⊞ - Set the values of the Custom Attrib using these parameters.
* Value `attr0value1` -
* Value `attr0value2` -
* Value `attr0value3` -
* Value `attr0value4` -

  

## Examples
### Texture Offsets
You can have set of images in a TOP, and apply all of them in one material to different parts of an object. This allows you to have a pre-rendered animation clip with the clip playing at different speeds and time offsets on different surfaces.
You can adjust the material frame time by the first vertex/point texture W component (texture coordinated are U (horizontal), V (vertical) and W (one of a set of texture images). A texture (W) value of -1 moves back in time 1 frame. This lets you apply different frames to many polygons simultaneously using the Vertex SOP, or [Point SOP](Point_SOP.html "Point SOP").
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Vertex SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common SOP Info Channels
* num\_points - Number of points in this SOP.
* num\_prims - Number of primitives in this SOP.
* num\_particles - Number of particles in this SOP.
* last\_vbo\_update\_time - Time spent in another thread updating geometry data on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
* last\_meta\_vbo\_update\_time - Time spent in another thread updating meta surface geometry data (such as metaballs or nurbs) on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002020.200002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • Vertex• [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Vertex_SOP&oldid=32297>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")