

# Carve_SOP

TouchDesigner Documentation




# Carve SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Carve SOP works with any face or surface type, be that polygon, Bzier, or NURBS. It can be used to slice a primitive, cut it into multiple sections, or extract points or cross-sections from it.
Like the Project SOP, it also creates profile curves, but they are extracted as iso-parametric (2D) profiles directly from a surface, whereas the Project SOP extracts a 3D curve projected onto a surface.
Note: When using a Carve SOP on a trimmed surface, you can't fillet or join the trim curves.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[carveSOP\_Class](https://docs.derivative.ca/CarveSOP_Class "CarveSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Carve Page](#Parameters_-_Carve_Page)
* [3 Parameters - Method Page](#Parameters_-_Method_Page)
* [4 Example](#Example)
  + [4.1 Opening a Closed Primitive](#Opening_a_Closed_Primitive)
  + [4.2 Dicing a Face or Surface](#Dicing_a_Face_or_Surface)
  + [4.3 Cutting a Hole in a Surface](#Cutting_a_Hole_in_a_Surface)
  + [4.4 Animating a Point Over a Face or Surface](#Animating_a_Point_Over_a_Face_or_Surface)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Carve Page
Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the Group specified. Accepts patterns, as described in the Scripting Guide under Pattern Matching.
First U `firstu` - Enables the parameter to set the first position in U.
First U `domainu1` - This specifies a starting location to begin the cut/extract. Select this and a parametric U location between 0 and 1.
Second U `secondu` - Enables the parameter to set the second position in U.
Second U `domainu2` - This specifies an ending location to complete the cut / extract. Select this and a parametric U location between 0 and 1.
First V `firstv` - Enables the parameter to set the first position in V.
First V `domainv1` - This specifies a starting location to begin the cut/extract. Select this and a parametric V location between 0 and 1. Applies only to surfaces.
Second V `secondv` - Enables the parameter to set the second position in V.
Second V `domainv2` - This specifies an ending location to complete the cut / extract. Select this and a parametric V location between 0 and 1. Applies only to surfaces.
  

## Parameters - Method Page
Carve Method `method` - ⊞ - Select between Cut and Extract methods.
* Cut `cut` - Cut will slice (or 'cut-out') the original geometry within the area specified on the Carve Page.
* Extract `extract` - Extract will create 3D curves, points, or 2D profiles within the area specified on the Carve page. The Extract Type parameter is used to determine what is extracted.
Keep Inside `keepin` - Keep the primitives specified between the first and second locations.
Keep Outside `keepout` - Keep the primitives lying outside the first and second locations.
Extract Type `extractop` - ⊞ - If enabled, it will extract a cross-section along each location specified above.
Note: if a face is used, only points can be extracted and the V parameters have no effect.
* Extract 3D Isoparametric Curve(s) `xisoparm` - The extraction operation creates a 3-D, free-floating curve that matches the surface perfectly at the given U or V location.
* Extract Point(s) `xpoint` - Available for Mesh and surfaces only. If selected, it will create a point at every U, V location specified, rather than removing a U cross section and a V cross section.
* Extract 2D Isoparametric Profile(s) `xprofile` - Creates a 2D curve at the specified U/V location that matches the surface perfectly.
Keep Original `keeporiginal` - If selected, it will not remove the original primitive.
Location `location` - ⊞ - Determines how the Cut/Extract is defined at the boundaries. Additionally, extra subdivisions can be added in two ways using the parameters below.
* Divisions `div` - The Cut/Extract occurs precisely at the locations defined on the Carve page. Additional divisions can be specified using the U/V Divisions parameters below and they are evenly distributed across the Cut/Extracted geoemtry.
* Breakpoints `break` - Performs cutting or extractions at breakpoints for curves and surfaces, at vertices for polygons, and along isoparms for meshes.
By default this option will only cut the outer breakpoints within the specified interval. By selecting Breakpoints, the U and V Divisions parameters are replaced with Cut At All Internal U/V Breakpoints, which cut the primitives at all breakpoints falling within the specified interval when enabled.

U Divisions `divsu` - This specifies the number of cuts / extracts to be performed between first U and the second U.
V Divisions `divsv` - Specifies the number of cuts/extracts to be performed between first V and second V.
Cut at All Internal U Breakpoints `allubreakpoints` - When using Location = Breakpoints, the resulting primitive is divided at all U breakpoints into separate primitives.
Cut at All Internal V Breakpoints `allvbreakpoints` - When using Location = Breakpoints, the resulting primitive is divided at all V breakpoints into separate primitives.
  

## Example
### Opening a Closed Primitive
Given a closed surface, it can be converted to an identical open surface at any location by using the Carve SOP, and cutting at a single location (e.g. First U enabled, Second U disabled). The same is true for faces.
  

### Dicing a Face or Surface
Select the Cut operation, First U = `0`, Second U = `1`, First V = `0`, Second V = `1`, with (at least) three Divisions for U and V. This will dice the surface into (at least) 3 components. This can later be used with the Primitive SOP to "explode" the surface.
  

### Cutting a Hole in a Surface
Select the Cut operation, First U = `0.33`, Second U = `0.66`, First V = `0.33`, Second V = `0.66`, `2` Divisions for U and V. Keep Inside is off, Keep Outside is on. This will cut a rectangular region from the centre of the surface.
  

### Animating a Point Over a Face or Surface
Select the Extract option, First U = `x`, Last U disabled, First V = `y`, Last V disabled, Extract Point is on, Keep Primitives is optional. This will create a point over any position on the surface (0<=x<=1, 0<=y<=1).
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Carve SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • Carve• [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Matching names using wildcard characters and bracketing. Useful in "[Select](Select_CHOP.html "Select CHOP")" type parameters to select multiple operators, paths, channels, etc.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Carve_SOP&oldid=24176>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")