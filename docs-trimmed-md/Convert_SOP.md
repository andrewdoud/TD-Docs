

# Convert_SOP

TouchDesigner Documentation




# Convert SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Convert SOP converts geometry from one geometry type to another type. Types include polygon, mesh, Bezier patche, particle and sphere primitive.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[convertSOP\_Class](https://docs.derivative.ca/ConvertSOP_Class "ConvertSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Level of Detail Page](#Parameters_-_Level_of_Detail_Page)
* [4 Parameters - Divisions per Span Page](#Parameters_-_Divisions_per_Span_Page)
* [5 Notes](#Notes)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
From Type `fromtype` - ⊞ - Determines which geometry by type will be converted. The default is All Types:
* All Types `all` - All geometry will be converted.
* Sphere `sphere` -
* Tube `tube` -
* Particles `part` -
* Meta-ball `metaball` -
* Polygon `poly` -
* Mesh `mesh` -
* Bezier Curve `bezcurve` -
* Bezier Surface `bezsurf` -
* NURBS Curve `nurbcurve` -
* NURBS Surface `nurbsurf` -
* Circle `circle` -
* Triangle Strip `tristrip` -
* Triangle Fan `trifan` -
Convert to `totype` - ⊞ - Determines what the above From Type geometry will be converted to. Conversion to Polygons is the default:
  
**Notes**:
Not all geometry can be converted to specific types. For example, a triangulated polygon surface to a single NURBS surface, or a Mesh sphere into a primitive sphere. Also, certain conversions will preserve shapes. For example, converting a Bzier curve to a NURBS curve or a polygonal mesh to a NURBS Surface.
**Circle Notes**: Converting to primitive circles is available for action users who are used to working with polygon circles so that you can convert them to primitive circles for the TouchDesigner Skeleton, Arm, and Limb SOPs.
**Trimmed Surface Notes**: If the primitive to be converted is a curve (NURBS or Bezier) and is flat, a trimmed surface will be generated such that the visible piece coincides with the curve. If the curve is not flat, it will be converted to a non-trimmed surface. The advantage of the trimmed solution is that it yields a very clean surface and handles concave curves perfectly.
* Polygon `poly` -
* Mesh `mesh` -
* Bezier Curve `bezcurve` -
* Bezier Surface `bezsurf` -
* NURBS Curve `nurbcurve` -
* NURBS Surface `nurbsurf` -
* Circle `circle` -
* Trimmed Bezier Surface `trimbezsurf` -
* Trimmed NURBS Surface `trimnurbsurf` -
* Particles `part` -
Connectivity `surftype` - ⊞ - This option is used to select how the points of the created surface are connected.
* Rows `rows` - Creates horizontal lines.
* Columns `cols` - Creates vertical lines.
* Rows and Columns `rowcol` - Both Rows and Columns. Looks like Quadrilaterals in wire frame display, but all polygons are open (if the primitive type is polygon).
* Triangles `triangles` - Build the grid with Triangles.
* Quadrilaterals `quads` - Generates sides composed of quadrilaterals (default).
* Alternating Triangles `alttriangles` - Generates triangles that are opposed; similar to the Triangles option.
  

## Parameters - Level of Detail Page
This affects the use of the U/V/Trim Curve fields:
* For Level of Detail: U, V, Trim Curve Level of Detail
In a spline's case, the span is the curve arc between two breakpoints. The number of divisions per span specifies how many points to be created between the two breakpoints. If the number of divisions = 0, a single segment will connect the two breakpoints; if number of divisions = 1, two edges will be created; etc.
The advantage of Divisions over the Level of Detail is that it tells you exactly how many points you'll end up with - extremely useful for polygonal modeling.
U `lodu` - When set to Level of Detail, controls the number of points or CVs that are used in the newly generated geometry depending on the above setting. Converting a NURBS surface into a polygon mesh with a Level of Detail of 1 results in a fair approximation of the NURBS surface whereas a value of 2 generates a very dense polygonal mesh.
When set to Divisions per Span, specificies the number of divisions per span.
**Tip:** Animate the Level of Detail based on how close your character or geometry is to the camera by using the `primdist()` expression. Then the detail will increase/decrease as the camera gets closer/further away.

V `lodv` - When set to Level of Detail, controls the number of points or CVs that are used in the newly generated geometry depending on the above setting. Converting a NURBS surface into a polygon mesh with a Level of Detail of 1 results in a fair approximation of the NURBS surface whereas a value of 2 generates a very dense polygonal mesh.
When set to Divisions per Span, specificies the number of divisions per span.
**Tip:** Animate the Level of Detail based on how close your character or geometry is to the camera by using the `primdist()` expression. Then the detail will increase/decrease as the camera gets closer/further away.

Trim-Curve `lodtrim` - The trimmed part of a surface will be converted using this Trim lod (level of detail) instead of using an implicit "1" constant.
  

## Parameters - Divisions per Span Page
This affects the use of the U/V/Trim Curve fields:
* For Divisions per Span: U, V, Number of Trim Curve Divisions.
In a spline's case, the span is the curve arc between two breakpoints. The number of divisions per span specifies how many points to be created between the two breakpoints. If the number of divisions = 0, a single segment will connect the two breakpoints; if number of divisions = 1, two edges will be created; etc.
The advantage of Divisions over the Level of Detail is that it tells you exactly how many points you'll end up with - extremely useful for polygonal modeling.
U `divu` - When set to Level of Detail, controls the number of points or CVs that are used in the newly generated geometry depending on the above setting. Converting a NURBS surface into a polygon mesh with a Level of Detail of 1 results in a fair approximation of the NURBS surface whereas a value of 2 generates a very dense polygonal mesh.
When set to Divisions per Span, specificies the number of divisions per span.
**Tip:** Animate the Level of Detail based on how close your character or geometry is to the camera by using the `primdist()` expression. Then the detail will increase/decrease as the camera gets closer/further away.

V `divv` - When set to Level of Detail, controls the number of points or CVs that are used in the newly generated geometry depending on the above setting. Converting a NURBS surface into a polygon mesh with a Level of Detail of 1 results in a fair approximation of the NURBS surface whereas a value of 2 generates a very dense polygonal mesh.
When set to Divisions per Span, specificies the number of divisions per span.
**Tip:** Animate the Level of Detail based on how close your character or geometry is to the camera by using the `primdist()` expression. Then the detail will increase/decrease as the camera gets closer/further away.

Trim-Curve `divtrim` - The trimmed part of a surface will be converted using this Trim lod (level of detail) instead of using an implicit "1" constant.
  

U Order `orderu` - When converting to a spline type, this specifies the degree + 1 of the U or V basis function.
Paste Coordinates
* From Feature Surfaces - The resulting mesh will have the shape of the paste hierarchy (i.e. the top-most features will determine the shape).
* From Base Surface - The resulting mesh will take the shape of the bottom-most surface.
Paste Attributes
* From Feature Surfaces - Each mesh point has the attributes of the top-most feature at that location.
* From Base Surface - The resulting mesh will inherit the primitive attributes of the root surface (e.g. the material), and the point attributes will be those of the root surface as well.
By using base coordinates and feature attributes you are, in fact, pasting attributes onto the surface.

V Order `orderv` - When converting to a spline type, this specifies the degree + 1 of the U or V basis function.
Paste Coordinates
* From Feature Surfaces - The resulting mesh will have the shape of the paste hierarchy (i.e. the top-most features will determine the shape).
* From Base Surface - The resulting mesh will take the shape of the bottom-most surface.
Paste Attributes
* From Feature Surfaces - Each mesh point has the attributes of the top-most feature at that location.
* From Base Surface - The resulting mesh will inherit the primitive attributes of the root surface (e.g. the material), and the point attributes will be those of the root surface as well.
By using base coordinates and feature attributes you are, in fact, pasting attributes onto the surface.

Preserve Original `new` - When checked, the original geometry will be retained along with the converted geometry.
Interpolate Through Hulls `interphull` - This option applies to the conversion between polygonal faces and grids to NURBS and Bzier surfaces and curves. When selected, the resulting curves retain the same topology as the original polygon. When not selected, the polygon points are used as a hull to define the new curve or surface.
Particle Type `prtype` - ⊞ - Selects how the particles are rendered.
* Render as Lines `lines` - Each particle will be rendered as a 2-point line, with the length determined based on the particles velocity. If the particle has no velocity it will just be a single pixel in size.
* Render as Point Sprites `pointprites` - For use with the [Point Sprite MAT](Point_Sprite_MAT.html "Point Sprite MAT"). Each particle is a square of pixels that always face the camera. The size of the square is determined by parameters in the Point Sprite and the `pscale` vertex/point attribute. The point sprites will have texture coordinates generated for them automatically also ((0,0) in the bottom left and (1,1) in the top right).
## Notes
Face to Surface Conversion - When converting from a set of polygons to a mesh, a single mesh will result only if [Facet SOP](Facet_SOP.html "Facet SOP").
Otherwise, each polygon is converted individually into a mesh. In fact, any individual face can be converted to any surface. This is accomplished by cutting the face into three or four adjacent sections, and then creating a patch from them.
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Convert SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • Convert• [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Convert_SOP&oldid=24181>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")