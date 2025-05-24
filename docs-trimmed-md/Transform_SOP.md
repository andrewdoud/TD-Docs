

Transform SOP - TouchDesigner Documentation




# Transform SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Transform SOP translates, rotates and scales the input geometry in "object space" or local to the SOP. The Model Editor and the Transform SOP both work in "object space", and change the X Y Z positions of the points. In contrast, animating the transformation channels of an object in the Geometry Viewer Pane moves/scales the entire object in "world space" and does not affect the XYZ point positions of the geometry.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[transformSOP\_Class](https://docs.derivative.ca/TransformSOP_Class "TransformSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [3 Parameters - Post Page](#Parameters_-_Post_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Transform Page
Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
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
Uniform Scale `scale` - Uniform Scale allows you to shrink or enlarge geometry along all three axes simultaneously.
Normals Maintain Length `vlength` - When selected, vector type attributes (i.e. normals, velocity) maintain the same length under transforms. i.e. When geometry is scaled, the normals remain constant in length.
Look At `lookat` - Allows you to orient your object by naming the object you would like it to Look At, or point to. Once you have designated this object to look at, it will continue to face that object, even if you move it. This is useful if, for instance, you want a camera to follow another object's movements. The Look At parameter points the object in question at the other object's origin.
**Tip:** To designate a centre of interest for the camera that doesn't appear in your scene, create a Null object and disable its display flag. Then Parent the Camera to the newly created Null object, and tell the camera to look at this object using the Look At parameter. You can direct the attention of the camera by moving the Null object with the Select state. If you want to see both the camera and the Null object, enable the Null object's display flag, and use the Select state in an additional Viewport by clicking one of the icons in the top-right corner of the TouchDesigner window.

Up Vector `upvector` - ⊞ - When orienting an object, the Up Vector is used to determine where the positive Y axis points.
* X `upvectorx` -
* Y `upvectory` -
* Z `upvectorz` -
Forward Direction `forwarddir` - ⊞ -
* +X `posx` -
* -X `negx` -
* +Y `posy` -
* -Y `negy` -
* +Z `posz` -
* -Z `negz` -
  

## Parameters - Post Page
The transforms on this page are apllied after the settings made on the Transform page (see above).
Post Transform Order `postxord` - ⊞ - Set the order in which scale and transform is applied in the post transform.
* Scale Translate `st` -
* Translate Scale `ts` -
Post Translate X `posttx` - ⊞ - Sets the center of the geometry after the Transform page has been applied.
* Off `off` - No Change.
* Origin `origin` - Moves the geometry to the origin 0,0,0.
* Reference Input `reference` - Moves the geometry to a location based on the Reference Input supplied to this SOP's second input (ie. Input 1).
From Input `fromx` - ⊞ - Determines which part of the input geometry to align to the Origin or Reference Input as selected in Post Translate parameter above.
* Min `min` - Align to the geometry's minimum bounds in this axis.
* Center `center` - Align to the geometry's center point in this axis.
* Max `max` - Align to the geometry's maximum bounds in this axis.
To Reference `tox` - ⊞ - When using Reference Input this determines which part of the Reference Input to align the geometry to.
* Min `min` - Align to the Reference Input's minimum bounds in this axis.
* Center `center` - Align to the Reference Input's center in this axis.
* Max `max` - Align to the Reference Input's maximum bounds in this axis.
Post Translate Y `postty` - ⊞ - Sets the center of the geometry after the Transform page has been applied.
* Off `off` - No Change.
* Origin `origin` - Moves the geometry to the origin 0,0,0.
* Reference Input `reference` - Moves the geometry to a location based on the Reference Input supplied to this SOP's second input (ie. Input 1).
From Input `fromy` - ⊞ - Determines which part of the input geometry to align to the Origin or Reference Input as selected in Post Translate parameter above.
* Min `min` - Align to the geometry's minimum bounds in this axis.
* Center `center` - Align to the geometry's center point in this axis.
* Max `max` - Align to the geometry's maximum bounds in this axis.
To Reference `toy` - ⊞ - When using Reference Input this determines which part of the Reference Input to align the geometry to.
* Min `min` - Align to the Reference Input's minimum bounds in this axis.
* Center `center` - Align to the Reference Input's center in this axis.
* Max `max` - Align to the Reference Input's maximum bounds in this axis.
Post Translate Z `posttz` - ⊞ - Sets the center of the geometry after the Transform page has been applied.
* Off `off` - No Change.
* Origin `origin` - Moves the geometry to the origin 0,0,0.
* Reference Input `reference` - Moves the geometry to a location based on the Reference Input supplied to this SOP's second input (ie. Input 1).
From Input `fromz` - ⊞ - Determines which part of the input geometry to align to the Origin or Reference Input as selected in Post Translate parameter above.
* Min `min` - Align to the geometry's minimum bounds in this axis.
* Center `center` - Align to the geometry's center point in this axis.
* Max `max` - Align to the geometry's maximum bounds in this axis.
To Reference `toz` - ⊞ - When using Reference Input this determines which part of the Reference Input to align the geometry to.
* Min `min` - Align to the Reference Input's minimum bounds in this axis.
* Center `center` - Align to the Reference Input's center in this axis.
* Max `max` - Align to the Reference Input's maximum bounds in this axis.
Post Scale `postscale` - ⊞ - Sets the scale of the geometry after the Transform page has been applied.
* Per Axis `peraxis` - Allows individual settings for each axis using the parameters below.
* Unity `unity` - Scales the geometry to fit in a 1,1,1 bounding box.
* Reference `reference` - Scales the geometry to fit the Reference Input's bounding box (second input on this SOP ie. Input 1).
Post Scale X `postscalex` - ⊞ - Sets the scale of the geometry after the Transform page has been applied to scale.
* Off `off` - No change the the scale in this axis.
* Unity `unity` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis.
* Reference Input `reference` - Scale the geometry to fit the Reference Input in this axis.
* Unity Proportional `unityprop` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis while keeping the input geometry's original proportions.
* Reference Proportional `referenceprop` - Scale the geometry to fit the Reference Input in this axis while keeping the input geometry's original proportions.
Post Scale Y `postscaley` - ⊞ - Sets the scale of the geometry after the Transform page has been applied to scale.
* Off `off` - No change the the scale in this axis.
* Unity `unity` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis.
* Reference Input `reference` - Scale the geometry to fit the Reference Input in this axis.
* Unity Proportional `unityprop` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis while keeping the input geometry's original proportions.
* Reference Proportional `referenceprop` - Scale the geometry to fit the Reference Input in this axis while keeping the input geometry's original proportions.
Post Scale Z `postscalez` - ⊞ - Sets the scale of the geometry after the Transform page has been applied to scale.
* Off `off` - No change the the scale in this axis.
* Unity `unity` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis.
* Reference Input `reference` - Scale the geometry to fit the Reference Input in this axis.
* Unity Proportional `unityprop` - Scale the geometry to 1.0 (ie. -0.5 to 0.5) in this axis while keeping the input geometry's original proportions.
* Reference Proportional `referenceprop` - Scale the geometry to fit the Reference Input in this axis while keeping the input geometry's original proportions.
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Transform SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • Transform• [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A 3D viewport for viewing and manipulating 3D scenes or objects interactively. A geometry viewer can be found in [Panes](Pane.html "Pane") (alt+3 in any pane) or the [Node Viewers](Node_Viewer.html "Node Viewer") of all Geometry Object components.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Transform_SOP&oldid=29944>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")