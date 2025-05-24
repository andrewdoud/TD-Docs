

Add SOP - TouchDesigner Documentation





























# Add SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Add SOP can both create new Points and Polygons on its own, or it can be used to add Points and Polygons to an existing input.

If an input is specified, this SOP adds points and polygons to it as specified below. If no input is specified, then it generates the points and polygons below as a new entity. It can read points and vertices from DATs. See also [DAT to SOP](DAT_to_SOP.html "DAT to SOP").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[addSOP\_Class](https://docs.derivative.ca/AddSOP_Class "AddSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Points Page](#Parameters_-_Points_Page)
* [3 Parameters - Polygons Page](#Parameters_-_Polygons_Page)
* [4 Parameters - Post Page](#Parameters_-_Post_Page)
* [5 Uses](#Uses)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Points Page

Points DAT `pointdat` - Path to a [Table DAT](Table_DAT.html "Table DAT") containing point data. By default, x, y, z, and w can be defined in the first 4 columns of the table using un-named columns.

If the `Named Attributes` parameter below is turned on, the following attributes can be defined in the Points Table DAT using named columns:

* `P(0) P(1) P(2) P(3)`
* `N(0) N(1) N(2)`
* `Cd(0) Cd(1) Cd(2) Cd(3)`
* `uv(0) uv(1) uv(2)`

Any other columns are added as single-float attributes.

**NOTE:** Turn off `Compute Normals` on the Polygon parameter page when supplying `N(0) N(1) N(2)` in the Points Table DAT.



Named Attributes `namedattribs` - Allows extra attributes to be defined in the Point Table DAT above.
Delete Geometry, Keep Points `keep` - Use this option to remove any unused points. When checked, existing geometry in the input are discarded, but the polygons created by this SOP are kept, as well as any points in the input.
Add Points `addpts` - When On you can add individual points with position and weight of your choosing by using the parameters below.
Point `point` - Sequence of points to add
Position `point0pos` - ⊞ - The three input fields represent the X, Y and Z coordinates of the point. These values can be constants (numbers) or variables. Below are three examples:
```
0.2    0.42    1.3

```

```
0.2    op('xform1').par.tx    1.36

```

```
# read the sixth point (first point is 0) from the SOP, grid1
op('grid1').points[5].x    op('grid1').points[5].y    op('grid1').points[5].z

```

* Position `point0posx` -

* Position `point0posy` -

* Position `point0posz` -

Weight `point0weight` - The spline weight of the point. If the point is later used to create a spline (nurbs or Bezier) primitive, the weight will influence the shape of the primitive and may cause that primitive to become rational. Polygons and metaballs are not affected by this weight.

  


## Parameters - Polygons Page

Method `method` - ⊞ - Specify to create polygons from the points by using a Group method or Pattern Method.

* By Group `group` - Create as many polygons as determined by the group field and by the grouping / skipping rules.

* By Pattern `pattern` - Specify the points to use to create polygons using the parameters Polygon Table or Polygon 0 below.

Group `group` - Subset of points to be connected.
Add `add` - ⊞ - Optionally join subgroups of points.

* All Points `all` - Adds all points just as if you added them manually in the Points page.

* Groups of N Points `group` - Adds only the number of points specified.

* Skip Every Nth Point `skip` - Adds points, buts skips every Nth one.

* Each Group Separately `sep` - Creates separate polygons for each group specified in the `Group` parameter. For example, if you have a Group SOP creating a group called group1 and using the `Create Boundary Groups` option, you can connect this to an Add SOP and enter group1\_\_\* in the `Group` parameter. If `Each Group Separately` is chosen, polygons will be created for each boundary on the surface.

**Tip: The Each Group Separately option is useful when pasting surfaces. Boundary groups can be created for the boundaries of two adjacent surfaces, and then the PolyLoft SOP (using the Points option) can be used to stitch these surfaces together.**


N `inc` - Increment / skip amount to use for adding points.
Closed `closedall` - Closes the generated polygons.
Polygons Table `polydat` - Path to a Table DAT containing polygon data. Accepts rows of polygons specified by point number in the first column. The second column indicates if the polygons are closed (1) or open (0).
Polygon `poly` - Sequence of polygon patterns
Pattern `poly0pattern` - Create a fixed number of polygons by specifying a point pattern for each polygon. Enter connection lists here to add polygons. These consist of a list of point numbers to define the order in which the points are to be connected. The form is: {from}-{to}[:{every}][,{of}].

Examples of Valid Connection Lists:

`1 2 3 4` - Makes a polygon by connecting point numbers 1,2,3,4.
`1 3-15 16 8` - All points from 3-15 are included.
`1-234 820-410 235-409` - Points from 1-820 are included, in the specified order.
`0-15:2` - Every other point from 0 to 15 is included.
`0-15:2,3` - Every 2 of 3 points are included (i.e. 0, 1, 3, 4, 6, 7, 9, 10, 12, 13, 15).
`!4` - Every point except 4 is included.
`!100-200` - Every point <100 and >200 is included.
`*` - Include all points.
`9-0` - The first ten points are included in reverse order.
`!9-0` - All but the first ten points are included in reverse order.
Closed `poly0closed` - To create a closed polygon, check the Closed button.

  


## Parameters - Post Page

Remove Unused Points `remove` - Keep only the connected points, and discard unused points.
Compute Normals `normals` - Creates normals on the geometry.

  


## Uses

Used in conjunction with a point expression, the Add SOP can be useful for extracting a specific point from another SOP. For example, to extract the X, Y and Z value of the fifth point, from a Grid SOP in geo1:

```
op('geo1/grid1').points[5].x
op('geo1/grid1').points[5].y
op('geo1/grid1').points[5].z

```

Points added in this way are appended to the end of the point list if a Source is specified. Middle-mouse click on the SOP node to find out how many points there are. For example, if you have added two points and there are 347 points (from 0 to 346), you have added the last two point numbers: 345 and 346.

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Add SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002020.200002018.28070before 2018.28070

| SOPs |
| --- |
| Add• [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.


A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.


A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Add_SOP&oldid=32293>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")