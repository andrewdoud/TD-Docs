

CHOP to SOP - TouchDesigner Documentation




# CHOP to SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The CHOP to SOP takes CHOP channels and generates 3D polygons in a SOP. It reads sample data from a [CHOP](CHOP.html "CHOP") and converts it into point positions and point attributes. This makes it complementary to the [SOP to CHOP](SOP_to_CHOP.html "SOP to CHOP"). The Channels created by the [SOP to CHOP](SOP_to_CHOP.html "SOP to CHOP") can be modified and then re-inserted into the SOP network via a CHOP to SOP.
By default, the SOP is a line from (`-1 0 0`) to (`1 0 0`) containing one point for every sample in the CHOP.
It matches the input channels to the Channel Scope (`tx ty tz`) where possible. If `tx` or `ty` or `tz` don’t match anything, it just uses the value from the default line, and it only shows a Warning.
The simplest thing to do is to send it a channel named `ty`, which will make a 3D curve that looks like the CHOP curve.
This does what a [Point SOP](Point_SOP.html "Point SOP") with a `op('wave1')['chan1'].eval(0)` function can do, but is much faster.
By using point groups from the incoming SOP, the channels can be inserted only into the group's points.
The CHOP to SOP also supports custom attributes. If the user maps a channel to an attribute that is not found, that attribute is added to the points. Currently, all custom attributes are floats and of size = 1.
In its default state it will attempt to replace the point positions (`P(0) P(1) P(2)`) with the channels named `tx ty` and `tz`.
The channel and attribute scope are first expanded into individual names and matched on a 1 to 1 basis. If you are filling P it doesn't matter if you specify `t[xyz]` or `tx ty tz`, both will replace `P(0) P(1) P(2)`, which can be collapsed to `P`.
For example: Add custom attributes "Scale", "Twist" or "Roll" to the backbone's points with a CHOP to SOP.
If you connect a SOP to its input, it will use the SOP as a starting geometry versus the default line.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[choptoSOP\_Class](https://docs.derivative.ca/ChoptoSOP_Class "ChoptoSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Operator Inputs](#Operator_Inputs)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Group `group` - Modify only the points within this point group. If blank, all points are modified. Accepts patterns, as described in: [Pattern Matching](Pattern_Matching.html "Pattern Matching").
CHOP `chop` - Specifies which CHOP Network / CHOP contains the sample data to fetch.
Start Position `startpos` - ⊞ - Sets the bounds for positions that are not defined by a channel, ie. a channel is not set to one of the P attributes.
* X `startposx` -
* Y `startposy` -
* Z `startposz` -
End Position `endpos` - ⊞ - Sets the bounds for positions that are not defined by a channel, ie. a channel is not set to one of the P attributes.
* X `endposx` -
* Y `endposy` -
* Z `endposz` -
  

Channel Scope `chanscope` - The names to use to modify the attributes.
Attribute Scope `attscope` - A string list of attributes to modify in the SOP. List of Common Attributes:
* `P` - Point position (X, Y, Z) - 3 values
* `Pw` - Point weight - 1 value
* `Cd` - Point color (red, green, blue, alpha) - 4 values
* `N` - Point normal (X, Y, Z) - 3 values
* `uv` - Point texture coordinates (U, V, W) - 3 values
See [Attributes](https://docs.derivative.ca/index.php?title=Attributes&action=edit&redlink=1 "Attributes (page does not exist)") for a complete listing of attributes.

Organize by Attribute `organize` - Instead of using the point index, use the value of this attribute as the index to use when looking up into the CHOP.
Mapping `mapping` - ⊞ - Determines how the CHOP samples are mapped to the geometry points.
* One Sample to Each Point `onetoone` - The samples are simply mapped 1-to-1, each sample is mapped to the next point in order.
* Resample CHOP to Fit SOP `scale` - If there are more or less CHOP samples than points in the geometry, then the CHOP channels are resampled to interpolate values for all the geometry points.
Compute Normals `compnml` - Creates normals on the geometry.
Compute Tangents `comptang` - Creates tangents on the geometry.
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the CHOP to SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditor2022.241402021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • CHOP to• [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Experimental:POP to](https://docs.derivative.ca/Experimental:POP_to_SOP "Experimental:POP to SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=CHOP_to_SOP&oldid=33485>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")