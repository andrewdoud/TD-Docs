

Capture SOP - TouchDesigner Documentation





























# Capture SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Capture SOP is used to weight points in a geometry to capture regions. The weighting scheme is described in the next section, [Capture Region SOP](Capture_Region_SOP.html "Capture Region SOP").

The weights and the regions they correspond to are transferred down the SOP chain as point and detail attributes.

The Capture SOP can take an optional second input to specify extra capture regions to use in the capture process. Any capture regions that are in this second input are processed after the capture regions that are in the object hierarchy specified by the Hierarchy parameter. You can also specify a second input and not specify a Parent Object at all.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[captureSOP\_Class](https://docs.derivative.ca/CaptureSOP_Class "CaptureSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Capture Page](#Parameters_-_Capture_Page)
* [3 Parameters - Override Page](#Parameters_-_Override_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Capture Page

Group `group` - Specify the point groups from the first input (input0) to operate on.
Hierarchy `rootbone` - An object hierarchy is traversed to find the Capture Regions with which to do the weighting. This parameter specifies the top of the traversal hierarchy.
Weight from `weightfrom` - ⊞ - Use this menu to specify where to get the weight from.

* Surface `surface` - (default) Uses the surface to compute the weight of a point (or CV in the case of NURBS). This is very helpful for NURBS surfaces when the CV's may be far off the surface. By using Weight From Surface, each CV is weight based on the surface's location within a Capture Region. This is determined by calculating the CVs "most influenced point" on the NURBS surface and computing the weight of that position.

* Points `cv` - Using the Weight From Points choice, the location of the point within the region is used for the weighting.

Capture Frame `captframe` - Specifies the frame number to do the capture computations. Every time TouchDesigner reaches this frame, the geometry will be re-captured. It is a common practice to set the Capture Frame to an frame outside of your animation range, -1 for example. Specifies the frame number to do the capture computations. Every time TouchDesigner reaches this frame, the geometry will be re-captured. It is a common practice to set the Capture Frame to an frame outside of your animation range, -1 for example.

**Note:** When a .toe file is loaded, all of the associated capture regions are evaluated at the Capture Frame. Keyframes must be set to position the capture regions properly at the Capture Frame, otherwise the geometry will be weighted incorrectly upon the subsequent file loads.



Point Coloring `color` - ⊞ - This option colors each point by capture region (using point attributes) according to its capture weight. The points inherit their colors from the Capture Region(s) in which they lie. For example, if a point falls within a blue capture region and also a yellow capture region, the point will be colored green (more blue near if the blue weighting dominates, and more yellow if the yellow weight dominates). In addition, the points become darker as the weighting gets lighter. For example, near the edge of a blue region, a caught point will appear dark blue. Near the centre, it will appear bright blue. If a point is not caught by any region, it is colored bright red.

* Default Source Color `coldefault` -

* Color by Capture Region `colregion` -

Override File `captfile` - The name of the capture override file (`*.ocapt`). This file is loaded after TouchDesigner completes its point weighting. Each line of the override file lists a point number, a region (path and primitive number) and a weight. The points on the geometry are modified to use these custom weights.

**Override File Format** - Each line in the override file must have the following format:

For example:

```
0 /obj/chain_bone1/cregion 0 0.0 			
0 /obj/chain_bone2/cregion 0 3.757989 			
0 /obj/chain_bone3/cregion 0 1.757989			

```

  

This weights point 0 to three regions (actually only two because the first entry has a weight of zero). Remember that the Override File is read after TouchDesigner does it's own capture weight computation, so in this case, if point 0 was originally assigned to region `/obj/chain_bone4/cregion 0`, this part of its weighting would be unchanged.
There is no upper limit to the number of regions that can be weighted to a point. If a point/region combination is in the file twice, the second one is used.

For example:

```
0 /obj/chain_bone1/cregion 0 1.0			
0 /obj/chain_bone1/cregion 0 2.0			

```

This causes the first entry to be ignored (a weighting of 2.0 is used).

The weight field is used to prescribe the relative amount of influence a region has on a point. It can be any number. The range of the weights computed by TouchDesigner are specified by the Inner/Outer Weight parameter of each Capture Region (please see [Capture Region SOP](Capture_Region_SOP.html "Capture Region SOP")).
The easiest way to a capture Override File is to use the Save Override File button (see below) and start from the file produced by TouchDesigner.


  


## Parameters - Override Page

Save File `savefile` - The file specified here can be used as a "working file" to save the point weighting of all the points or a selected subset of points. The file format for the capture override files is fairly straight-forward (see above), so this is a good place to start if you need to do custom overriding.
Increment Save File `autoincr` - This increments the Save File name before saving. Be careful about turning this option off because there is no warning or confirm dialog to prevent you from overwriting an .ocapt file.
Save All Data to File `savecaptfile` - This saves the point weighting of all points to the Save File.
Save Selected Points to File `savesel` - This saves the point weighting only for the points that are selected in the viewport.

Note: you must be editing this particular SOP in the Viewport for this selection to apply to this SOP.


  


## Operator Inputs

* Input 0:  -
* Input 1:  -

  


## Info CHOP Channels

Extra Information for the Capture SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • Capture• [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


Hierarchy relates components with other components. There are two groups of Hierarchy in TouchDesigner. 3D Object Components, and 2D Panel Components. Hierarchies let one component to be positioned relative to another. Each group can be connected via lines between the bottoms/tops of nodes in a network, or by placing one component inside the other.


The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).


TOuch Environment file, the file type used by TouchDesigner to save your entire project.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Capture_SOP&oldid=24255>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")