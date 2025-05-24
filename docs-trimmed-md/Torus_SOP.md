

# Torus_SOP

Torus SOP - TouchDesigner Documentation




# Torus SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Torus SOP generates complete or specific sections of torus shapes (like a doughnut).
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[torusSOP\_Class](https://docs.derivative.ca/TorusSOP_Class "TorusSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Torus Page](#Parameters_-_Torus_Page)
* [3 Parameters - Detail Page](#Parameters_-_Detail_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Torus Page
Primitive Type `type` - ⊞ - Select from the following types. For information on the different types, see the [Geometry](Category_Geometry.html "Category:Geometry") category articles.
* Polygon `poly` -
* Mesh `mesh` -
* NURBS `nurbs` -
* Bezier `bezier` -
Connectivity `surftype` - ⊞ - This option is used to select the type of surface, when using a Mesh primitive type.
* Rows `rows` - Creates horizontal lines.
* Columns `cols` - Creates vertical lines.
* Rows and Columns `rowcol` - Both Rows and Columns. Looks like Quads in wire frame display, but all polygons are open (if the primitive type is polygon).
* Triangles `triangles` - Build the grid with Triangles.
* Quadrilaterals `quads` - Generates sides composed of quadrilaterals (default).
* Alternating Triangles `alttriangles` - Generates triangles that are opposed; similar to the Triangles option.
Orientation `orient` - ⊞ - The axis along which the torus is constructed.
* X Axis `x` -
* Y Axis `y` -
* Z Axis `z` -
Modify Bounds `modifybounds` - Enabled only when an input is connected to the Torus SOP to set bounds for the torus. Turn Modify Bounds = On to enable the transform parameters below to further modify the position and radius of the bounds.
Radius `rad` - ⊞ - The first value (radx) defines the radius of the torus, the second value (rady) determines the radius of the inner ring.
[![TouchGeometry256.gif](https://docs.derivative.ca/images/4/4a/TouchGeometry256.gif)](https://docs.derivative.ca/File:TouchGeometry256.gif)
* X `radx` -
* Y `rady` -
Center `t` - ⊞ - Offset of torus center from object origin.
* X `tx` -
* Y `ty` -
* Z `tz` -
Reverse Anchors `reverseanchors` - Invert the direction of anchors.
Anchor U `anchoru` - Set the point in X about which the geometry is positioned, scaled and rotated.
Anchor V `anchorv` - Set the point in Y about which the geometry is positioned, scaled and rotated.
Anchor W `anchorw` - Set the point in Z about which the geometry is positioned, scaled and rotated.
Rows `rows` - The rows define the number of divisions along the torus.
Columns `cols` - The columns determine the number of divisions along the torus' cross-section.
  

## Parameters - Detail Page
Angle Offset `angleoffset` - Rotates the torus along the minor radius. For example, if using 4 rows set this value to 45 to create flat top + bottom surfaces.
Imperfect `imperfect` - This option applies only to Bezier and NURBS types. If selected, the tube is an approximated nonrational curve, otherwise it is a perfect rational curve.
U Order `orderu` - If a spline curve is selected, it is built at this order for U and V.
V Order `orderv` - If a spline curve is selected, it is built at this order for U and V.
U Angle `angleu` - ⊞ - The start and end sweep angles of the torus, if U Wrap is not enabled.
* `beginangleu` -
* `endangleu` -
V Angle `anglev` - ⊞ - These are the start and end angles of the cross-section circle that is swept to make the torus, if V Wrap is not enabled.
* `beginanglev` -
* `endanglev` -
U Wrap `closeu` - If U Wrap is checked, it creates a 360 cross-section.
V Wrap `closev` - Checking V Wrap creates a torus along V by closing the primitive.
U End Caps `capu` - If U End Caps is checked, it puts faceted end-caps on the ends of the torus if it is less than 360.
For more capping options, turn this parameter off, and append a Cap SOP.

V End Caps `capv` - If V End Caps is checked, it applies a face between the top and bottom of the torus - if the torus is open.
For more capping options, turn this parameter off, and append a Cap SOP.

  

Texture Coordinates `texture` - ⊞ - This adds uv coordinates to the geometry created by the Torus SOP.
* Off `off` - No uv coordinates added.
* Row & Columns `rowcol` - uv coordinates added based on Rows and Columns in the geometry.
Compute Normals `normals` - Checking this option On will compute surface normals.
## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Torus SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • Torus• [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Torus_SOP&oldid=27187>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")