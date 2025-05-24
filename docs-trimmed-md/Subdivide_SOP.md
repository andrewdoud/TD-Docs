

# Subdivide_SOP

Subdivide SOP - TouchDesigner Documentation




# Subdivide SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Subdivide SOP takes an input polygon surface (which can be piped into one or both inputs), and divides each face to create a smoothed polygon surface using a Catmull-Clark subdivision algorithm. Especially useful for avoiding the angular appearance often associated with polygonal models - without adding lots of extra geometry to the entire object. For best results, polygons should be convex and relatively uniform in distribution.
Subdivision surfaces also allows you to create the smoothed surface based on a polygon control shape. As the control shape changes, so does the smooth shape within.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[subdivideSOP\_Class](https://docs.derivative.ca/SubdivideSOP_Class "SubdivideSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Creases and Cracks](#Creases_and_Cracks)
  + [2.1 Creases](#Creases)
  + [2.2 The Crease Algorithm](#The_Crease_Algorithm)
  + [2.3 Closing Cracks](#Closing_Cracks)
* [3 Parameters - Page](#Parameters_-_Page)
* [4 Example](#Example)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Creases and Cracks
### Creases
Creases control the strength of pull of the polygon faces on the subdivision surfaces, much like a magnet drawing the surface towards the reference polygon. They can be applied selectively using the Creases field to specify an input group to use.
Creases work by controlling the strength of the pull of the polygon faces on the subdivision surfaces, like a magnet drawing the surface towards the reference polygon. The figure below shows the result of setting the Crease Weight to `0, 1, 2` reading from left to right. As the weight increases so the pull effect strengthens and the shape approaches the reference polygon.
[![Subdivision-Creases.gif](https://docs.derivative.ca/images/5/5e/Subdivision-Creases.gif)](https://docs.derivative.ca/File:Subdivision-Creases.gif)
  

### The Crease Algorithm
If there is a second input:
If the Override button is enabled, each edge defined in the second input will have its edge crease weight set to the value of the override.
If the vertex attribute "`creaseweight`" exists on the second input, each matching edge in the input will have its crease weight set to the maximum of the vertex attributes for any shared edges.
If the primitive attribute "`creaseweight`" exists on the second input, each polygon in the second input will set matching edges to the appropriate weights.
If there is no second input:
If an override is specified, the value of the override is used for all edges in the sub-divided surface.
If the vertex attribute "`creaseweight`" exists, this attribute will be used to define the crease weights on the edges of the surface.
If the primitive attribute "`creaseweight`" exists, this attribute will be used to define the crease weights for the subdivision surface.
When defining crease weights on shared edges, the maximum of the weights of the shared edges is used. For example, if two polygons share an edge and the primitive attribute is used, the maximum of the crease weight will be used for the shared edge.
  

### Closing Cracks
Cracks can be closed by either Pull Cracks Closed or Stitch Cracks Together, so only one of these two options can be chosen at a time from the Surrounding Faces parameter. Bias applies only to Pulling, and is disabled when Stitching is chosen.
A crack is formed by a single edge on the non-subdivided area and multiple edges on the subdivided area. The Surrounding Faces menu determines what will will happen to the single edge on the non-subdivided area, and in more generally, to the polygon containing this edge.
If No Edge Division is chosen and cracks are pulled closed, all the points on the subdivided edges are pulled (i.e. moved) to the closest points on the non-subdivided edges. Bias is disabled, when No Edge Division is specified.
If cracks are pulled with the Divide Edges option, the non-subdivided edge is split into many sections, so that each each point on the non-subdivided edge now corresponds to a new point on the subdivided edge. Then, points on the newly divided edge are joined with the points on the subdivided boundary. A Bias of `1` will place these joined points along the subdivided boundary. A Bias of `0` will place them along the non- subdivided boundary (and values between 0 and 1 will place them somewhere inbetween).
Pulling cracks with the Triangulate option will do exactly the same thing as Divide Edges, except it will also triangulate the non-subdivided polygon. This is desirable because pulling the non-subdivided boundary towards the curved subdivided boundary will likely generate a non-planar polygon, so Triangulate will divide this polygon into smaller (planar) ones. Pulling cracks with a Bias of `1` and triangulating usually produces the nicest results.
The Triangulate option is necessary because the [Divide SOP](Divide_SOP.html "Divide SOP") is not designed to handle (very) non-planar polygons.
The Stitch Cracks Together option, on the other hand, inserts new polygons (triangles) to close up the cracks. When No Edge Division is chosen, many triangles are created, each having one vertex on one point of the non-subdivided edge.
When Divide Boundary Edges is chosen, the non-subdivided edge is divided, so there are more points available to be used for triangles. The resulting triangles are more regularly shaped (not as long and skinny). The Triangulate option will again triangulate the non-subdivided polygon, although this option is less likely to be used becuase this polygon should remain planar during stitching.
  

## Parameters - Page
Group `subdivide` - Subset of input to use as a polygonal mesh to subdivide. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Creases `creases` - This field allows you to specify a subset of the second input to use as creases. The elements of the second input specified by the Creases field are used as creases. Each edge in a crease polygon corresponds to the edge in the polygon mesh which has the same point numbers. Point position is irrelevant. For polygon edges to be classified as the same edge, they must share the same points. Merely being physically close is not sufficient.
The primitive attribute `creasesharpness` is used to determine the sharpness of the specified creases unless overridden.

Depth `iterations` - How many iterations to subdivide. Higher numbers give a smoother surface.
Override Crease Weight Attribute `overridecrease` - Determine if the crease sharpness should be determined by the primitive or vertex `creaseweight` attribute or by overridden by this SOP.
Crease Weight `creaseweight` - If the crease weight is overriden, this is the weight used.
**Tip:** The default is to have the **Override Crease Weight Attribute** enabled. So you can simply set a value which applies to all the creases. You can, however, set a crease attribute using the Vertex or Primitive SOPs which allows for more control.

Generate Resulting Creases `outputcrease` - If any creases are sharper than the Depth, they will be left over in the resulting geometry. With this parameter enabled, these left over creases are created with the appropriate primitive attribute values, and placed in the specified group.
New Group `outcreasegroup` - Name of the group to place the generated creases into.
Close Cracks `closeholes` - ⊞ - Choose how gaps are handled in the output geometry.
* Do Not Close `noclose` - Don't close cracks.
* Pull Cracks Closed `pull` - Move points on boundary of subdivided area in order to close cracks formed during the subdivision.
* Stitch Cracks Together `stitch` - Add polygons (triangles) to close the cracks caused by subdividing.
Surrounding Faces `surroundpoly` - ⊞ - Choose how to handle the polygons on either side of a crack when pulling or stitching it closed.
* No Edge Division `nodiv` - When No Edge Division is chosen, many triangles are created, each having one vertex on one point of the non-subdivided edge.
* Divide Edges `edges` - Divides edges surrounding the subdivided area when pulling or stitching cracks by inserting new polygons (triangles) to close up the cracks.
* Triangulate `triangulate` - Does exactly the same thing as Divide Edges, except it also triangulates the non-subdivided polygon. This is desirable because pulling the non-subdivided boundary towards the curved subdivided boundary will likely generate a non-planar polygon, so Triangulate will divide this polygon into smaller (planar) ones. Pulling cracks with a Bias of 1 and triangulating usually produces the nicest results.
Bias `bias` - Determines which points are moved when pulling crack closed.
* 0 means move points on subdivided area to meet boundary.
* 1 means move points on boundary to meet subdivided area.
  

## Example
Below, a Subdivide SOP is used to create a subdivision surface from a [Box SOP](Box_SOP.html "Box SOP"). The Depth of the subdivision is set to 2. The [Facet SOP](Facet_SOP.html "Facet SOP") consolidates the points so that the box faces are treated as a unit.
[![SubdivisionSOPeg.gif](https://docs.derivative.ca/images/8/8a/SubdivisionSOPeg.gif)](https://docs.derivative.ca/File:SubdivisionSOPeg.gif)
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Subdivide SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • Subdivide• [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Subdivide_SOP&oldid=24238>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")