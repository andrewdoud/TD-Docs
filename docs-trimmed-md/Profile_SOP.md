

# Profile_SOP

Profile SOP - TouchDesigner Documentation




# Profile SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Profile SOP enables the extraction and manipulation of profiles.
You will usually need a [Trim SOP](Trim_SOP.html "Trim SOP"), [Bridge SOP](Bridge_SOP.html "Bridge SOP"), or Profile SOP after a [Project SOP](Project_SOP.html "Project SOP"). Use a Trim SOP to cut a hole in the projected surface. Use a Bridge SOP to skin the profile curve to another profile curve.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[profileSOP\_Class](https://docs.derivative.ca/ProfileSOP_Class "ProfileSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Profile Page](#Parameters_-_Profile_Page)
* [3 Operator Inputs](#Operator_Inputs)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Profile Page
Group `group` - This field allows you to specify the particular group of curves on the surface. Other primitives are ignored. You can specify profile curves within the group by providing a profile pattern (e.g. \*.3 specifies the fourth profile in all spline surfaces).
Method `method` - ⊞ - This menu allows you to extract a stand-alone 3D curve as the world or parametric image of the profile. The non-parametric option will yield a curve whose shape and position in space are identical or very similar to those of the chosen profile. The parametric option will produce a planar, XY face whose vertices and type will be identical to those of the profile in 2D; also, if the profile is a spline it will have the same basis as the extracted curve.
* Extract `extract` - Use the extraction parameters below to extract a 3D curve from the profile.
* Remap `remap` - Use parametric parameters below to produce a planar face from the profile.
Parametrically to X Y `parametric` - If Fitted (this option not checked), the profile will be a spatial NURBS curve whose position and shape in space will be identical to the curve on surface. It may very well be non-planar. If Extracted Parametrically (this option checked), the result will extract the profile's parametric image as a 3D face, which will be a planar face in XY whose type (polygon, Bzier, NURBS) will the same as the profile's, and whose vertices match the profile CVs. This, however, does not guarantee spatial coincidence between profile and extracted curve, and is more of an analytical tool.
**Tip:** A profile extracted parametrically can be reapplied to the surface identically with the Project SOP by choosing the **Parametric** option with no Mapping to Range. Use this method to extract the profile, pull its points or edit it as you would any 3D face, then re-project it on the surface at the same location.

Smooth Curve `smooth` - If enabled, it will fit a spline through the extracted points. This parameter is disabled when extracting the profile parametrically. Disable this parameter in order to bypass the fitting process which might be both expensive (in processing speed) and unnecessary when extracting profiles produced by boolean operations (see [Surfsect SOP](Surfsect_SOP.html "Surfsect SOP")).
Divisions per Span `sdivs` - The number of points per span to be computed on the profile. A span is the line connecting two consecutive CVs on a polygon, or the arc between two breakpoints on a spline curve. The profile tends to become more accurate as the number of divisions is higher.
Tolerance `tolerance` - This parameter specifies the precision of the fitting process for the extracted 3D data, and is typically less than 0.01.
Order `order` - The spline order of the resulting 3D curve. The type of curve (Bzier or NURBS) is inherited from the spatial curve. The order, however, is not inherited because the spline order provides useful control over the quality of the fit. If the profile is a polygon, the spatial curve will be a NURBS curve.
Preserve Sharp Corners `csharp` - Controls the precision with which sharp corners in the profile curve are interpolated. It should be on when the profile has areas of high changes in curvature.
Keep Surface `keepsurf` - Specifies whether the parent surface should be removed after the extraction or not.
Delete Original Profile `delprof` - When Keep Surface parameter is On, select whether to leave or delete the original profile.
Mapping Type `maptype` - ⊞ - Select how to reposition and scale an existing profile to fit within the specified domain range. It is a good means of bringing an invisible profile into view by setting the mapping range between 0 and 1 in the U and V parametric directions. A profile mapped outside the unit domain becomes invisible but is not removed from the surface. Other ways to change a profile are available through the [Primitive SOP](Primitive_SOP.html "Primitive SOP").
* Uniform `unif` - Uniform converts the spatial coordinates of the profile to (U,V) points in the domain of the surface without taking into account the parameterization of the surface.
* Chord Length `chordlen` - Chord Length takes into account the surface parameterization and attempts to compute a profile best suited to the spatial and parametric determinants of the model.
U Range `urange` - ⊞ - Indicates in percentages what part of the U surface domain is the mapping area. A full range of 0-1 will cause the profiles to be mapped to the entire domain in the U parametric direction. The range is not restricted to the 0-1 interval.
* `urange1` -
* `urange2` -
V Range `vrange` - ⊞ - Indicates in percentages what part of the V surface domain is the mapping area. A full range of 0-1 will cause the profiles to be mapped to the entire domain in the V parametric direction. The range is not restricted to the 0-1 interval.
* `vrange1` -
* `vrange2` -
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Profile SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • Profile• [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Profile_SOP&oldid=24221>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")