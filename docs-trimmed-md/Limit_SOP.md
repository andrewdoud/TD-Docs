

# Limit_SOP

Limit SOP - TouchDesigner Documentation




# Limit SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Limit SOP creates geometry from samples fed to it by [CHOPs](CHOP.html "CHOP"). It creates geometry at every point in the sample. Different types of geometry can be created using the Output Type parameter on the **Channels Page**.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[limitSOP\_Class](https://docs.derivative.ca/LimitSOP_Class "LimitSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Channels Page](#Parameters_-_Channels_Page)
* [3 Parameters - Custom Page](#Parameters_-_Custom_Page)
* [4 Parameters - Output Page](#Parameters_-_Output_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Channels Page
CHOP `chop` - Specifies which CHOP Network / CHOP contains the sample data to fetch.
Rotate Order `rord` - ⊞ - Specifies the order in which the Rotate Channel X / Y / Z channels are applied.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
X Channel `chanx` - Channels used to specify the point's positions, tx.
Y Channel `chany` - Channels used to specify the point's positions, ty.
Z Channel `chanz` - Channels used to specify the point's positions, tz.
Rotate Channel X `chanrx` - Channels used to specify the rotational data of the geomtery created at each point. Only used when Output Type is "Polygon at Each Point" or "Primitive Circle at Each Point".
Rotate Channel Y `chanry` - Channels used to specify the rotational data of the geomtery created at each point. Only used when Output Type is "Polygon at Each Point" or "Primitive Circle at Each Point".
Rotate Channel Z `chanrz` - Channels used to specify the rotational data of the geomtery created at each point. Only used when Output Type is "Polygon at Each Point" or "Primitive Circle at Each Point".
Radius Channel `chanrad` - Uniformly controls the radius of the geometry created at each point. The Radius channels are multiplied with the Radius parameter on the **Output Page**.
Radius Channel X `chanradx` - Channels that control the radius on the respective axis. The Radius channels are multiplied with the Radius parameter on the **Output Page**.
Radius Channel Y `chanrady` - Channels that control the radius on the respective axis. The Radius channels are multiplied with the Radius parameter on the **Output Page**.
Radius Channel Z `chanradz` - Channels that control the radius on the respective axis. The Radius channels are multiplied with the Radius parameter on the **Output Page**.
Alpha Channel `chanalpha` - Controls the point alpha, giving you alpha control of any geometry created at those points.
**Note:** If using a [Copy SOP](Copy_SOP.html "Copy SOP"), turn on the Use Template Point Attributes option in the Copy SOP's **Attributes Page** to allow the geometry to inherit the point attributes.

Red Channel `chanr` - These channels control the point color, or the color of any geometry created at those points.
Green Channel `chang` - These channels control the point color, or the color of any geometry created at those points.
Blue Channel `chanb` - These channels control the point color, or the color of any geometry created at those points.
Texture W `texturew` - Controls the w texture-offset for the point(s) This is most often used as a frame-offset or time-offset, expressed in # of frames from the current frame or frame 1 of an image sequence.
  

## Parameters - Custom Page
Allows custom attributes to be added to the geometry created. Use the + button to add additional parameters to add more custom attributes.
Custom Attribute `customattr` - Sequence of custom attributes to be added to the geometry created.
Name `customattr0name` - Specify the name of the custom attribute, for example pscale, age, or any custom name.
Channel Zero `customattr0chan0` - Select which channel to assign to the [0] index of the attribute. ie. pscale[0]
Channel One `customattr0chan1` - Select which channel to assign to the [1] index of the attribute. ie. pscale[1]
Channel Two `customattr0chan2` - Select which channel to assign to the [2] index of the attribute. ie. pscale[2]
Channel Three `customattr0chan3` - Select which channel to assign to the [3] index of the attribute. ie. pscale[3]
  

## Parameters - Output Page
Output Type `output` - ⊞ - The type of geometry the Limit SOP produces from its sample data.
* Polygonal Line `line` - Creates a point for each sample and connects them with a polygonal line.
* Polygon at Each Point `polys` - Places a polygon at each sample point. Number of points in polygon defined by Divisions.
* Primitive Circle at Each Point `circles` - Places a primitive circle at each sample point.
* Sphere at Each Point `spheres` - Places a primitive sphere at each smaple point.
* Poly Sphere at Each Point `polyspheres` - Places a polygonal sphere at each sample point. Sphere's frequency defined by Divisions.
* Tubes `tubes` - Creates a tube down the path. Tubes cross-section defined by Divisions.
* Strips `strips` - Creates a strip down the path. Number of points in strip defined by Divisions.
Divisions `divisions` - Only works on the following Output Types.
* Polygon at Each Point - Number of points per polygon.
* Poly Sphere at Each Point - Frequency of each Polygonal Sphere.
* Tubes - Number of points in cross-section of the tube.
* Strips - Number of points in cross-section of the strip.

Radius `rad` - Radius of geometry created. Disabled for "Polygonal Line".
Smooth Flip `flipsmooth` - Dynamically controls the twist of each instance of geometry on a series of points to avoid frame-by-frame flipping, which can sometimes occur when geometry is oriented along a path.
Limit `dolimit` - ⊞ - Creates a bounding box for the position of the output geometry. Drop down menu determines behavior when outside bounded region.
* Off `off` - Bounding region off.
* Clamp `clamp` - Clamps position to specified value.
* Loop `loop` - Loops position between bounded region.
* Zigzag `zigzag` - Zigzags position back and forth between bounded region.
X Limit `xlimit` - ⊞ - Parameters to set edges of bounding region when Limit is active.
* `xlimitmin` -
* `xlimitmax` -
Y Limit `ylimit` - ⊞ - Parameters to set edges of bounding region when Limit is active.
* `ylimitmin` -
* `ylimitmax` -
Z Limit `zlimit` - ⊞ - Parameters to set edges of bounding region when Limit is active.
* `zlimitmin` -
* `zlimitmax` -
Apply Texture `texture` - Applys u, v, and w texture coordinates to the created geometry.
Scale `texscale` - ⊞ - Scales the texture coordinates a specific amount.
* `texscale1` -
* `texscale2` -
Offset `texoffset` - ⊞ - Offsets the texture coordinates a specific amount.
* `texoffset1` -
* `texoffset2` -
Orient to Path `orient` - If this option is selected, the object will be oriented along the path. To see what the path looks like, change the Output Type to "Polygonal Line". When the Output Type is "Polygon/Primitive Circle at Each Point", the positive Z axis of each object will be pointing down the path. When the Output Type is "Tubes/Strips" then the cross-section of the geometry created will be pointing down the path.
Lookat Object `lookat` - Orient to Path must be checked for Lookat Object to have any effect. This allows you to orient your geometry by naming the object you would like it to Look At, or point to. Once you have designated this object to look at, it will continue to face that object, even if you move it. The Look At parameter points the each piece of geometry at the other object's origin individually.
Rotate Polys `dorotate` - ⊞ - Rotate the geometry at each point using the Rotate parameter (below). Only works for Output Type is "Polygon/Primitive Circle at Each Point".
* Off `off` - Do not rotate polys. Rotate parameter is greyed out.
* On `on` - Add value of Rotate to polys equally.
* Cumulative `cum` - Add value of Rotate to polys cumulatively (ie. increasing with each poly).
Rotate `rotate` - ⊞ - Rotation channels rx, ry, and rz for Rotate Polys parameter.
* X `rotatex` -
* Y `rotatey` -
* Z `rotatez` -
Compute Normals `normals` - Computes normals for the geometry created.
  

## Info CHOP Channels
Extra Information for the Limit SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2021.100002020.200002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • Limit• [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Limit_SOP&oldid=32299>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")