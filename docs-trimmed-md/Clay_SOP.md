

Clay SOP - TouchDesigner Documentation




# Clay SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Clay SOP deforms faces and surfaces by pulling points that lie directly on them. As opposed to the Point SOP or other SOPs that manipulate control points (CVs), the Clay SOP operates on the primitive contours themselves, providing a direct, intuitive, and unconstrained way of reshaping geometry. Thus, rather than translating CVs to change the aspect of the primitive, the Clay SOP takes the inverse approach of manipulating the primitive's skin to reposition the CVs.
The point that defines the area to be modified is called a "target point" or "target" for short. It is expressed as a (u,v) pair in the parametric space of the primitive and ranges between 0 and 1 in both U and V. The image of the target point on the primitive is a 3D point which Clay can displace in several ways. Furthermore, if the primitive is a surface, there is are options to pull only the point or a whole isoparametric curve in either U or V.
Clay does not refine the faces and surfaces unless asked to, so the complexity of the geometry does not increase. The area affected by the change varies with each primitive type and topology. In all cases it is possible to reduce to amount of change by inserting a Refine SOP before the Clay SOP and inserting detail around the target point. For other ways to increase the locality of the deformation as well as its sharpness, see U and V Sharpness below.
If a second input is present, it is possible to snap the target (u,v) point to an (s,t) point on the first primitive of the second input. Without a second input, the primitives can be made to snap to themselves. Moreover, the Clay SOP is able to snap the target to arbitrary points in space.
Both this SOP and the Align SOP can be used effectively as snapping tools and building blocks for curve networks. The main difference between the two SOPs is that Clay deforms the inputs partially, while Align translates and/or rotates the whole primitive.
The Clay SOP accepts a mix of any combination of face and surface types.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[claySOP\_Class](https://docs.derivative.ca/ClaySOP_Class "ClaySOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Clay Page](#Parameters_-_Clay_Page)
* [3 Parameters - U Page](#Parameters_-_U_Page)
* [4 Parameters - V Page](#Parameters_-_V_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Clay Page
Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in Pattern Matching in the [Scripting Guide].
Warp Method `method` - ⊞ - The following describe the four types of transformations the Clay SOP can apply to the target (U, V) points or isoparametric curves (U or V). All the transformations are exclusive, and all reduce to a signed translation along a direction. The difference between the various transformations is the way the translation and the direction are specified.
* Matrix `mat` - The matrix method relocates the target point based on a transformation matrix. For a description of transforms, see the [Transform SOP](Transform_SOP.html "Transform SOP").
* Vector `vec` - The vector method provides a distance and a vector to translate along.
* Point `point` - The point method provides a 3D point in object space that the target point must snap to.
* Primitive `prim` - The primitive method allows the target point to be snapped to a point on another primitive. Any primitive type is allowed, including metaballs, all quadrics, and even particle systems. The point on the destination primitive is expressed parametrically as a (U, V) pair.
If the Clay SOP has a second input, then the destination primitive is going to be the first primitive in that input. If there is no second input, the primitives in the first input will snap to themselves (each face or surface to itself).

Transform Order `xord` - ⊞ - Sets the overall transform order for the transformations. The transform order determines the order in which transformations take place. Depending on the order, you can achieve different results using the exact same values. Choose the appropriate order from the menu.
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
Translate `t` - ⊞ - These three fields move the Source geometry in the three axes.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - These three fields rotate the Source geometry in the three axes.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `s` - ⊞ - These three fields scale the Source geometry in the three axes.
* X `sx` -
* Y `sy` -
* Z `sz` -
Pivot `p` - ⊞ - The pivot point for the transformations (not the same as the pivot point in the pivot channels). The pivot point parameters allow you to define the point about which geometry scales and rotates. Altering the pivot point produces different results depending on the transformation performed on the object.
For example, during a scaling operation, if the pivot point of an object is located at: `-1, -1, 0` and you wanted to scale the object by `0.5` (reduce its size by 50%) the object would scale toward the pivot point and appear to slide down and to the left.
[![TouchGeometry91.gif](https://docs.derivative.ca/images/b/bf/TouchGeometry91.gif)](https://docs.derivative.ca/File:TouchGeometry91.gif)
In the example above, rotations performed on an object with different pivot points produce very different results.
* X `px` -
* Y `py` -
* Z `pz` -
Distance `dist` - Specifies the translation distance along the given vector.
Normal `normal` - When On, the translation will be performed along the primitive normal at the target (U, V) point. Otherwise an explicit direction is required, see Direction parameter below. If the input contains face primitives, the primitive normal is independent of the target (U) point. Primitive normals can be displayed from the Display Options dialog.
Direction `dir` - ⊞ - The direction of the vector is the Normal parameter above is Off.
* X `dirx` -
* Y `diry` -
* Z `dirz` -
Coordinates `coord` - ⊞ - Specifies the absolute 3D location the (U, V) target must translate to.
* X `coordx` -
* Y `coordy` -
* Z `coordz` -
U and V `uvsnap` - ⊞ - The primitive method allows the target point to be snapped to a point on another primitive specified by U and V here. See Warp Method parameter for details.
* `uvsnap1` -
* `uvsnap2` -
```
   |opFamily=SOP
```
}}
  

## Parameters - U Page
Deform along U `uwarp` - Determines whether the clay operation affects the U parametric direction. Both faces and surfaces respond to this option. If the primitives are face types and the toggle is off, clay doesn't change the inputs at all. If the inputs are surfaces and U is off, clay will pull the surfaces along the entire V direction (if V is on) or not at all.
U `u` - This value defines a point in the parametric space of a face, representing the location to be affected by the clay operation. This location is referred to as the "target". For surfaces, U defines a line of constant value in the parametric space of the primitive and requires a second coordinate - V - to specify a unique location (see the V> Page below). Spline faces and surfaces have explicit parametric spaces known as domains; since domains are not restricted to the unit range [0, 1], the Clay SOP maps U to the real domain value of the primitive. For polygons and meshes, U is expressed in terms of the number or vertices and columns respectively and in terms of their relative positions.
U Bias `uusebias` - Indicates whether the clay algorithm should use the bias it thinks works best for the given U parameter, or take the value explicitly stated beside the toggle. Since clay affects the CVs in the neighbourhood of the given parametric location, the bias can influence the amount of pull applied to the CVs on either side of this location. The effect is a slant of the "wave" the parametric point rides on - towards one side or the other.
U Bias `ubias` -
U Sharpness `usharp` - This parameter affects only NURBS curves and surfaces. The pull generated by clay on these primitives can be smooth or sharp depending on the position of the target relative to the underlying domain (the farther away from a knot, the rounded the bulge) and the knot multiplicity near the target (the higher the multiplicity the sharper the pull). If the pull is too round or affects too big an area in U, the U Sharpness parameter can reduce it by inserting one or more knots at the target U value. When the U Sharpness is zero no knots are inserted. When the U Sharpness is 1, all "degree" knots are inserted and the shape becomes very sharp. The U Sharpness varies in discrete steps; the number of steps equals the U degree of the spline.
**Note:** The range of the U Sharpness slider varies with the degree of the spline (i.e. the closer it is to 1, the more knots it adds). Since the number of knots added forms a discrete sequence, the slider will automatically jump to the valid positions.

  

## Parameters - V Page
Deform along V `vwarp` - Determines whether the clay operation affects the V parametric direction of the surface. If the inputs are surfaces and V if off, clay will pull the surfaces along the entire U direction (if U is on) or not at all. If both U and V are on, clay will pull the surface at the target (U, V) point specified in the U and V folders below. This option does not affect face types.
V `v` - This value affects only surface types. V defines a line of constant value in the parametric space of the surface and together with U specifies a unique location in that space. Spline surfaces have explicit parametric spaces known as domains; since domains are not restricted to the unit range [0, 1], the Clay SOP maps V to the real domain value of the surface. For meshes, V is expressed in terms of the number or rows and their relative positions.
V Bias `vusebias` - Indicates whether the clay algorithm should use the bias it thinks works best for the given V parameter, or take the value explicitly stated beside the toggle. Since clay affects the CVs in the neighbourhood of the given parametric location, the bias can influence the amount of pull applied to the CVs on either side of this location. The effect is a slant of the "wave" the parametric point rides on -- towards one side or the other.
V Bias `vbias` -
V Sharpness `vsharp` - This parameter affects only NURBS surfaces. The pull generated by clay on these primitives can be smooth or sharp depending on the position of the target relative to the underlying domain (the farther away from a knot, the rounded the bulge) and the knot multiplicity near the target (the higher the multiplicity the sharper the pull). If the pull is too round or affects too big an area in V, the V Sharpness parameter can reduce it by inserting one or more knots at the target V value. When the V Sharpness is zero no knots are inserted. When the V Sharpness is 1, all "degree" knots are inserted and the surface becomes very sharp. The V Sharpness varies in discrete steps; the number of steps equals the V degree of the spline.
**Note:** The range of the V Sharpness slider varies with the degree of the spline (i.e. the closer it is to 1, the more knots it adds). Since the number of knots added forms a discrete sequence, the slider will automatically jump to the valid positions.

  

  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Clay SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\n2022.241402021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • Clay• [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Matching names using wildcard characters and bracketing. Useful in "[Select](Select_CHOP.html "Select CHOP")" type parameters to select multiple operators, paths, channels, etc.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Clay_SOP&oldid=24179>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")