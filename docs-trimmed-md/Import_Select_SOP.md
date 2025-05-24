

Import Select SOP - TouchDesigner Documentation





























# Import Select SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Import Select SOP is used to import and load the geometry types primitives defined in [USD COMP](USD_COMP.html "USD COMP") and [FBX COMP](FBX_COMP.html "FBX COMP"). It essentially loads any geometry type that [USD COMP](USD_COMP.html "USD COMP") or [FBX COMP](FBX_COMP.html "FBX COMP") can support such as a Mesh, Points, NURBS Curves or Patches, Basis Curves. Each geometry represents one primitive from the loading file or it can be a set of primitives merged together for better performance.

In [USD COMP](USD_COMP.html "USD COMP") and [FBX COMP](FBX_COMP.html "FBX COMP") if the Import Select SOP renders merged geometries, an [Info DAT](Info_DAT.html "Info DAT") operator is created next to this SOP which represents the original paths of primitives within/from importing file, which can be useful for user to checkout what geometry the current SOP is made of.
Import Select SOP can have its own animation controls within the Playback page or use the settings from its parent COMP.

The imported geometry can be loaded directly from GPU or CPU, depending on whether the Straight To GPU toggle is set to ON or not at the parent COMP node.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[importselectSOP\_Class](https://docs.derivative.ca/ImportselectSOP_Class "ImportselectSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - General Page](#Parameters_-_General_Page)
* [3 Parameters - Playback Page](#Parameters_-_Playback_Page)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Specific Import Select SOP Info Channels](#Specific_Import_Select_SOP_Info_Channels)
  + [4.2 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - General Page

Import Parent `parent` - Specify the import parent (eg. USD/FBX COMP) to search for the asset. When no COMP is specified it will by default search in the first import parent in its path.
Geo Path `geometry` - The geometry path from the imported file.
Reload `reload` - Reloads the asset from the import parent.
Compute Tangents `comptang` - A toggle to compute the tangents for this SOP.
## Parameters - Playback Page

Use Parent Animation `useparentanim` - A toggle to specify whether to use the parent COMP animation controls or have a custom setting for this SOP.
Shift Animation Start `shiftanimationstart` - A toggle to specify whether to shift the animation to the start of animation indicated in the importing file.
Sample Rate Mode `sampleratemode` - ⊞ - A menu to choose between the FPS or use a custom sample rate.

* File FPS `filefps` - uses the FPS from what is defined in the importing file.

* Custom `custom` - a desired value specified by Sample Rate parameter.

Sample Rate `samplerate` - It is used to specify the sample rate (FPS) for the animation. This parameter is disabled by default and can be enabled once the Custom option is selected from the Sample Rate Menu.
Play Mode `playmode` - ⊞ - A menu to specify the method used to play the animation.

* Locked to Timeline `lockedtotimeline` - This mode locks the animation position to the timeline. The parameters Play, Speed, Index, Cue and Cue Point, are disabled in this mode since the timeline is directly tied to animation position.

* Specify Index `specifyindex` - This mode allows the user to specify a particular index (position) in the animation using the Index parameter below. Use this mode for random access to any location in the animation.

* Sequential `sequential` - This mode continually plays regardless of the timeline position (the Index parameter is disabled). Play, Speed, Cue, and Cue Point parameters below are enabled to allow some control. The default is set to this value.

Initialize `initialize` - Resets the animation to its initial state.
Start `start` - Resets the animation to its initial state and starts playback.
Cue `cue` - A toggle to jump to Cue Point when it is set to ON and it stays at that position. Only available when Play Mode is Sequential.
Cue Pulse `cuepulse` - When pressed the animation jumps to the Cue Point and continues from that point.
Cue Point `cuepoint` - Set any index in the animation as a point to jump to.
Cue Point Unit `cuepointunit` - ⊞ - Specifies a unit type for Cue Point. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Play `play` - A toggle that makes the animation to play when it sets to ON. This Parameter is only available/enabled if the Sequential mode is selected from the Play Mode.
Index `index` - This parameter explicitly sets the animation position when Play Mode is set to Specify Index. The units’ menu on the right lets you specify the index in the following units: Index, Frames, Seconds, and Fraction (percentage).
Index Unit `indexunit` - ⊞ - Specifies a unit type for Index. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Speed `speed` - This is a speed multiplier which only works when Play Mode is Sequential. A value of 1 is the default playback speed. A value of 2 is double speed, 0.5 is half speed and so on.
Trim `trim` - A toggle to enable the Trim Start and Trim End parameters.
Trim Start `tstart` - Sets an in point from the beginning of the animation, allowing you to trim the starting index of the animation. The units’ menu on the right let you specify this position by index, frames, seconds, or fraction (percentage).
Trim Start Unit `tstartunit` - ⊞ - Specifies a unit type for Trim Start. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Trim End `tend` - Sets an end point from the end of the movie, allowing you to trim the ending index of the animation. The units’ menu on the right let you specify this position by index, frames, seconds, or fraction (percentage).
Trim End Unit `tendunit` - ⊞ - Specifies a unit type for Trim End. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Extend Left `textendleft` - ⊞ - Determines how the parent COMP handles animation positions that lie before the Trim Start position. For example, if Trim Start is set to 1, and the animation current index is -10, the Extend Left menu determines how the animation position is calculated.

* Hold `hold` -

* Cycle `cycle` -

* Mirror `mirror` -

Extend Right `textendright` - ⊞ - Determines how the parent COMP handles animation positions that lie after the Trim End position. For example, if Trim End is set to 20, and the animation current index is 25, the Extend Right menu determines how the animation position is calculated.

* Hold `hold` -

* Cycle `cycle` -

* Mirror `mirror` -

  


## Info CHOP Channels

Extra Information for the Import Select SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific Import Select SOP Info Channels

* true\_start\_time -

* true\_end\_time -

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

  

TouchDesigner Build: Latest\n2021.100002019.146502018.28070

| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • Import Select• [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.


There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.


The panel at the bottom of TouchDesigner, it controls the current global looping [Time](Time_COMP.html "Time COMP") your TouchDesigner project, or of just one component.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Import_Select_SOP&oldid=24472>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")