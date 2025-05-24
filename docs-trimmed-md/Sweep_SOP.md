

# Sweep_SOP

TouchDesigner Documentation




# Sweep SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Sweep SOP sweeps primitives in the Cross-section input along Backbone Source primitive(s), creating ribbon and tube-like shapes. The cross-section primitives are placed at each point of the backbone perpendicular to it. The Backbone Source can have one or several primitives. If there is more than one, Sweep will sweep the cross section along each one.
A backbone is a primitive curve that can be open or closed, but must have at least two points. The cross section input can also have multiple primitives, and can be assigned to the backbone in various ways. The origin of the cross section primitive is placed at a point on the backbone by default, but you can also choose a point number of the cross section to place. In most cases, it is best to build 1the cross section primitives in the XY plane; Sweep will automatically orient them properly along the backbone. The orientation of the cross section is based on the direction of the backbone line segment and the positive Z axis. So vertical movement in the backbone will result in the cross section rotating around backbone axis. For example, if you create the cross section in the XY plane, you can maintain its orientation (+Y Up) by building the backbone in the XZ plane.
If the backbone primitive(s) have point colors or texture coordinates, they will be maintained and applied to the cross section primitives.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[sweepSOP\_Class](https://docs.derivative.ca/SweepSOP_Class "SweepSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Sweep Page](#Parameters_-_Sweep_Page)
* [3 Parameters - Output Page](#Parameters_-_Output_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Sweep Page
X-Section Group `xgrp` - You can use only a subset of primitives from the Cross-section inputs by specifying a group here.
Path Group `pathgrp` - You can use only a subset of primitives from the Backbone inputs by specifying a group here.
Reference Group `refgrp` - You can use only a subset of primitives from the Reference inputs by specifying a group here.
Cycle Type `cycle` - ⊞ - Determines the Cycle Type based on these menu options.
* All Primitives at Each Point `all` - Places all the primitives from the Cross-section input at each point on the Backbone.
* One Primitive at a Time `each` - Similar to the above, except the transformation is applied to individual primitives rather than to the whole.
* Cycle Primitives `cycle` - This cycles through incoming primitives when placing them on a backbone. i.e. Start with 0 at vertex 0, primitive 1 > vertex 1, etc.
Angle Fix `angle` - Attempts to fix buckling twists that may occur when sweeping.
Fix Flipping `noflip` - Attempts to fix buckling twists that may occur when sweeping by fixing flipped normals.
Remove Coincident Points on Path `skipcoin` - When selected, any points right on top of one another will be ignored.
Aim at Reference Points `aimatref` - Reference Points are used in conjunction with the backbone to control the orientation of the elements along the sweep. This is done by drawing a line between the reference point and corresponding backbone point in order to determine an angle vector which determines the orientation of the cross-section profiles. Enable this parameter to allow this behaviour.
**Note:** In order for this to work, you must supply **Reference Points** via the third input, and there must be exactly the same number of **Reference Points** as there are points in the **Backbone**.

Use Vertex `usevtx` - Use vertex number of the incoming cross-section to place the cross-section on the backbone.
Connection Vertex `vertex` - Specify a specific vertex to connect to the backbone.
Scale `scale` - Scales the cross sections globally.
Twist `twist` - Cumulative rotation of the cross sections around the backbone. If a value of five is specified, the cross section at the first point of the backbone is rotated five degrees, the next ten degrees, the next fifteen degrees and so on.
Roll `roll` - Non-cumulative rotation of the cross sections around the backbone. All cross sections get the same rotation.
**Note:** The **Scale**, **Twist** and **Roll** parameters can now be controlled directly by points' attributes of the same names. Thus, combined with the [Channel SOP](CHOP_to_SOP.html "CHOP to SOP"), those parameters can now be controlled dynamically. You can use scale and other attributes coming in to taper.

  

## Parameters - Output Page
Create Groups `newg` - Selecting this option enables the creation of groups. A group is created for each backbone that is incoming. This allows for easy skinning in the [Skin SOP](Skin_SOP.html "Skin SOP").
Sweep Groups `sweepgrp` - Specify the name of your output groups in this field.
Skin Output `skin` - ⊞ - Determines the output based on these menu options.
* Off `off` - Doesn't skin the output.
* On `on` - Skins the output.
* On with Auto Close `auto` - Closes the skinned mesh if the path curve which it follows is also closed. This allows you to close primitives properly.
**Tip:** There is a way of speeding the skinning of many points using the second input of the [Point SOP](Point_SOP.html "Point SOP"). Suppose you have Thousands of proceedurally animated curves you wish to skin with the Sweep SOP - rather than performing a skining operation after the animation, make a second set of unanimated geometry that is preskinned. Then assuming your have a matching number of points you can just swap in the animated points into the skinned geometry.
This technique is significantly faster than using the Skin Output option of the Sweep SOP, or a Skin SOP following the Sweep SOP.

Fast Sweep `fast` - Enables an optimized skinning technique which speeds up output from 2 - 4 times in many cases at the expense of accuracy. In order for it to work correctly, the input topologies must remain consistent between cooks and each cross-section must have the same number of vertices.
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
* Input 2:  -
  

## Info CHOP Channels
Extra Information for the Sweep SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • Sweep• [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Sweep_SOP&oldid=31200>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")