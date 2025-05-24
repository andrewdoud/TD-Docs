

# Copy_SOP

TouchDesigner Documentation




# Copy SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Copy SOP lets you make copies of the geometry of other SOPs and apply a transformation to each copy.
It also allows you to copy geometry to points on an input template.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[copySOP\_Class](https://docs.derivative.ca/CopySOP_Class "CopySOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Copy Page](#Parameters_-_Copy_Page)
* [3 Parameters - Stamp Page](#Parameters_-_Stamp_Page)
* [4 Parameters - Attributes Page](#Parameters_-_Attributes_Page)
* [5 Tips](#Tips)
* [6 Examples](#Examples)
  + [6.1 Creating Stamped Geometry](#Creating_Stamped_Geometry)
* [7 Operator Inputs](#Operator_Inputs)
* [8 Info CHOP Channels](#Info_CHOP_Channels)
  + [8.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [8.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Copy Page
Specifies a subset of template primitives from which to copy onto. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Source Group `sourcegrp` - Specifies a subset of input primitives to copy from. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Template Group `templategrp` - Specifies a subset of template primitives from which to copy onto. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Number of Copies `ncy` - Sets number of Copies to be made of the source. For a template input, it specifies the number of copies to be placed at each point of the template.
Primitives per Point `nprims` - Defines how many primitives to copy from each point.
Rotate to Normal `nml` - Only used when a template input is specified. If the template is a sphere, and the first input is a circle, a circle is placed at each point of the sphere. With this option on, all the circles will re-orient to face the surface of the sphere (a default sphere has normals radiating outwards from the center).
If an up attribute exists on the template geometry, then this will be used (along with the normal) to fully define the rotates for the copies. An up attribute is created with the Point SOP.

Transform Cumulative `cum` - Each transformation "builds" on the location left by the one before it. Transformations are cumulative as the Copy SOP produces new copies.
Transform Order `xord` - ⊞ - Sets the overall transform order for the transformations. The Transform Order determines the order in which transformations take place. Depending on the order, you can achieve different results using the exact same values. Choose the appropriate order from the menu.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `rord` - ⊞ - Sets the order of the rotations within the overall transform order.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Translate `t` - ⊞ - These allow you to specify the Translation (how much it moves over in a given direction), Rotation, and the Scale between each copy. Three columns are given for X, Y, and Z coordinates. Guide geometry is provided for the Pivot's translations. The Pivot is represented by a single red dot in the Viewport. Changing the Pivot parameters moves this point of reference.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - These allow you to specify the Translation (how much it moves over in a given direction), Rotation, and the Scale between each copy. Three columns are given for X, Y, and Z coordinates. Guide geometry is provided for the Pivot's translations. The Pivot is represented by a single red dot in the Viewport. Changing the Pivot parameters moves this point of reference.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `s` - ⊞ - These allow you to specify the Translation (how much it moves over in a given direction), Rotation, and the Scale between each copy. Three columns are given for X, Y, and Z coordinates. Guide geometry is provided for the Pivot's translations. The Pivot is represented by a single red dot in the Viewport. Changing the Pivot parameters moves this point of reference.
* X `sx` -
* Y `sy` -
* Z `sz` -
Pivot `p` - ⊞ - These allow you to specify the Translation (how much it moves over in a given direction), Rotation, and the Scale between each copy. Three columns are given for X, Y, and Z coordinates. Guide geometry is provided for the Pivot's translations. The Pivot is represented by a single red dot in the Viewport. Changing the Pivot parameters moves this point of reference.
* X `px` -
* Y `py` -
* Z `pz` -
Uniform Scale `scale` - Uniform Scale allows you to shrink or enlarge geometry along all three axes simultaneously.
Normals Maintain Length `vlength` - Vector type attributes (i.e. normals, velocity) maintain the same length under transforms. i.e. When geometry is scaled, the normals remain constant in length.
Create Output Groups `newg` - If selected, this creates a group for each copy number, and places each primitive created at that stage into it.
Copy Groups `copyg` - Defines the base name of the groups created.
Look At `lookat` - Orients the copied geometry to lookat, or point to, the [object](Object.html "Object") component specified in the parameter.
Up Vector `upvector` - ⊞ - When specifying a Look At, it is possible to specify an up vector for the lookat. Without using an up vector, it is possible to get poor animation when the lookat object passes through the Y axis of the target object.
* X `upvectorx` -
* Y `upvectory` -
* Z `upvectorz` -
  

## Parameters - Stamp Page
Stamping is allowed in any parameter in TouchDesigner. The only requirement is that the stamped parameter is upstream in some fashion from the Copy SOP doing the stamping.
Stamp Inputs `stamp` - When enabled, it will Stamp proceeding variables for each input copied.
Copy `copy` - Sequence of stamp variables
Param `copy0param` - Token of each stamp variable. Stamped parameters are accessible via the global `fetchStamp()` method in the [td Module](Td_Module.html "Td Module") in python, or `param()` in tscript. See the example, below.
Value `copy0value` - Value of each stamp variable. Stamped parameters are accessible via the global `fetchStamp()` method in the [td Module](Td_Module.html "Td Module") in python, or `param()` in tscript. See the example, below.
  

## Parameters - Attributes Page
This page allows you to determine how point attributes on template geometry affect attributes on the source geometry. The template attribute can modify the source in four ways:
* Set - Override the source attribute.
* Multiply - Multiply the source attribute.
* Add - Get Added to the source attribute.
* Sub - Get Subtracted from the source attribute.
The template point attributes are able to affect point, primitive, or vertex attributes in the source geometry simply by entering values in the appropriate fields.
Use Template Point Attribs `doattr` - Enables the parameters below to allow template point attributes to be applied to the copied source geometry.
Copy to Point `setpt` - ⊞ - Copy the attributes to the source geometry's points.
* \* `*` -
Copy to Primitive `setprim` - ⊞ - Copy the attributes to the source geometry's primitives.
* \* `*` -
Copy to Vertex `setvtx` - ⊞ - Copy the attributes to the source geometry's vertices.
* \* `*` -
Multiply Point `mulpt` - ⊞ - Multiply the attributes with the source geometry's point attributes.
* \* `*` -
Multiply Primitive `mulprim` - ⊞ - Multiply the attributes with the source geometry's primitive attributes.
* \* `*` -
Multiply Vertex `mulvtx` - ⊞ - Multiply the attributes with the source geometry's vertex attributes.
* \* `*` -
Add Point `addpt` - ⊞ - Add the attributes to the source geometry's point attributes.
* \* `*` -
Add Primitive `addprim` - ⊞ - Add the attributes to the source geometry's primitive attributes.
* \* `*` -
Add Vertex `addvtx` - ⊞ - Add the attributes to the source geometry's vertex attributes.
* \* `*` -
Subtract Point `subpt` - ⊞ - Subtract the attributes from the source geometry's point attributes.
* \* `*` -
Subtract Primitive `subprim` - ⊞ - Subtract the attributes from the source geometry's primitive attributes.
* \* `*` -
Subtract Vertex `subvtx` - ⊞ - Subtract the attributes from the source geometry's vertex attributes.
* \* `*` -
  

## Tips
You can use the `me.copyTotal` python member to calculate the degrees of rotation for a given number of copies. For example, if you have 28 copies, you can set the rotation to be: `360/me.copyTotal` - this would automatically give you 12.8571 degrees, evenly spacing your 28 copies around the full circumference of the circle.
Using a Particle SOP as the Template object, you can copy objects defined in the Copy Data input to each particle template. This allows you, for example, to copy a Bee to each particle to create a swarm of bees.
Make a series of copies about an axis, and skin them to achieve lathe-like effects, similar to the results achieved with the Revolve SOP.
  

## Examples
### Creating Stamped Geometry
1. Place a Circle SOP, and set its type to Polygon.
2. Set the number of Divisions in the Circle to: `fetchStamp("sides",3)` The method `fetchStamp()` returns the value of the global parameter sides. If it is not yet defined it will return a value of 3.
3. Append a Copy SOP, and set the Number of Copies to `5`; and set Translate X to: `2.5` .
4. In the Stamp page of the Copy SOP, turn on Stamp Inputs. Set Param 1 to: `sides` and `me.copyIndex+3`[![CopySOPStampPage.png](https://docs.derivative.ca/images/d/d9/CopySOPStampPage.png)](https://docs.derivative.ca/File:CopySOPStampPage.png)
5. This creates a triangle on the first stamped copy; a square on the next; a pentagon on the third, and so on. The geometry for each copy is cooked separately.
[![CopySOPStampExample.png](https://docs.derivative.ca/images/0/02/CopySOPStampExample.png)](https://docs.derivative.ca/File:CopySOPStampExample.png)
You can set multiple stamp Params at once and they can be used anywhere in the ancestry of the copy's input.
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Copy SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditor2022.241402021.100002020.200002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • Copy• [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Copy_SOP&oldid=32298>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")