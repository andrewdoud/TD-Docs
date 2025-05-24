

Curveclay SOP - TouchDesigner Documentation





























# Curveclay SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Curveclay SOP is similar to the Clay SOP in that you deform a spline surface not by modifying the CVs but by directly manipulating the surface. However, instead of using a point on the surface, you use one or more faces to deform that surface. Also, CurveClay does not yet support polygonal meshes.   
  

The combination of inputs will determine the modes of transformation. For any combination of inputs, the following parameters modify the following behaviors of the SOP.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[curveclaySOP\_Class](https://docs.derivative.ca/CurveclaySOP_Class "CurveclaySOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Curve Clay Page](#Parameters_-_Curve_Clay_Page)
* [3 Parameters - Projection Page](#Parameters_-_Projection_Page)
* [4 Parameters - Displacement Page](#Parameters_-_Displacement_Page)
* [5 Notes](#Notes)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Curve Clay Page

Face Group `facegroup` - Subset of faces (NURBS, Bézier, Polygons) to project, or subset of proles to deform, depending on how many inputs are connected.

Examples include: 0.5 1.2-3.9 5.\*

This group can even take surfaces (possibly intermixed with profile curves) when the 2nd input is not present, indicating that all the surface’s proles must be used.   

Then, the example above becomes: 0.5 1.2-3.9 5



Surface Group `surfgroup` - Subset of spline surfaces to be deformed when all three SOP inputs are connected.
Divisions on Face `divs` - The number of points to evaluate on the proles or the faces. This SOP works by using a straight line approximation of the given curve to deform the surface. Thus, more segments are slower, but the result looks better. Fewer divisions need to be specified when deforming proles and when the rest and deforming faces have an equal number of breakpoints.
Sharpness `sharp` - Species the area around the face to deform. The larger the sharpness is, the smaller the deformation area around them (thus having a sharper pull on the surface).
Refinement `refine` - Usually, CurveClay automatically renes the surface. However, you may specify some degree of renement control. In general, the more rened the surface is, the smoother the result. Better renement results in a denser surface. You should experiment with values between -1 and 1. When the value is negative, the SOP will rst rene the surface to the same detail level as when renement is 0, and then it unrenes it. The lower the value, the more unrened it becomes.

  


## Parameters - Projection Page

Controls curve projection. Enabled if all 3 inputs exist.

Projection Axis `projop` - ⊞ - Choice of several projection axes:

* X `xaxis` - Cartesian Axis - X, Y, or Z.

* Y `yaxis` - Cartesian Axis - X, Y, or Z.

* Z `zaxis` - Cartesian Axis - X, Y, or Z.

* Minimum Distance `mindist` - Project curve points to their closest places on surface.

* User Defined: `other` - Enter Vector into the field below.

 `projdir` - ⊞ - Specify the direction vector of the projection.

* `projdir1` -

* `projdir2` -

* `projdir3` -

  


## Parameters - Displacement Page

How to deform surface. Enabled if only 1 input exists.

Displacement Axis `deformop` - ⊞ - Choice of several projection axes:

* Surface Normal `snormal` - The proles will be deformed along the surface normal.

* X `xaxis` - Cartesian axis - X, Y, or Z.

* Y `yaxis` - Cartesian axis - X, Y, or Z.

* Z `zaxis` - Cartesian axis - X, Y, or Z.

* User Defined: `other` - Enter the vector into the eld below.

 `deformdir` - ⊞ - Specify the direction vector of the displacement.

* `deformdir1` -

* `deformdir2` -

* `deformdir3` -

Distance `deformlen` - Distance deformed along the vector.
Deform Inside of Loop `deforminside` - Check if the inside of closed loops should be deformed.
Consider Profiles Individually `individual` - Check if multiple curves form a closed loop.

  


## Notes

When using CurveClay on a wrapped surface, here are some points to remember:

* You may want to use a higher number of divisions, since when going across the seam of the wrapped surface, straight line approximation would be turned off and more sample points may be needed.
* If you’re not going across the seam, then the reﬁnement of the surface is only local. However, when the deformation area of the surface gets near the seam, the reﬁnement is done over the whole surface. Do not be alarmed if the whole surface has been reﬁned.

  


## Operator Inputs

* Input 0:  -
* Input 1:  -
* Input 2:  -

  


## Info CHOP Channels

Extra Information for the Curveclay SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • Curveclay• [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Curveclay_SOP&oldid=24184>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")