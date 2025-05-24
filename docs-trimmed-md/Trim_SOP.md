

# Trim_SOP

Trim SOP - TouchDesigner Documentation




# Trim SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Trim SOP cuts out parts of a spline surface, or uncuts previously cut pieces. When a portion of the surface is trimmed, it is not actually removed from the surface; instead, that part is made invisible. This means that you can still modify the surface (modify the position of its points, for instance) that is not displayed in order to affect the part that is displayed.
The surface can be trimmed by specifying open or closed profiles as inside or outside regions. The profiles need not be contained within the domain (UV space) of the surface; they can also be nested.
Open profiles are treated as follows: if both ends of the profile are inside the surface, the ends are connected to one another; if the profile's ends are outside the domain of the surface they are projected onto, that part of the surface appears to be cut away.
You will usually need a Trim SOP, [Bridge SOP](Bridge_SOP.html "Bridge SOP"), or [Profile SOP](Profile_SOP.html "Profile SOP") after a [Project SOP](Project_SOP.html "Project SOP").
* Use a Trim SOP to cut a hole in the projected surface.
* Use a [Bridge SOP](Bridge_SOP.html "Bridge SOP") to skin the profile curve to another profile curve.
* Use a [Profile SOP](Profile_SOP.html "Profile SOP") to extract the curve on surface or remap it's position.
### Selection Method - Winding Rule
The selection method employed for clarifying overlapping trim loops is the winding rule, which executes overlapping commands instead of having them cancel each other out.
**Tip:** Since only surfaces containing profile curves can be trimmed, you will always need a Project or [Carve SOP](Carve_SOP.html "Carve SOP") in the chain above the Trim SOP.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[trimSOP\_Class](https://docs.derivative.ca/TrimSOP_Class "TrimSOP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 Selection Method - Winding Rule](#Selection_Method_-_Winding_Rule)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Example](#Example)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Group `group` - This field allows you to specify the group that you would like to trim. You can select the group from the pop-up menu, or specify a points and primitives range.
You can specify profile curves within the group by providing a profile pattern (e.g. `*.3` specifies the fourth profile in all spline surfaces).

 `optype` - ⊞ - The types of trimming operations available.
* Keep Outside `keepout` - Trims the interior of the curve, or makes a hole in the display of the surface. Keeping what's outside the profile curve generates an outer trim loop in order to define the limits of the surface to be displayed-the surface that's outside of the profile curve.
* Keep Inside `keepin` - Keeps the interior of the curve and removes the display of everything else.
* Keep Natural `keepnatural` - Trim based on the natural orientation of the profiles, be they open or not. Counter-clockwise profiles keep their interior, generating a result similar to Keep Inside. Clockwise profiles discard their interior, similar to Keep Outside, and may require an explicit outer trim-loop if none is present.
* Untrim `untrim` - Turns the trim curve into a plain profile.
* Change Altitude `chgalt` -
Process Profiles Individually `individual` - When this option is off, the trim loops in the group (or all the loops on the surfaces if no group has been specified) will be considered together to form a region. It will report the first region that is found. That is, if more than one closed loop could be formed by joining the lines, there is no guarantee that the region is trimmed. Also, if there is a closed loop in the group of loops, then just that loop is used.
If the loops on the surface don't form a closed loop, then the SOP will attempt to form a region by using the boundary of the region. If all the loops make a total of two intersections with the boundary, then it will attempt to form the loop by forming it around the boundary.
**For example:** Use the [Carve SOP](Carve_SOP.html "Carve SOP") to extract four profiles: two in U, and two in V. Pipe that into a Trim SOP and turn this option off. The four profiles will define a region to be trimmed. Notice that the profile end-points do not coincide, and the profiles are not parametrically continuous, nor are they created in the proper order. Despite all this, the Trim SOP is able to figure out the hole.

Build outer Trim-Loop Explicitly `bigloop` - This option allows you to specify that an outer trim loop be built. It is useful where you have more than one profile curve on the surface and are performing several successive trim operations involving both the Keep Inside and Keep Outside options (see example, below).
**Tip:** An outer trim loop must be generated the first time you punch a hole in the surface, but not if you just keep the contents of that hole and throw away the rest. By default, the outer loop (which goes all around the domain boundary) is built for you automatically. Sometimes, however, you first do a **Keep Inside**, then a **Keep Outside** with an area that's not inside the preserved regions, so you may want the outer curve at that point. That is when this parameter is useful.

Trimming Tolerance `trimtol` - How close two trim curves must be to each other or to the edge of the patch in order to be considered an intersection.
Altitude `altitude` - You can specify the altitude of the trim. The `$ALTITUDE` variable is the surface's current altitude. This marks the transition for the surface from trimmed in to trimmed out.
  

## Example
The following results were obtained by using a [Project SOP](Project_SOP.html "Project SOP") to project two NURBS circles onto a NURBS grid. Then two Trim SOPs were added, one after the other, to the [Project SOP](Project_SOP.html "Project SOP") . The first Trim SOP was set to Keep Inside, while the second Trim SOP had it's operation changed as indicated.
[![TouchGeometry15.gif](https://docs.derivative.ca/images/7/7a/TouchGeometry15.gif)](https://docs.derivative.ca/File:TouchGeometry15.gif)
The illustrations show a Gouraud shaded view of the resulting geometry.
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Trim SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • Trim• [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A way of moving data from one TouchDesigner process to another. Images are moved via Touch Out / In TOPs, channels are moved via Touch Out / In CHOPs and Pipe Out / In CHOPs. Data moves via TCP/IP or UDP.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Trim_SOP&oldid=24246>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")