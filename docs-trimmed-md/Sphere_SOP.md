

Sphere SOP - TouchDesigner Documentation





























# Sphere SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Sphere SOP generates spherical objects of different geometry types. It is capable of creating non-uniform scalable spheres of all geometry types.

If an input is provided, the sphere's radius is automatically determined as a function of the input's bounding geometry.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[sphereSOP\_Class](https://docs.derivative.ca/SphereSOP_Class "SphereSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Operator Inputs](#Operator_Inputs)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Page

Primitive Type `type` - ⊞ - Select from the following types. For information on the different types, see the [Geometry](Category_Geometry.html "Category:Geometry") category articles. Depending on the primitive type chosen, some SOP options may not apply. Using the 'Primitive' primitive type is not recommended when using instancing.

* Primitive `prim` -

* Polygon `poly` -

* Mesh `mesh` -

* NURBS `nurbs` -

* Bezier `bezier` -

Connectivity `surftype` - ⊞ - This option is used to select the type of surface, when using a Mesh Primitive Type.

* Rows `rows` - Creates horizontal lines.

* Columns `cols` - Creates vertical lines.

* Rows and Columns `rowcol` - Both Rows and Columns. Looks like Quads in wire frame display, but all polygons are open (if the primitive type is polygon).

* Triangles `triangles` - Build the grid with Triangles.

* Quadrilaterals `quads` - Generates sides composed of quadrilaterals (default).

* Alternating Triangles `alttriangles` - Generates triangles that are opposed; similar to the Triangles option.

Orient Bounds `orientbounds` - Available only when an input is connected to the Sphere SOP to set bounds for the sphere. When Orient Bounds = On it will rotate the geometry to match the orientation of the input SOP used for bounds.
Modify Bounds `modifybounds` - Available only when an input is connected to the Sphere SOP to set bounds for the sphere. When Modify Bounds = On the transform parameters below will further modify the rotation, position, and radius of the bounds.
Rotate Order `rord` - ⊞ - Sets the order in which the rotations are applied.

* Rx Ry Rz `xyz` -

* Rx Rz Ry `xzy` -

* Ry Rx Rz `yxz` -

* Ry Rz Rx `yzx` -

* Rz Rx Ry `zxy` -

* Rz Ry Rx `zyx` -

Radius `rad` - ⊞ - The radius of the sphere in X, Y and Z.

* X `radx` -

* Y `rady` -

* Z `radz` -

Center `t` - ⊞ - Offset of sphere center from object center.

* X `tx` -

* Y `ty` -

* Z `tz` -

Rotate `r` - ⊞ - These three fields rotate the Sphere along the X, Y, and Z axes.

* X `rx` -

* Y `ry` -

* Z `rz` -

Reverse Anchors `reverseanchors` - Invert the direction of anchors.
Anchor U `anchoru` - Set the point in X about which the geometry is positioned, scaled and rotated.
Anchor V `anchorv` - Set the point in Y about which the geometry is positioned, scaled and rotated.
Anchor W `anchorw` - Set the point in Z about which the geometry is positioned, scaled and rotated.
Orientation `orient` - ⊞ - Determines axis for sphere. Poles of sphere align with orientation axis.

* X Axis `x` -

* Y Axis `y` -

* Z Axis `z` -

Frequency `freq` - This controls the level of polygons used to create the sphere, when using the Polygon Primitive Type.
Rows `rows` - Number of rows in a sphere when using the mesh, imperfect NURBS and imperfect Bzier.
Columns `cols` - Number of columns in a sphere when using the mesh, imperfect NURBS and imperfect Bzier.
U Order `orderu` - If a spline curve is selected, it is built at this order for U.
V Order `orderv` - If a spline curve is selected, it is built at this order for V.
Imperfect `imperfect` - This option applies only to Bzier and NURBS spheres. If selected, the spheres are approximated nonrational curves, otherwise they are perfect rational curves.
Unique Points per Pole `upole` - Applies to Mesh, NURBS and Bzier surfaces only. This option determines whether points at the poles are shared or are individual to the columns.
Accurate Bounds `accurate` - If the SOP is being used to generate a bounding sphere for it's input geometry, this parameter tells the SOP to use a more accurate (but slower) bounding sphere calculation.
Texture Coordinates `texture` - ⊞ - Adds UV texture coordinates to the sphere.

* Off `off` - No UV coordinates added to surface.

* By Primitive Type `byprimtype` - Adds vertex UV coordinates.

* Equirectangular Inside (Spherical Polar) `equirectangularin` -

* Equirectangular Outside (Spherical Polar) `equirectangularout` -

* Equidistant Azimuth (Fish Eye 180) `equiazimuth` -

* Equidistant Azimuth (Fish Eye 360) `equiazimuth360` -

Compute Normals `normals` - Creates normals on the geometry.

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Sphere SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070

| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • Sphere• [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").


A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Sphere_SOP&oldid=31225>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")