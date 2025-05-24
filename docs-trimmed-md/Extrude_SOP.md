

TouchDesigner Documentation





























# Extrude SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Extrude SOP can be used for:

* Extruding and bevelling Text and other geometry
* Cusping the bevelled edges to get sharp edges
* Making primitives thicker or thinner

The default is a 1 unit extrusion directly backwards from the input geometry's normals.

It uses the normal of the surface to determine the direction of extrusion. In the case of planar or open polygons, the normal is difficult to determine, and may not always provide the result that you expect. Turn on the Primitive Normals display in the [Viewer](Viewer.html "Viewer") display options to see the normals.

The extrusion is created by extending surfaces from the vertices of the input geometry along the cross-section curve given in the second input (Input 1). The first vertex of the cross-section curve is placed by default at the vertices of the input geometry and aligned so that the curve's positive Y axis extends opposite to the input geometry's normal. The cross-section's positive X axis by default extends outwards from center of the input geometry.

If no cross-section curve is given, a vertical line going from (0,0,0) to (0,1,0) is used. This results in a 1 unit extrusion directly backwards from the input geometry's normals. As another example, using a straight line from (0,0,0) to (.1,.1,0) will result in an extrusion that extends 1 unit backwards from the input and flares .1 unit outwards on all sides. The Thickness and Depth parameters can be used to shift and scale the cross-section without directly changing the curve.

**Note:** The shape of the cross-section is always relative to its first vertex, so shifting the entire cross-section curve will have no effect. Also, only the X and Y axes of the curve are used i.e. Z position values are ignored.

After the new geometry is created, normals are computed by default.

**Warning:** If you take a default output from a [Text SOP](Text_SOP.html "Text SOP") and Extrude it, it may have bad rendering artifacts (and too many polygons) as it's extruding each of the triangles of the triangulated letters. You need to change the Output parameter of the Text SOP to Closed Polygons. See [OP Snippets](OP_Snippets.html "OP Snippets").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[extrudeSOP\_Class](https://docs.derivative.ca/ExtrudeSOP_Class "ExtrudeSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Values Page](#Parameters_-_Values_Page)
* [4 Parameters - Groups Page](#Parameters_-_Groups_Page)
* [5 Production Tips](#Production_Tips)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Page

Source Group `sourcegrp` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified for the source. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
X-Section Group `xsectiongrp` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified for the cross-section. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").

  


## Parameters - Values Page

Fuse Points `dofuse` - ⊞ - This should almost always be turned on when cross-sections are used. It consolidates points of polygons that would otherwise cross or overlap when the bevel takes place.

* No fusion `off` -

* Clamp all points `all` -

* Clamp minimal set `min` -

* Clamp individual face `on` -

* Clamp straight `straight` -

Front Face `fronttype` - ⊞ - Control how the front face of the extrusion should be built. You may wish to have a "No Output" because some faces are never actually seen when doing animation and, therefore, would only take up additional overhead if left on.

* No Output `off` - No face is created.

* Output Face `face` - Faces are created.

* Convex Face `convex` - Create faces built with Convex Polygons (use this option if faces are to be deformed, i.e. [Twist SOP](Twist_SOP.html "Twist SOP"), [Lattice SOP](Lattice_SOP.html "Lattice SOP")).

Back Face `backtype` - ⊞ - This value controls whether or not the back of the extruded object will have a face or not. The options are the same as the Front Face options above.

* No Output `off` -

* Output Face `face` -

* Convex Face `convex` -

Side Mesh `sidetype` - ⊞ - Controls how the cross-section(s) will be extruded. If the input cross-section is a Bzier or NURBS curve, the surface will be constructed with a patch of the same geometry type.

* No Output `off` - No mesh is created.

* Rows `rows` - Creates horizontal lines.

* Columns `cols` - Creates vertical lines.

* Rows and Columns `rowcol` - Both Rows and Columns. Looks like Quads in wire frame display, but all polygons are open (if the primitive type is polygon). Compare them in the Model Editor.

* Triangles `triangles` - Build the grid with Triangles.

* Quadrilaterals `quads` - Generates sides composed of quadrilaterals (default).

* Alternating triangles `alttriangles` - Generates triangles that are opposed; similar to the Triangles option.

Initialize Extrusion `initextrude` - If the cross-section face that you created doesn't match up nicely to the size of the geometry you are extruding, this command will scale and translate it so that it fits nicely.

The reason it might not be nice to begin with is that the curve wasn't drawn exactly on the world-axis in Model-mode and/or was drawn at a grossly different scale than the object it is extruding.



Thickness Translate `thickxlate` - Shifts the cross-section profile perpendicularly to the normals of the input geometry. This relates to the X axis of the cross-section profile. When used with text, this typically has the effect of making the text lighter (narrower) or heavier (bolder).
Thickness Scale `thickscale` - Scales the cross-section profile perpendicularly to the normals of the input geometry. This is equivalent to scaling the cross-section in its X axis. This parameter has no effect on the default profile, which is equivalent to a vertical line along the Y axis. Negative scaling values are allowed.
Depth Translate `depthxlate` - Moves the cross-section in the direction of the normal. Positive values will move backwards to the direction of the normal. Depth movement relates to the Y axis of the input cross-section. Using this parameter will shift the position of the output geometry in direction of the normal.
Depth Scale `depthscale` - Scales the cross-section in the direction of the source geometry's normals. This is equivalent to scaling the input cross-section in its Y axis and will determine how deep (thick) the resulting extrusion is.
Vertex `vertex` - Translates the cross-section such that the vertex specified is at the cross-section origin.
Cusp Polygonal Sides `docusp` - Determines whether or not sides are to be smooth-shaded or faceted using the angle value in Side Cusp Angle field.

Cusping lets you specify at which angle between adjacent polygons, a sharp edge (faceted edge where vertices are un-shared) should be displayed instead.



Side Cusp Angle `cuspangle` - When checked, this value will control the angle at which faceting of the sides will occur. A value of 20 is default.
Consolidate Faces to Mesh `sharefaces` - If selected the extrusion will share points between the front face and the first row of the side mesh and between the last face and the last row of the side mesh.
Remove Shared Sides `removesharedsides` - Prevents the creation of duplicate sides.

  


## Parameters - Groups Page

Create Output Groups `newg` - When this option is checked, it causes the Extrude SOP to generate three new groups representing the primitives belonging to the front faces, back faces, and the side bevel/extrusion. The name of the groups are determined by the three option fields below.
Front Group `frontgrp` - Output group name to create for front face geometry.
Back Group `backgrp` - Output group name to create for back face geometry.
Side Group `sidegrp` - Output group name to create for side bevel/extrude geometry.

  


## Production Tips

This SOP is mainly used for generating bevels and extrusions of text where the input cross-sections are fed from a [Font SOP](Font_SOP.html "Font SOP"). Any curve or group of curves can also be used as input.

Offsets - This SOP can be used for generating two offsetting curves where the distance between the two curves remains constant. To do this, make sure that you set Side Mesh to No Output, the first thickness to zero and adjust the second to increase or decrease the distance of the offset.

Fixing Stray Normals - If your geometry contains normals that are pointed in many directions (say after reading geometry from a [File In SOP](File_In_SOP.html "File In SOP"), or if you have a lot of open or non-planar polygons), you can fix it so that they are suitable for extrusion.

Do this by appending a [Group SOP](Group_SOP.html "Group SOP") to the SOP that contains your geometry, enable Normal, and reduce the Spread Angle to something less than 180. Then append a [Primitive SOP](Primitive_SOP.html "Primitive SOP"), which should work on the group made in the Group SOP. In the Face/Hull page, set the Vertex menu to Reverse.

Now the normals in your geometry will all be oriented in the roughly the same direction, and ready for extrusion. To narrow the tolerance, decrease the Spread Angle further.

  


## Operator Inputs

* Input 0:  -
* Input 1:  -

  


## Info CHOP Channels

Extra Information for the Extrude SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • Extrude• [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").


A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Extrude_SOP&oldid=24187>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")