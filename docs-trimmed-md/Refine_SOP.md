

Refine SOP - TouchDesigner Documentation





























# Refine SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Refine SOP allows you to increase the number of CVs in any NURBS, Bzier, or polygonal surface or face without changing its shape. It is also used to decrease the number of CVs within a given tolerance (i.e. a simple but fast method of data reduction).

### The Difference Between Refinement and Unrefinement

Refinement and unrefinement work both on faces (polygons, Bzier curves and NURBS curves) and surfaces (primitive meshes, Bzier surfaces and NURBS surfaces). To unrefine a face or a surface you need to specify a parametric interval (not just a single value as in refinement). This allows you to unrefine primitives within arbitrary intervals, either locally or globally. For example, to unrefine the whole primitive choose 0 and 1 as the two parametric boundaries; [0,0.5] will unrefine only the first parametric half of the primitive.

The interval boundaries are given by the First/Second U/V fields. Since refinement does not need an interval, the Second U/V fields are disabled by default.

The Tolerance control is only available for unrefinement, and not for refinement. Refinement does not need tolerances because it generates a curve or a surface that is mathematically identical to the original. Unrefinement, however, may tend to smooth out (or "melt") the original in a given area. In short, unrefinement is lossy; refinement isn't.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[refineSOP\_Class](https://docs.derivative.ca/RefineSOP_Class "RefineSOP Class")

## Contents

* [1 Summary](#Summary)
  + [1.1 The Difference Between Refinement and Unrefinement](#The_Difference_Between_Refinement_and_Unrefinement)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Refine Page](#Parameters_-_Refine_Page)
* [4 Parameters - Unrefine Page](#Parameters_-_Unrefine_Page)
* [5 Parameters - Subdivide Page](#Parameters_-_Subdivide_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Page

Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
First U `firstu` - Enable or disable the First U controls.
First U `domainu1` - This specifies a starting / ending location to complete the operation. Select this and a parametric U location between 0 and 1.
Second U `secondu` - Enable or disable the Second U controls.
Second U `domainu2` - This specifies a starting / ending location to complete the operation. Select this and a parametric U location between 0 and 1.
U Divisions `divsu` - If refining or sub-dividing, this option specifies the number of refines to be performed between First U and Second U.
First V `firstv` - Enable or disable the First V controls.
First V `domainv1` - This specifies a starting / ending location to complete the operation. Select this and a parametric V location between 0 and 1.
Second V `secondv` - Enable or disable the Second V controls.
Second V `domainv2` - This specifies a starting / ending location to complete the operation. Select this and a parametric V location between 0 and 1.
V Divisions `divsv` - If refining or sub-dividing, this option specifies the number of refines to be performed between First V and Second V.

  


## Parameters - Refine Page

If enabled, will refine the primitive at the locations specified above. If the primitive is a NURBS, then a knot is inserted multiple times as described below.

NURB Count U `refineu` - Number of knots to insert at each location in the U / V basis when refining NURBS.
NURB Count V `refinev` - Number of knots to insert at each location in the U / V basis when refining NURBS.
Spacing `space` - ⊞ - Specify how to measure along splines / curves.

* Uniform Domain Lengths `domain` - Refine at equal basis intervals if refining a spline.

* Uniform Arc Lengths `arc` - Each refinement is done at the centre of the maximum knot span (splines) or edge length (polygons).

**Note:** **Uniform Domain Lengths** should be selected if the domain ranges are animating, otherwise the inserted points will be undeterminable as different maximum lengths are encountered.

  


## Parameters - Unrefine Page

If enabled, will remove CVs from any NURBS curve or surface, polygon or mesh (points/ rows removed) between First U and Second U, and First V and Second V.

NURB Count U `unrefineu` - Number of knots to remove at each location in the U / V basis if refining NURBS.
NURB Count V `unrefinev` - Number of knots to remove at each location in the U / V basis if refining NURBS.
Tolerance U `tolu` - Only remove knots that do change the curve, polygon, or surface by more than this distance.
Tolerance V `tolv` - Only remove knots that do change the curve, polygon, or surface by more than this distance.

  


## Parameters - Subdivide Page

Subdivide refines a primitive such that the subdivision causes a sharp discontinuity if ever displaced. In essence subdivide is equivalent to refine for polygons and Bziers, since any refinement causes a potential discontinuity. In the case of a NURBS it is equivalent to a maximum refinement (i.e. count = primitive basis order - 1).

Spacing `subdivspace` - ⊞ - Subdivide refines a primitive such that the subdivision causes a sharp discontinuity if ever displaced. In essence subdivide is equivalent to refine for polygons and Bziers, since any refinement causes a potential discontinuity. In the case of a NURBS it is equivalent to a maximum refinement (i.e. count = primitive basis order - 1).

* Uniform Domain Lengths `domain` - Refine at equal basis intervals if refining a spline.

* Uniform Arc Lengths `arc` - Each refinement is done at the centre of the maximum knot span (splines) or edge length (polygons).

**Note:** **Uniform Domain Lengths** should be selected if the domain ranges are animating, otherwise the inserted points will be undeterminable as different maximum lengths are encountered.

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Refine SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070

| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • Refine• [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Refine_SOP&oldid=27206>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")