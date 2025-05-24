

# DAT_to_SOP

DAT to SOP - TouchDesigner Documentation




# DAT to SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The DAT to SOP can be used to create geometry from DAT tables, or if a SOP input is specified, to modify attributes on existing geometry. See also the [Add SOP](Add_SOP.html "Add SOP").
Without a SOP input, the output is created entirely from the DAT, one SOP point per row of the DAT, except for an optional top row with column headings. The common columns headings include the point number `index`, point position `P(0) P(1) P(2)`, point weight `Pw`, the color and alpha `Cd(0) Cd(1) Cd(2) Cd(3)`, texture coordinates `uv(0) uv(1) uv(2)`, and point normal `N(0) N(1) N(2)`. If no index column is specified, row number is used as the point number. If there is no heading for the Point DAT, the list of attributes is assumed to be in order `P(0) P(1) P(2) Pw Cd(0) Cd(1) Cd(2) Cd(3) N(0) N(1) N(2) uv(0) uv(1) uv(2)` for the first 14 columns.
If an input is used, attributes are read in and replace the ones in the existing geometry. The Merge parameter will be enabled when an input is connected. Depending on the Merge menu setting, either the Points DAT or Primitive DAT parameter used for the merge data. If an input is used, the Points or Primitives DAT must have a column named `index`. This column is used to match the point or primitive to the incoming geometry by point or primitive number.
Attributes in the columns headings should have column name *`attrib`* if it is a single value attribute, or have multiple columns named `attrib(0)`, `attrib(1)`, `attrib(2)` etc if it is a multiple-value attribute.
Data can also be converted into a form that can be rendered as particles.
**Example File :** [File:SOPtoDATtoSOP.tox](https://docs.derivative.ca/File:SOPtoDATtoSOP.tox "File:SOPtoDATtoSOP.tox")
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[dattoSOP\_Class](https://docs.derivative.ca/DattoSOP_Class "DattoSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Operator Inputs](#Operator_Inputs)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Points DAT `pointsdat` - DAT with point data. The optional `index` indicates the point number, if none is specified, row number will be used. Attributes can be specified in `attribute_name(attribute_index)`. If there are no named column headings for the Point DAT, the index column should be removed and the list of attributes is assumed to be in order `P(0) P(1) P(2) Pw Cd(0) Cd(1) Cd(2) Cd(3) N(0) N(1) N(2) uv(0) uv(1) uv(2)` for the first 14 columns. Sample point data:
```
   index	P(0)	P(1)	P(2)	Pw	N(0)	N(1)	N(2)									
   0		-0.5	-0.5	-0.5	1	0	0	-1								
   1		-0.5	0.5	-0.5	1	0	0	-1								
   2		0.5	0.5	-0.5	1	0	0	-1								
   3		0.5	-0.5	-0.5	1	0	0	-1								
   ...																
```
The common columns attributes include point position `P(0) P(1) P(2)`, point weight `Pw`, the color and alpha `Cd(0) Cd(1) Cd(2) Cd(3)`, texture coordinates `uv(0) uv(1) uv(2)`, and point normal `N(0) N(1) N(2)`. See [Point Attributes](Attribute.html#Point_Attributes "Attribute") for a list of attributes.

Vertices DAT `verticesdat` - DAT with vertex data. `index` indicates the primitive number and `vindex` the vertex number in that primitive. Attributes are specified in the same manner as for points. ample vertex data:
```
   index	vindex	uv(0)	uv(1)	uv(2)												
   0		0	0	0	0											
   0		1	0	1	0											
   0		2	1	1	0											
   0		3	1	0	0											
   1		0	1	0	0											
   1		1	1	1	0											
   1		2	1	1	1											
   1		3	1	0	1											
   ...																
```
Common attributes include the color and alpha `Cd(0) Cd(1) Cd(2) Cd(3)`, texture coordinates `uv(0) uv(1) uv(2)`, and vertex normal `N(0) N(1) N(2)`. See [Vertex Attributes](Attribute.html#Vertex_Attributes "Attribute") for a list of attributes.

Primitives DAT `primsdat` - DAT with primitive data. The optional `index` indicates the primitive number, if none is specified, row number will be used. Column headings are required; `vertices` list the point numbers in order, `close` indicates whether the primitive is a closed or open curve. Attributes are specified in the same manner as for points. Sample primitive data:
```
   index	vertices	close	Cd(0)	Cd(1)	Cd(2)	Cd(3)										
   0		0 1 2 3		1	0.2	1	1	1								
   1		4 5 6 7		1	0.2	0.2	0.5	1								
   2		8 9 10 11	1	0.2	0.2	0.2	1									
```
Common attributes include the color and alpha `Cd(0) Cd(1) Cd(2) Cd(3)`. See [Primitive Attributes](Attribute.html#Primitive_Attributes "Attribute") for a list of attributes.

Detail DAT `detaildat` - DAT with detail data. Attribute names are specified on the first row and attribute data on the second row. Sample detail data:
```
   pCaptPath		pCaptData(0)	pCaptData(1)	pCaptData(2)	...											
   /bone1/cregion 	0		3.33333		0		...
```
Merge `merge` - ⊞ - Specify whether to merge point data or primitive data. This parameter is only enabled when there is an input connected to the SOP.
* Points `points` - Merge point data.
* Vertices `vertices` -
* Primitives `primitives` - Merge primitive data.
* Detail `detail` -
Add Float Attributes `float` - Add a non-standard attribute specified in the point or primitive DAT as a float.
Add Int Attributes `int` - Add a non-standard attribute specified in the point or primitive DAT as an int. It will not be added if it has already been specified in the Float attributes.
Add String Attributes `string` - Add a non-standard attribute specified in the point or primitive DAT as a string. It will not be added if it has already been specified in the Float or Int attributes.
Build `build` - ⊞ - Specifies how to build geometry.
* Use Primitive DAT `dat` - Build geometry using data from the Primitive DAT.
* Connect All Points `all` - Connect all points.
* Connect Every 2 Points `pts2` - Connect points in pairs.
* Connect Every 3 Points `pts3` - Connect points in triples.
* Connect Every 4 Points `pts4` - Connect every 4 points together.
* Connect Every N Points `ptsn` - Connect every N points together.
* Polygon with N Rows `polyrow` - Create a polygon grid with N rows.
* Polygon with N Columns `polycol` - Create a polygon grid with N columns.
* Mesh with N Rows `meshrow` - Create a mesh grid with N rows.
* Mesh with N Columns `meshcol` - Create a mesh grid with N columns.
* Particle System using All Points `particleall` - Creates a particle system of points.
N `n` - Number of points used for building primitives.
Closed U `closed` - Closed curves in U.
Closed V `closedv` - Closed curves in V.
Connectivity `connect` - ⊞ - Connectivity of polygons.
* Rows `rows` - Creates horizontal lines.
* Columns `cols` - Creates vertical lines.
* Rows and Columns `rowcol` - Both Rows and Columns. Looks like Quads in wireframe display, but all polygons are open (if the primitive type is polygon). Compare them in the Model Editor.
* Triangles `triangles` - Build the grid with Triangles.
* Quadrilaterals `quads` - Generates sides composed of quadrilaterals (default).
* Alternating Triangles `alttriangles` - Generates triangles that are opposed; similar to the Triangles option.
Particle Type `prtype` - ⊞ - When creating a particle system, specify to render the particles as lines or point sprites.
* Render as Lines `lines` -
* Render as Point Sprites `pointprites` -
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the DAT to SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • DAT to• [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=DAT_to_SOP&oldid=24257>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")